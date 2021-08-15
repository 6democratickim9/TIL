

**11일차 주요목차**

1. Polymorphism 연습 예제
2. interface
3. java.util.Collection:자료구조
   - Set
   - List

-----------

- interface

  > 다양한 계층구조 형성을 통한 **다형성 지원이 목적** 
  >
  > 서버와 클라이언트와의 약속, 소통방식

  - 자바는 **단일 상속이므로 단일 계층구조**를 가지는데 **인터페이스를 이용하면 다양한 계층 구조**를 가질 수 있음

  - 일반적으로 인터페이스는 ``abstract method``와 ``public static final`` 상수만 가질 수 있다

    :point_right: **구현된 메소드는 가질 수 없음**

    (1.8 이상부터 default 및 static 메서드는 예외)

    :arrow_right: 가지면 ``abstract``와 다를 게 없음

- 인터페이스를 구현해두면 **결합도가 낮아지고** 내부에서 업데이트가 되어도 사용자에게 보이지 않음

- ``interface``를 이용하면 **다양한 구현체(하위클래스)들이 업데이트 되어도 외부 영향을 최소화** 할 수 있다

  :point_right: **결합도를 느슨하게** 하여 **유지보수성을 향상**시킬 수 있다

- ### Inheritance 장점
  
  1. **부모 멤버(변수, 메서드)를 물려받아 재사용**
  
  2. **계층구조 형성을 통한 다형성 지원** 
  
     :point_right: Java Interface는 **2번 장점을 다양하게 지원**

```java
public interface Flyer{
	String ID="javaking";
	public void fly();
    //public void landOff(){}
}
public interface Fighter{
    public void fight();
}
//하위 구현 클래스
public class SuperMan extends Person implements Flyer,Fighter{
    //다양한 인터페이스를 implements해서 다양한 계층구조 하에 편입 가능
    //인터페이스의 abstract 메서드는 반드시 구현
    public void fly(){}
    public void fight(){}
}
```

- ``String ID="javaking";`` : public static final 상수로 인식
- ``public void fly();`` : abstract , 추상메서드로 인식
- ``public void landOff(){}``: 일반 구현 메서드는 정의 불가 -> compile error



- 인터페이스끼리는 **다중 상속이 가능**

- jdk 1.8 버전 이상에서는 ``default`` 메서드와 ``static`` 메서드를 **인터페이스에 정의**할 수 있다 

  :point_right: **유지보수성 차원** 

------------



찾아볼것

private, protected 상속될 때 어떻게되는지

abstract

final

