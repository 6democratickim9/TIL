# 그래프 순회

> 그래프에 있는 노드들을 방문하는 과정

- 순회=serach

- 너비우선탐색

  - breadth-first search
  - 넓게 우선적으로 탐색
  - 루트노드를 먼저 방문한 뒤에 자식노드의 depth 순서대로 너비를 우선적으로 고려해서 탐색
  - ![image-20210713230640493](C:\Users\MIN\TIL\data_structure\DFS_BFS.assets\image-20210713230640493.png)

  - 알고리즘

    1. vertex를 먼저 선택 후 visit 했다고 체크

    2. 해당 vertex를 큐 만든 후에 push 해둠

    3. 큐가 비어있지 않을 때까지, 큐가 차있을 때까지 반복

    4. 매 회마다 하나의 vertex를 큐로부터 front에서 빼낸다. 
    5. 빠진 vertex를 v라고 한다면, vertex로부터 주위에 연결된 vertex 중 아직 visit 되지 않은 vertex들을 큐에 추가
    6. 해당 vertex는 한 번이라도 큐에 포함된 적이 있음 이라고 visit 마크
    7. 큐가 빌 때 까지 과정 반복
    8. 큐가 비었는데 그래프 상에 visit 되지 않거나 큐에 한 번도 들어가지 않은 vertex가 존재한다면 그래프는 connect 되어있지 않다고 봄





- 깊이우선탐색

  - depth-first search
  - depth가 깊어지는 순서대로 먼저 탐색
  - ![image-20210713230650911](C:\Users\MIN\TIL\data_structure\DFS_BFS.assets\image-20210713230650911.png)
  - 알고리즘
    - BFS와 모든 알고리즘이 같음
    - 사용하는 자료구조가 BFS는 큐, DFS에선 스택을 사용하게 됨
    - 스택이 비지 않을 때 까지 하나를 꺼내서 인접한 것들 중에 아직 한 번도 스택에 들어가지 않았던 것들을 스택에 추가하는 알고리즘 수행

  

<img src="C:\Users\MIN\TIL\data_structure\DFS_BFS.assets\image-20210713233838392.png" alt="image-20210713233838392" style="zoom:67%;" />