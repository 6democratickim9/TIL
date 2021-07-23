### 자료구조

- Primitive
  - Stack and Queue
    - Stack
      - 자료를 순서대로 쌓아놓은 자료구조
      - LIFO(Last IN Last OUT)
    - Queue
      - 먼저 온 사람은 먼저
      - FIFO(First In First Out)
  - Tree and Graph
    - Tree
      - 관계를 얘기하는 것
      - 위에서부터 밑으로 퍼져나가는 형태
    - Graph
      - 그래프
      - 부모-자식 관계 보다는 인접한 관계를 표현한 자료구조

- Non-Primitive

-------



- 알고리즘
  - 알고리즘의 복잡도, 시간, 시간 소요(몇 개의 인풋이 주어졌는가)
  - 자료와 데이터들이 몇 개의 인풋을 가지고 있는가
  - 몇 개의 인풋을 변수로 잡고 N대비 소모할 것인가 --> 시간복잡도



- Weak Ordering
  - 약하게 순서 매기는 것
  
- Shortest Path
  - 그래프 내에서 두 노드가 주어졌을 때 그래프 내에서 어떤 경로를 따라가야 A-F까지 도달할 수 있는가
  
- Minimum Spanning Tree
  - 트리로 변환 시 선들 가운데 몇 개만 선택
  - 선택 시 적힌 숫자들의 합이 최소가 되도록 + 모든 엣지들이 연결되도록 하는 문제

- Topological Sorting
  - 선행 구조도를 가지고 있음
  - 실제 어떤 순서대로 과목을 수강해야 하는지 나열
  - 나열된 형태이기 때문에 어떻게 분류/정렬할것인지에 대한 문제 해결
  
- Dynaminc Programming
  - 큰 문제를 작은 문제들로 나눔
  - 작은 문제들을 해결한 결과 취합 --> 최종 하나의 결과 도출
  
  -------------
  
  

데이터 타입을 먼저 명시하고 array의 이름을 정하고 사이즈를 정해준다.

int score[10];

C나 C++를 사용하면 메모리의 연속적인 공간을 할당받고 공간 내에서 순서가 형성됨

array를 생성하는 데에는 두 가지 방법이 있음

```
Type d[10];
```

--> 미리 사이즈를 정해둠

동적 array 크기 할당

```
Type *d = new Type [size];
```

동적 메모리를 할당했다면 OS에 돌려주기 위해서는

```
delete [] d;
```

C++ 강좌나 dynamic memory allocation을 찾아보자

- 1차원 array 생성
- 실제로 1차원 array 생성 시

```c++
int arr[10]; //정적 생성

int *arr = new int[10]; //동적 생성
```

- 2차원 array 생성

  ```c++
  int arr[3][4];
  int **a = new int *[3];
  for(int i=0;i<3;i++)
      a[i] = new int[4];
  ```

  

---------

## Dynamic Memory Allocation

- 프로세스가 돌아가는 런타임 내에 영역의 크기를 알려줌으로써 영역을 확보하는 방법
- https://talkingaboutme.tistory.com/entry/Memory-Dynamic-Memory-Allocation

