# 📋 함수의 점근적 분석법

- 알고리즘의 complexity가 n이 크게 증가했을 때 띄는 양상의 방식을 알아보자.

## :one: 세타 노테이션

- ![image-20210721004015772](C:\Users\MIN\TIL\data_structure\AsymtoticAnalysis_2.assets\image-20210721004015772.png)

어떤 함수f(n)이 위의 조건을 만족한다면 

- f(n)을 기준으로 f(n)을 표현하고자 하는 대푯값 gn을 놓고 봤을 떄, g(n) * constant1와 g(n) * constant2 이 있을 때, f(n)이 반드시 둘 사이에 끼어 있도록 하는 g(n)이 있다고 하면 우리는f(n)을 theta of g(n)이라고 표현할 수 있다.
- f(n)이 theta of g(n)이라고 할 때

<img src="C:\Users\MIN\TIL\data_structure\AsymtoticAnalysis_2.assets\image-20210721004502614.png" alt="image-20210721004502614" style="zoom:50%;" />

n이 n0보다 큰 시점으로부터 항상 f(n)은 둘 사이에 끼어 있는 형태가 된다.

### 🖍g(n)은 f(n)의 symptotically tight bound 이다.

> n이 점근적으로 커졌을 때, g(n)이 f(n)을 타이트하게 위아래로 바운드하고 있다고 얘기한다.



## :two: O- Notation

> 세타 노테이션에서 위쪽만을 취하고 아래쪽은 제외한 노테이션

![image-20210721005025876](C:\Users\MIN\TIL\data_structure\AsymtoticAnalysis_2.assets\image-20210721005025876.png)

위의 조건을 만족하는 constant c와 n0가 하나라도 존재하면 f(n)은 Big-O of g(n)이라고 얘기할 수 있다.

<img src="C:\Users\MIN\TIL\data_structure\AsymtoticAnalysis_2.assets\image-20210721005125210.png" alt="image-20210721005125210" style="zoom:50%;" />

- f(n)이 n0를 기점으로 항상 c곱하기 g(n)보다 더 작다는 것을 알 수 있음

- 이 때 g(n)을 f(n)의 asymtotically upper bound라고 얘기한다.

- f(n)이 theta of g(n)이라면 theta는 upper,lower를 포함하는 tight한 바운드

  👉f(n)은 Big-O of g(n) 이라고 얘기해도 맞는 말!

- 알고리즘의 최악의 경우에도 g(n)을 넘어가지 않는다.

## :three: Omega Notation

> 아래쪽으로 바운드하는 한 쪽만 있는 노테이션

- 아래쪽을 바운드 하고있음
- <img src="C:\Users\MIN\TIL\data_structure\AsymtoticAnalysis_2.assets\image-20210721005714023.png" alt="image-20210721005714023" style="zoom:67%;" />

- g(n)은 asymtotically lower bound for f(n)이라고 한다.

- best case 러닝타임을 얘기한다.


## :four: o-Notation & Little Omega Notation

- O Notation과 Omega Notation을 강화하기 위한 Notation

