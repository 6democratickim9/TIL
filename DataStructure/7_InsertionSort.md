# Insertion Sort🗃

- Sorting 알고리즘들이 알고리즘을 디자인하는 다양한 접근법들 제시

  ➕ 앞에서 배운 분석을 통해 효율 정도를 알 수 있음

## Sorting Problem ♨️

- Input으로 N개의 숫자 혹은 오브젝트가 주어졌을 떄

  - Output으로는 Input을 재배열한 시퀀스를 준다

  - 시퀀스가 감소하지 않는 순서로 출력

    ⚠️ 증가하는 순서라고 얘기하지 않는 이유?

    - 같은 값이 있을 때는 permatuation을 항상 증가하는 순서로 만들 수 없기 때문

    :point_right: **시퀀스가 감소하지 않는 순서로 출력**



## Insertion Sort 🗃

- Background

  - 리스트의 element가 k개의 sorting이 되어 있는 array가 있다고 했을 때

    - 새로운 아이템을 array에 추가하는데 sorting되어 있다는 특성이 깨지지 않게 새로운 아이템의 적합한 위치를 찾아서 넣어주는 알고리즘

      

      

      ​									정렬된 array에 14를 추가하는 시나리오 생각하기

<img src="C:\Users\MIN\TIL\DataStructure\7_InsertionSort.assets\image-20210727224858977.png" alt="image-20210727224858977" style="zoom:67%;" />

<img src="C:\Users\MIN\TIL\DataStructure\7_InsertionSort.assets\image-20210727224914955.png" alt="image-20210727224914955" style="zoom:67%;" />

​														

<img src="C:\Users\MIN\TIL\DataStructure\7_InsertionSort.assets\image-20210727225015326.png" alt="image-20210727225015326" style="zoom:67%;" />

- 위와 같은 방법으로 시나리오를 생각한다
- 14와 index들을 하나하나 비교하며 바꿔주기

:point_right: 새로운 아이템의 정확한 위치를 찾아나갈 때 까지 swap을 해주는 알고리즘



### 알고리즘 정리 :desktop_computer:

1. 제일 앞에 있는 1개의 array가 sort되었다고 가정
2. 두 번째 element부터 그 앞의 부분이 sorting되어 있다고 가정
3. 올바른 위치를 찾아서 insertion해주는 알고리즘

```c++
template <typename Type>
void Insertion__Sort(Type *_array,int _n){
    for(int i=1;i<_n;i++){
        for(int j=i;j>0;j--){
            if(_array[j-1]>_array[j]){
                std::swap(_array[j-1],_array[j]);
            }
            else{
                break;
            }
        }
    }
}
```

일반적으로 ``temp=a,a=b,b=temp``방식의 코드를 많이 사용함

:point_right: 조금 더 최적화 하는 방법

1. tmp=insertion하고자 하는 아이템 임시 저장
2. tmp보다 작은 아이템이 나올때까지다른 element들을 오른쪽으로 shift
3. tmp보다 작은 아이템이 등장하면 쉬프팅을 멈추고 tmp를 빈자리에 넣어줌

📝 asymptotic analysis측면에서는 complexity가 같지만 **실제 구현측면에서는 더 속도빠른 알고리즘!**

- 구현된 알고리즘

- ```c++
  template <Typename Type>
  void Insertion_Sort_without_Swap( Type*_array, int n){
      for(int i=1;i<_n;i++){
          Type tmp=_array[i];
          for(int j=i;j>0;j--){
              if(_array[j-1] > tmp){
                  _array[j] = _array[j-1];
              }
              else{
                  _array[j]=tmp;
                  break;
              }
          }
          if(_array[0]>tmp){
              _array[0]=tmp;
          }
      }
  }
  ```

  