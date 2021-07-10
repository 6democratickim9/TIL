## 비선형 자료구조 :ledger:

### :deciduous_tree:Trees 

- **노드들의 집합체**
- **계층적인 관계**를 나타내는 자료구조
- 첫 번째 노드 루트: **뿌리노드**
- 하나의 노드는 **다양한 개수의 자녀들을 가질 수 있음**



### :palm_tree: Trees 용어 

- 모든 노드들은 **0개 혹은그 이상의 자녀**들을 가지고 있음
- 루트 노드를 제외한 각각의 노드는 **정확하게 하나의 부모노드**를 가지고 있음
- **degree**
  - 노드가 가지고 있는 **자녀의 숫자들**
  - ![image-20210707201459088](C:\Users\MIN\TIL\data_structure\tree.assets\image-20210707201459088.png)
  - 여기서 I의 degree는 3
    - deg(I)=3
  - JKL은 sibling 노드라고 부름

- 자녀노드의 개수에 따라 leaf 노드인지 internal 노드인지 구분
  - **leaf 노드** :leaves:
    - 자녀 없는 노드
  - **internal 노드 :inbox_tray:**
    - leaf노드를 제외한 자녀 있는 노드들

![image-20210707201900868](C:\Users\MIN\TIL\data_structure\tree.assets\image-20210707201900868.png)



### :evergreen_tree:Trees 의 종류 :evergreen_tree:

----

#### :tanabata_tree: Ordered Trees

- 자녀들의 순서가 존재할 때

#### :deciduous_tree: Unordered Trees

- 자녀들의 순서가 중요하지 않을 때
- 일반적으로 unordered 트리가 많음



### Tree의 경로

> 노드들의 시퀀스

- 노드들을 순서대로 표현한 것
- 트리에서 경로가 정의되려면 **바로 앞에 있는 노드가 다음 노드의 부모**여야만 경로가 정의됨
  - PATH B-E-G
    - 길이는 2--> 선의 갯수로 친다!

![image-20210708234032394](C:\Users\MIN\TIL\data_structure\tree.assets\image-20210708234032394.png)

- 경로의 길이는 몇 개의 선을 거쳐갔느냐가 중요
- 좀 더 큰 트리에서 살펴보면

![image-20210708234114758](C:\Users\MIN\TIL\data_structure\tree.assets\image-20210708234114758.png)



### :christmas_tree: Tree의 깊이

- 노드를 선택했을 때 루트의 노드로부터 선택된 노드까지 경로는 반드시 하나밖에 존재하지 않음
  - 만약 아닐 시 그래프는 트리가 아니게 됨!

- 반드시 노드와 루트 사이의 경로는 유니크하다
- TREE에서 DEPTH란?
  - 루트노드로부터 해당 노드까지의 경로의 길이
  - ![image-20210708234748183](C:\Users\MIN\TIL\data_structure\tree.assets\image-20210708234748183.png)
    	- E의 depth: 2
    	- L의 depth: 3



### :christmas_tree: Tree의 높이

> 노드들 중 depth가 가장 큰 값

- 트리 내에 루트노드가 1개: 트리의 height는 0

- 정의에 따라서 아무 노드가 없어도 트리로 부를 수 있음
  - empty tree의 height: -1
- 트리 내에서 노드A에서 노드 B까지 경로가 존재한다고 했을 때
  - A: ancester
  - B: descendant
- 노드는 그 자체로 자기자신의 조상이면서 동시에 자손

- **strictly descendant**
  - 자기자신이 자기 자신의 자손이나 부모가 되는 것을 **금지시키는 것**으로 쓸 수 있음
  - 일반적으로 **조상, 자손은 자기자신을 포함하여 얘기**하는 것

- 루트 노드는 트리의 모든 다른 노드의 조상

![image-20210708235610112](C:\Users\MIN\TIL\data_structure\tree.assets\image-20210708235610112.png)

- BCDEFG- B노드의 자손(자기자신 포함)

  ![image-20210708235651222](C:\Users\MIN\TIL\data_structure\tree.assets\image-20210708235651222.png)

- IHA- I 노드의 조상(자기자신 포함)





### :book: 실제 트리 자료구조로 표현하기

- 자녀노드들의 list representation 을 주로 사용

  