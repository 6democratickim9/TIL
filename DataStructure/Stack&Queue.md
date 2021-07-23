## Stack & Queue

- Stack:eyes:
  - 선형자료구조의 하나
  - LIFO의 특성을 가지고 있음
  - Last-in First-out
    - 마지막으로 들어간 요소가 처음으로 나온다
    - 데이터 입력 혹은 제거 시 스택의 최상단에서만 이루어짐
  - Top
    - 스택의 최상단
  - Push
    - 특정 아이템을 최상단에 추가
  - Pop
    - 스택의 최상단에서 하나의 아이템을 제거



- Queue :first_quarter_moon:
  - FIFO
    - First-in First-out
    - 먼저 들어간 데이터가 제일 먼저 나옴
    - 스택보다 합리적인 자료구조
  - 인터넷 웹서버 등
  - insertion 같은 경우 끝에서 발생
  - 삭제하는 오퍼레이션은 큐의 앞에서 발생
  - Front
    - 헤드
    - 삭제 발생
  - Rear/back/tail
    - insertion 발생
    - enqueue
      - 큐에 아이템 삽입
      - rear 에서 이루어짐
    - dequeue
      - 데이터 삭제
      - front 에서 발생
  - Linear Queue
    - 데이터를 삭제하는 과정에서 앞에 공간이 있음에도 불구하고 더 이상의 데이터를 추가할 수 없는 상황 발생
  - Circular Queue
    - 공간 최대한 효율적으로 사용 가능
    - 어느 시점이 되면 다시 0으로 돌아오는 형태로 이루어져 있음
    - 실제로 구현하기 위해 나머지 연산자를 사용해 구현
    - 실제 큐는 선형자료구조이지만 동그랗게 말아서 공간을 전ㅊ적으로 다 활용 가능한 형태로 구현

- STL
  - standard template library
    - 많은 자료들을 제공하고 있음
    - 많이 사용되는 알고리즘도 구현되어있음 

