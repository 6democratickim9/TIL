# :chart: Graph

> 그래프란 데이터 사이의 인접한 정보를 저장하는 자료구조

- 그래프에는 오브젝트와 relationship 존재

- **오브젝트**

  - 저장하고자 하는 객체들

- **관계성**

  - edge로 연결하는 것

  - ex) ![image-20210709000432083](C:\Users\MIN\TIL\data_structure\graph.assets\image-20210709000432083.png)

    인천: 오브젝트

    인천 - 서울 : '-'가 관계성

- **vertex**

  - 오브젝트를 표현하는 노드

- **arc / link**

  - 관계를 표현하는 엣지들

- 네트워크나 인접관계를 가진 것들을 주로 그래프로 표현



## :chart_with_upwards_trend: Undirected Graph

> 방향 없는 그래프

- ![image-20210709000841991](C:\Users\MIN\TIL\data_structure\graph.assets\image-20210709000841991.png)

  E={{v1,v2},{v3,v5},{v4,v8},{v4,v9},{v9,v6}}

  - 방향이 없는 그래프에서 v1,v2는 각 방향으로 가는 엣지 모두가 있다고 가정

    - v1->v2 && v2->v1

  - 스스로에서 스스로 가는 엣지가 없다고 가정했을 때

  - V개의 vertex가 있는 undirected 그래프에서 최대한 많은 엣지의 개수

    - V_C_2라고 표현되는 조합을 하게되면 undirected 그래프에서 최대 개수 구할 수 있음
    - (V**2-V)/2

    ![image-20210709001640840](C:\Users\MIN\TIL\data_structure\graph.assets\image-20210709001640840.png)

    <img src="C:\Users\MIN\TIL\data_structure\graph.assets\image-20210709001953066.png" alt="image-20210709001953066" style="zoom: 67%;" />



> Vertex 7개: A to G까지 있는 상황
>
> 9개의 엣지가 있는 그래프

- 그래프의 degree도 자신의 이웃개수를 degree로 정의

  ![image-20210709001825823](C:\Users\MIN\TIL\data_structure\graph.assets\image-20210709001825823.png)

> A의 degree: D,B,E (3)
>
> F의 degree: C (1)
>
> G의 degree: X (0)



<img src="C:\Users\MIN\TIL\data_structure\graph.assets\image-20210709001937279.png" alt="image-20210709001937279" style="zoom:67%;" />

- **adcejent**
  - 점을 기준으로 연결되어 있는 것
- **neighbor**
  - 하나의 엣지로 곧바로 갈 수 있는 노드
  - vertex의 집합





### 1) Sub Graph

>  오리지널 그래프에서 엣지와 vertex들을 추출한 그래프

- 서브그래프에 존재하는 모든 vertex와 모든 엣지들은 **오리지널 그래프에 존재**해야만 서브그래프라고 할 수 있음음

  - <img src="C:\Users\MIN\TIL\data_structure\graph.assets\image-20210709002400422.png" alt="image-20210709002400422" style="zoom:50%;" /><img src="C:\Users\MIN\TIL\data_structure\graph.assets\image-20210709002419822.png" alt="image-20210709002419822" style="zoom:50%;" />

    ​				ORIGINAL										SUB



### 2) 경로 

- **Undirected Graph**

  - v0 에서 vk로 가는 경로

  - **경로의 길이**

    - ***몇 개의 엣지를 거쳐갔는가***

    - 트리와 같음

    - Vertex의 갯수 X

      

![image-20210709002913621](C:\Users\MIN\TIL\data_structure\graph.assets\image-20210709002913621.png)



- ABECF 의 length: 4



- #### Trivial Path

  - length(0)
  - 자기 자신에 머물러 있는 것

- #### Simple Path

  - 처음과 마지막을 제외하고 안에서 **중복이 없는** 경로

  - ##### Simple Cycle

    - Simple Path의 특수한 경우
    - Simple Path이면서 **처음과 마지막 vertex가 같은 경우**



### 3) Connectedness

> 연결성

- 그래프가 connected인가/아닌가
- 어떤 노드를 찍어도 연결되어 있을 때
- 한 pair라도 연결되어 있지 않으면 connected라고 하지 않음



### 4) Weighted Graphs

- 연결된 버텍스 사이에 **숫자나 값을 부여한 것**
  - ex) 대전-수원 사이의 거리
  - 얼마나 많은 에너지를 사용해야 하는가
- Weighted Undirected Graph라고 표현할 수 있음
- 그림을 그릴 때는 **weight값들은 엣지의 옆에** 써준다.

<img src="C:\Users\MIN\TIL\data_structure\graph.assets\image-20210709003708709.png" alt="image-20210709003708709" style="zoom:67%;" />

- 이런 그래프에서 path length는 경로를 따라 갔을 때 엣지에 써있는 weight의 합으로 표현됨
  - A-D-G의 path length: 5.1+3.7=8.8
  - A-D-G와 A-C-F-G의 path length는 당연히 다름
- Shortest Path문제
  - 두 개의 vertex가 주어졌을 때, weighted 그래프에서 path length가 최소화되는 경로를 찾는 문제
  - A-G의 shortest path: A-C-F-D-E-G



### 5) Tree

- Tree도 그래프의 한 종류

- 주어진 그래프가 트리가 되려면?

  - 그래프가 **연결**되어 있어야 함
  - 모든 vertex에서 모든 다른 vertex로 **경로가 존재해야 함**
  - 경로가 **유니크**해야 함

- 엣지의 개수가 노드의 개수보다 하나 작음

- **사이클 존재하지 않음**

  - 만약 주어진 트리에 **엣지를 추가하면 트리에 사이클이 생김**

- 엣지 제거 시 트리는 **연결이 끊김**

  - 서로 다른 그래프/트리로 나뉨

- #### Forest

  - **트리들의 집합**
  - tree의 정의에서 연결의 강제성을 제거한 것
  - **사이클이 없음**
  - **vertex개수>edge개수**
  - 트리의 개수
    - **vertex개수-edge 개수**



## :bar_chart: Directed Graph

> 엣지의 방향성이 존재하는 그래프

- 각 vertex에 path가 존재한다면 **양방향성을 띄고 있지 않음**

- Degree

  - #### **In_degree**

    - ##### 도착지점(나) 로 들어오는 edge의 개수

  - #### **Out_degree**

    - ##### 출발지점(나)로부터 출발하는 엣지의 개수

      - ##### Source

        - **in_degree가 0인 것**
        - 나가기만 하는 소스
        - in degree 가 0 인 vertex를 source vertex라고 표현

      - ##### Sink

        - out_degree가 0인 것