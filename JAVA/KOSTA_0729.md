2일차 주요목차 :coffee:

- JAVA SE 개발 환경설정
- JAVA 기본소개
- JAVA 기본 프로그램 작성 및 실행
- 객체지향 개념
- JAVA기본문법

--------

- 개발 도구
  - Java jdk
- ide
  - 통합 개발 환경
  - 우리는 ide로 eclipse를 사용해서 개발함

:point_right: jdk설치, ide인 eclipse를 설치 후 각각 설정

- Java 기본 소개

  1. 객체 지향 언어

  2. 네트워킹을 위해 고안된 언어

     - 홈네트워크를 위해 1990년대 초반에 oak라는 이름의 언어로 탄생

     - 이후 라이센스 관련하여 Java라는 이름으로 변경

  3. 플랫폼 독립적

     - OS별로 프로그램을 만들지 않아도 됨 (OS별로 JDK를 제공)
     - 한 번 작성한 프로그램은 어떤 환경에서도 동일하게 동작

     >  "Write Once, Run AnyWhere"

- JDK
  - Java Development Kit
  - 자바 개발 도구
- JRE
  - Java Runtime Environment
  - 자바 개발 환경
- JVM
  - Java Virtual Machine
  - 자바 가상 기계
  - OS와 자바 프로그램과의 통역자 역할

JDK>JRE>JVM

### Java 기본 프로그램 작성 및 실행

- 개발자는 Hello.java 라는 프로그램을 작성
- command line 상에서 ``javac Hello.java`` 명령어를 입력하면 java 파일을 이용해 컴파일된 class 파일이 생성된다
  - 컴파일은 jvm이 해석하기 위한 bytecode, 즉 , java Hello 라는 명령어로 class파일을 실행하면 실행결과가 출력된다
- 위 과정을 ide 통합개발환경인 eclipse에서는 저장시에 컴파일되고 실행 단축키 ``ctrl``+``f11`` 로 class를 실행한다



### 객체지향개념 :computer:

- 분석 설계 기법 중 하나

- 시스템의 기본 단위를 객체로 상정하고

- 객체와 객체의 관계를 중심으로 분석 설계하는 기법을 말한다

  

  #### 1) 객체

  - 시스템의 기본 단위, 시스템을 구성하는 주요 사물이나 개념을 객체로 상정
  - 객체는 속성과 기능으로 구성
  - 속성
    - variable, attribute
  - 기능
    - method,operation

  #### 2) 클래스

  - 객체를 위한 틀/ 설계도

  ####  3)변수

  - 정보를 저장하는 공간(정보는 변경 가능)

  #### 4) 메서드

  - 객체의 기능을 정의



### 소프트웨어 개발 수명주기

- 요구사항 분석 -> 설계-> 개발-> 테스트 -> 운영(유지보수) 단계로 구성

### 소프트웨어 개발 방법론

- 폭포수 모델 :man_playing_water_polo:

  - 단계별 완료 후 다음 단계 수행, 애자일 모델 

  :arrow_right:반복, 점중

TDD

- Test Driven Development
- 반복 테스트를 이용한 소프트웨어 방법론

UML

- 통합 모델링 언어
- 분석 단계
- 설계 단계
- OOAD(Object Oriented Analysis & Design 객체 지향 분석 설계 )를 위한 표기 언어 



-------------

## :one: 예제 

```java
package step1; 
public class TestMessage { 
	public static void main(String[] args) {
		System.out.println("굿모닝!!");
	}
}//실행 ctrl+f11
```

- ``package step1;``
  - 패키지 선언부 , **패키지는 class들을 디렉토리별로 분류**하여 관리하기 위해 사용 , **패키지명은 소문자로 명시** 
    ``ex) package org.kosta.cafe.model;``
    ``ex) package org.springframework.util;``
- ``public class TestMessage``
  - class 선언부 , class 명은 첫글자는 대문자 , 합성어의 첫글자는 대문자 , 나머지는 소문자로 명시 -> camel case 
- ``public static void main(String[] args)``
  - 메인 메서드 : 자바 프로그램의 시작점 -> **메인 메서드가 있어야 실행 가능**

## :two: 예제

```java
package step2;
public class Person {
	String name="아이유";
	public void eat() {
		System.out.println(name+" 점심 먹다");
	}
}

```

- ``package step2;``
  - 패키지: 소문자로 구성 , 디렉토리별로 클래스를 관리  
  - 클래스 정의 : 대문자로 시작 

- ``public class Person``

  - ``public`` : 접근 제어자 access modifier , public 은 어디서나 접근할 수 있는 가장 넓은 범위의 접근제어자 
  - ``class`` : class 를 정의할 때 사용하는 자바 키워드(예약어) 
  - ``Person`` : 클래스명

- ``String name="아이유";``

  - ```java
    /*  여러 줄 주석 
     * 
     *   인스턴스 변수 : 객체의 속성을 저장하는 공간 
     *   변수 선언 및 할당 
     *   String : 데이터 타입, 문자열 데이터를 저장할 때 명시하는 데이터 타입
     *   name : 변수명 
     *   = : assign 대입 또는 할당 
     *   "아이유" : 실제 데이터 
     */
    ```

- ``public void eat``
  - ``메서드`` : 객체의 기능을 정의
  - ``public`` : 접근제어자 ( 가장 넓은 범위 ) 
  - ``void`` : return 값이 없을 때 명시하는 자바 키워드 

## :three: 예제

```java
package step2;
public class TestPerson {
	public static void main(String[] args) {
		Person p=new Person();
		System.out.println(p.name);
		p.eat();
		p.name="이강인";
		System.out.println(p.name);
		p.eat();
	}
}
```

- ``public class TestPerson;``
  - Person class를 이용해 Person 객체(Object) 를 생성해 변수와 메서드를 테스트하는 목적을 가진 클래스 

- ``Person p=new Person();``
  - 객체 생성을 위한 코드라인 
    - ``Person`` : 클래스명이고 참조형 데이터 타입이다 
    - ``p`` : 변수 , 참조변수 , 객체를 참조하기 위한 주소값을 저장하는 공간 
    - `` = ``: assign 할당 
    - ``new ``: 객체 생성을 위한 자바 키워드 
    - ``Person()`` : 생성자 constructor 
    - 객체의 멤버(속성과 기능)에 접근할 때에는 참조변수.속성 또는 참조변수.메서드()  형식으로 접근해 실행한다 
- ``System.out.println(p.name);``
  - 객체의 속성(변수)에 접근해 값을 출력 
  - 객체의 기능 , 메서드를 호출해서 실행 

- ``p.eat();``
  - 변수 즉 속성값을 재할당 

## :four: 예제

```java
package step3;

public class Car {
	//인스턴스 변수,  정수형 데이터를 저장하기 위해 int 형으로 선언 
	int price;
	//인스턴스 변수, 문자열 데이터를 저장하기 위해 String 형으로 선언 
	String model;
	//메서드 
	public void go() {
		System.out.println(price+"만원 "+model+" 가다");
	}

}
```

```java
package step3;

public class TestCar {
	public static void main(String[] args) {
		//Car 객체 생성 
		Car c=new Car();
		//Car 객체의 price 변수에 2000 을 할당 
		c.price=2000;
		System.out.println(c.price);//할당한 Car 객체의 price 속성값을 출력 
		c.model="K5";
		System.out.println(c.model);
		c.go(); // 2000 만원 K5 가다 
	}
}
```

## :five: 예제

```java
package step4.method1;

public class Person {
	/*
	 * method case 1 
	 * 매개변수와 리턴값이 없는 메서드 
	 * 호출되면 실행되는 메서드 
	 */
	public void eat1() {
		System.out.println("먹다");
	}
	/*
	 * method case 2 
	 * 매개변수가 정의된 메서드 , 호출한 측에서 데이터(argument:전달인자)를 
	 * 매개변수(parameter)로 전달받는다
	 * 전달받은 매개변수의 데이터를 이용해서 실행한다 
	 */
	public void eat2(String food) {
		System.out.println(food+" 먹다");
	}
	/*
	 * method case 3 
	 * 리턴값이 존재하는 메서드 , 호출한 측으로 메서드 실행 결과를 반환한다
	 * 리턴값이 있을 때는 void 대신 리턴값의 데이터 타입을 명시해야 한다 
	 * 리턴을 명시하는 코드라인은 메서드 마지막 부분에 존재해야 하며 
	 * 메서드 별로 한번만 실행가능하다 
	 */
	public String eat3() {
		System.out.println("eat3 method 실행");
		return "eat3 메서드 실행결과";
	}	  
}
```

```java
package step4.method1;
/*
 * Method 케이스별로  테스트 하는 예제  
 * 1. 매개변수와 리턴값이 없는 경우 
 * 2. 매개변수가 있는 경우 
 * 3. 리턴값이 있는 경우 
 */
public class TestMethod1 {
	//메인메서드 : 프로그램의 시작점 
	public static void main(String[] args) {
		Person p=new Person();//Person 객체 생성 
		p.eat1();//메서드 호출 
		p.eat2("카스");//eat2 메서드의 매개변수parameter에 알맞는 전달인자(argument)를 명시
		p.eat2("치킨");
		//리턴값이 있는 메서드를 호출하여 결과값을 반환받아 출력해본다 
		String result=p.eat3();
		System.out.println("main:"+result);
		//위의 두 라인을 아래와 같이 한라인으로 표현할 수 있다 
		System.out.println("main:"+p.eat3());
	}
}
```



## :six: 예제

```java
package step4.method2;

public class Calculator {
	/*
	 * 매개변수 parameter 2개를 정의 
	 * 더하기 연산 결과를 return 한다 
	 * 이 때 연산 결과의 type이 정수이므로 int 형으로 명시한다
	 */
	public int plus(int i,int j) {
		return i+j;
	}
	public int minus(int num1,int num2) {
		return num1-num2;
	}
}
```

```java
package step4.method2;

public class TestMethod2 {
	public static void main(String[] args) {
		Calculator c=new Calculator();
		//전달인자 argument 2개를 메서드 호출시 전달
		int result=c.plus(2,2);
		System.out.println("연산결과:"+result);
		System.out.println("연산결과2:"+c.plus(3, 5));
		int num1=7;
		int num2=5;
		result=c.minus(num1,num2);
		System.out.println("연산결과3:"+result);
	}
}
```

