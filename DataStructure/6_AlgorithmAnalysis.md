# 알고리즘 분석👩🏻‍💻

- ### Asymptotic behavior👩🏻‍🏫

  - n이 증가했을 때, 알고리즘이 요구하는 런타임이 얼마나 증가하게 되는지가 기반이 됨
  - 알고리즘의 asymtotic behavior는 알고리즘이 n만큼 커졌을 때 잘 작동되는지 알아보는데 중요한 정보를 제공

**👉🏻 큰 n에 대해 동작하게 된다면 complexity를 낮추는 노력이 필요할 것**

### Machine Instructions

- 계산 프로세서들은 **한정된 숫자의 (정해진 연산)오퍼레이션들만 수행**할 수 있다.

- **인스트럭션 셋:** 인스트럭션들을 모아놓은 것

- 프로그램을 컴파일한다

  - 컴파일 한 후에 **머신이 수행할 수 있는 인스트럭션 레벨로 표현**하겠다는 의미
  - **컴파일 시 타겟을 정해놓음**
  - 코드로 짠 것을 machine language 로 translation 하는 과정에서 **target을 정해줌**

- 특정 Instruction은 특정 CPU에서 정확하게 **몇 번의 사이클에 수행되는지 정해져있음**

- 프로그램이 정확이 **어떤 instruction으로 이루어져있다는 것을 알면** 얼마만큼의 시간이 소비되는지 **계산 가능**

  ✋🏻 **캐시로 인해 정확한 계산은 힘들다!**

  - 램을 CPU의 캐시로 가져오는 데 **많은 CPU 사이클을 필요로 함**

- Assembly가 machine language에 가장 가까움(Low-Level Language)
- Python, C++,C#: High-Level Language(사람에 가장 가까운 언어)
- C: Mid-Level Language(로우레벨과 하이레벨 섞임)

### Operations

- constant time에 수행될 수 있음

- memory allocation/deallocation은 간단한 오퍼레이션보다 훨씬 느림

- 느린 이유는 메모리 할당 시 OS와 커뮤니케이션 하는 과정에서 간단 연산에 비해 100배씩 느린 경우가 있음

  ##### ⚠️singel CPU 인스트럭션에 수행가능하기 때문에 constant time으로 취급함

- object oriented language에서 클래스를 사용할 시

  - class의 new operator를 돌릴 때, 생성자나 파괴자를 호출하게 되는데 constructor에서 무엇을 할 지 알 수 없음 -> 배제
  - 단순히 메모리만 받아오는 것이 constant time에 가능하다고 하는 것

  



- ## Control Statement

  - if문으로 얘기하는 condition

  - if (condition)-> true일때: statement 수행/ false:else statement 

  - complexity가 두 가지로 나뉨

    1. condition을 test하는 complexity
    2. 결과에 따른 수행에 발생하는 complexity

    👉🏻일반적으로 컨디션 테스트 complexity는 constant time으로 생각

- ### Condition-controlled Loops

  - 반복문

- ### Switch  Statements

  - if문과의 차이점
    - switch: 비교 대상이 컴파일 시점에서 반드시 정해져 있는 값이랑만 비교 가능
      - 컴파일러가 어디로 점프하는지
    - if: i 가 무엇과 같은지 처리 가능

- Serail Statements
  - n개의 랜덤 리스트 속에서 특정 값을 찾는 경우

- Function
