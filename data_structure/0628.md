 

## 배열과 리스트

메모리에는 어떻게 기록이 되어있을까?

``` c++
int score[3]={52,17,61};
```

integer = 4바이트

4바이트의 메모리 공간

![image-20210628143540188](C:\Users\MIN\TIL\data_structure\0628.assets\image-20210628143540188.png)

- 메모리에서의 주소
- 52 라는 값은 현재 4칸의 메모리 공간 사용중

- score[0]은 4바이트의 첫 번째 공간 할당
- 연속적으로 4바이트씩 다음 element, 다음 element가 값을 메모리에 저장하고 있음

![image-20210628143746910](C:\Users\MIN\TIL\data_structure\0628.assets\image-20210628143746910.png)

array를 선언하게 되면 물리적인 램에서도 연속적인 공간 할당



### 포인터

- &
  - 주소 연산자
  - reference operator
- *
  - dereference operator
  - reference 를 역으로 따라감
  - 포인터가 가리키고 있는 값 자체에 직접적인 접근 가능





### Linked Lists

- 자료들의 선형적인 모음
  - 배열과 같다
- 모든 노드가 자신의 값과 다음 값을 pointing 하는 자료구조
  - array: 데이터에 바로바로 접근 가능
  - 모든 노드가 어떤 데이터와 다음 값에 대한 링크를 검 --> 후크를 채우는 식의 자료구조
  - 자연스러운 insertion 가능

```c++
typedef int Data;

typedef struct _Node
{
    Data item;
    struct _Node*next;
}Node;
   
typedef struct
{
    Node *head;
    int len;
}LinkedList;
```





