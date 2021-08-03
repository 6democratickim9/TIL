**4일차 주요목차**
- review 
- java data type : primitive data type, reference data type 
- 객체 초기화 단계 , java memory 
- 제어문 
   조건문 if , else if , else 
   조건문 switch case 



객체를 초기화 해야 될 필요가 있을 때 생성자 생성

# :one: 자바의 데이터 타입

- ## **primitive data type**

  - 정수형
    - 정수형의 기본형은 int형
  - 실수형
    - 실수형의 기본형은 double형
  - 문자형
    - 문자형은 오직 한 문자만(char)
  - 논리형
    - 논리형은 True || False 만 가능

- ## **reference data type**

  - 참조형 데이터 타입
  - 참조형 데이터 타입은 기본형을 제외한 모든 타입을 말한다
  - 변수 앞에 선언된 데이터 타입이 참조형인 경우 이 변수를 참조변수라고 한다
  - 참조변수에는 **객체를 참조하기 위한 주소값이 저장**되어 있음

    

  1) 

  ``String s;`` s 변수의 데이터 타입은 참조형 데이터 타입이자 클래스명인 String
  
  ``Person p;`` p 변수의 데이터 타입은 참조형 데이터 타입이자 클래스명인 Person
  
  
  
  2. ​	
  
  ``Person p = new Person();``
  
  - ``Person``: 참조형 데이터 타입이자 클래스명
  
  - ``p``: 참조 변수 reference variable
  
  - ``=``: assign 할당 or 대입
  
  - ``new``: 객체 생성시 명시하는 자바 키워드
  
  - ``Person()``:생성자 (객체 생성시 실행되는 영역)
  
    :point_right: ``new Person()``으로 객체가 **heap 영역에 저장되고 이 때 이 객체를 참조**하여 제어하기 위한 **객체의 주소값**이 반환
  
    - 이 반환되는 객체의 주소값을 **``p``라는 참조변수에 저장**하게 됨
  
  
  
  ```java
  package step3;
  
  public class Person {
  	private String name;
  	private int money;
  	public Person(String name, int money) {		
  		this.name = name;
  		this.money = money;
  	}
  	public String getName() {
  		return name;
  	}
  	public void setName(String name) {
  		this.name = name;
  	}
  	public int getMoney() {
  		return money;
  	}
  	public void setMoney(int money) {
  		this.money = money;
  	}
  	
  }
  ```
  
  ```java
  package step3;
  
  public class TestReferenceDataType {
  	public static void main(String[] args) {
  		//아래는 생성자 매개변수parameter 리스트에 알맞는 
  		//인자 argument 를 전달하지 않았으므로 error 
  		//Person p=new Person();
  		Person p; //선언 Person 참조형 타입 , p 는 참조변수 
  		//객체 생성 ( heap 영역에 객체 생성 , 주소값 반환 ) 
  		//p 참조변수에 주소값 할당 
  		p=new Person("아이유",100);
  		System.out.println(p);//주소값 확인 
  		System.out.println(p.getMoney());//참조변수로 객체를 제어 
  		p.setMoney(200);
  		System.out.println(p.getMoney());
  		System.out.println(p.getName());
  		Person p2=new Person("장기하",200);
  		System.out.println(p2);
  		//p2 객체의 주소값을 p 참조변수에 할당, 동일한 객체를 참조  
  		p=p2;
  		System.out.println("**예상해보기**");
  		System.out.println(p.getName());
  		System.out.println(p2.getName());
  	}
  }
  ```
  
  
  
  출력방식
  
  ```java
  step3.Person@15db9742
  100
  200
  아이유
  step3.Person@6d06d69c
  **예상해보기**
  장기하
  장기하
  ```
  
  
  
  
  
  ## Java Memory
  
  - **Heap 영역**
    - 동적 메모리 영역, **객체 정보(속성 정보)를 저장하는 영역**
    - Heap 영역에 저장되는 객체의 메모리 정보는 **고유한 주소값이 생성**
  - **Stack 영역**
    - 지역 변수 local variable이 저장되는 영역
  
  



:play_or_pause_button: Switch

```java
package step7;

public class TestSwitch {
	// switch case 구문 ( 조건문 ) 
	public static void main(String[] args) {
		int grade=1;
		switch(grade) {
		case 1:
			System.out.println("제네시스");
			break;//실행문을 벗어난다 
		case 2:
			System.out.println("그랜저");
			break;
		case 3:
			System.out.println("아반떼");
			break;
		case 4:
			System.out.println("모닝");
			break;
		default:
			System.out.println("따릉이");
		}
	}
}
```

- ``break`` 가 없으면 grade 의 값에서부터 순차적으로 프린트한다
