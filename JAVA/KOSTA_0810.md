## Meta Space 영역

> class 의 **메타 데이터가 저장되는 영역**

```java
package step1;

public class TestStatic2 {
	String name="아이유";
	
	static String name2= "박보검";
	public void test1() {
		System.out.println("object member method test1"+name);
	}
	
	public static void test2() {	
		new TestStatic2().test1();
	}
	public void test3() {
		test2();	
	}
	
	public static void main(String[] args) {
	
		TestStatic2 t = new TestStatic2();
		System.out.println(t.name);
		t.test1();
		System.out.println(name2);
	}

}

```

- ``String name="아이유";``

  - instance variable

- ``static String name2= "박보검";``

  - static variable: static 멤버 사용은 신중하게 해야 함

    :point_right:  class loading 시점에 한 번 메모리에 적재 후 계속 유지됨

- ``System.out.println("object member method test1"+name);``
  - object member method

- ``new TestStatic2().test1();``

  - ``test1();``

    :arrow_right: compile error

    ``static``->`` non static`` 으로 바로 접근 불가

  - ``new TestStatic2().test1();``

    - 얘처럼 객체 생성해야 함

- ``test2();``

  - object의 member method ``test3()``은 실행을 위해서는 **객체 생성을 전제**로 함

    :point_right:**``static member``에 바로 접근 가능**

  - ``test3()``이 실행된다는 것은 class loading 

    :point_right: **객체 생성을 전제**로 함

  - static은 미리 class loading 시점에 적재됨 

    :point_right: ``non static``에서 ``static``으로 바로 접근 가능

- ``System.out.println(name);``
  - **compile error**
    - ``name``은 instance variable이므로 **객체 생성시에만 메모리에 적재**
  - static에서 non-static으로 바로 접근 불가
  - 같은 클래스 내에서라도 **객체를 생성해서 접근해야 함**
- ``System.out.println(name2);``
  - static member 이므로 **바로 접근 불가능**

## 

# static 

> class 의 member ( variable , method )

- 객체 생성없이 클래스 로딩만으로 메모리에 적재 ( meta space 영역에 저장 )

- ``클래스명.member``

  - ``클래스명.static변수``  or ``클래스명.static메서드``

- ## Java Memory

  - **Heap 영역** : 객체의 instance variable 이 저장되는 영역
  - **Stack 영역** : local variable이 저장되는 영역 
  - **Meta Space 영역** : ``class`` 의 meta data 가 저장되는 영역 , ``static member``가 저장 

- ## Java Program 실행단계

  1. compile 된 class 실행 

  2. Class Loader가 Class Loading 

     :point_right: meta space 에 class meta data 정보를 메모리에 적재( static )

  3. class 검증단계

  4. 실행단계

     - ``main`` 실행

     - 필요시 동적으로 객체 생성 

       :point_right: **heap 영역에 객체 정보 저장 , stack 영역에 지역변수 저장** 

- static 접근 관련 

  ```j
  non-static			static 
    			----->	
    		직접 접근 가능 
    			<-----
  직접 접근 불가 , 반드시 객체 생성을 필요로 한다
  ```

  

```java
package step1;

class Fish{
	int count;
	static int sCount;
	Fish(){
		count++;
		sCount++;
	}
}
public class TestStatic3 {
	public static void main(String[] args) {
		Fish f1=new Fish();
		System.out.println(f1.count);//1
		System.out.println(Fish.sCount);//1
		Fish f2=new Fish();
		System.out.println(f2.count);//1
		System.out.println(Fish.sCount);//2
		Fish f3=new Fish();
		System.out.println(f3.count);//1  이유는 객체 생성시 heap영역에 별도로 객체 생성되어 count는 매번 새롭게 0->1 로 메모리에 저장 
		System.out.println(Fish.sCount);//3 이유는 class loading시에 단 한번 meta space 영역에 static sCount의 메모리가 적재되고 값이 업데이트됨
	}
}

```

```java
1
1//sCount
1
2//sCount
1
3//sCount
```



## final  :triangular_flag_on_post:

- ### ``final`` 상수

  - 한 번 할당되면 **재할당 불가**

  - 상수명은 대문자로 구성되고 합성어는 underscore **``_``로 연결**

  - 다른건 카멜케이스

    ex) ``private final String ADMIN_ID = "java";``

- ### ``final`` 메서드

  - 자식 클래스에서 **오버라이딩 불가**

- ### ``final`` 클래스

  - subclassing 불가
    - **상속 불가**

  

## abstract

> 추상 클래스 또는 추상 메서드 선언 시 사용하는 자바 키워드

1. ### abstract class

   - 부모 클래스의 역할에 집중
   - 자신은 ``new``로 직접 객체화 될 순 없지만 자식 클래스를 통해 멤버를 물려준다

   - 추상 클래스는 **직접 객체화 될 수 없다**

   ```java
   public abstract class Animal{}
   Animal a = new Animal();
   ```

   ``Animal a = new Animal();``

   :point_right: **compile error**

   -  abstract class 는 ``new`` 클래스명()-> **객체 생성 불가**
   - 단, 상속을 통한 **자식 객체에서 ``super()``를 이용해 생성은 가능**

2. ### abstract method

   - **구현부가 존재하지 않음**
   - 부모 차원에서 구현할 수 없는 기능이지만 **반드시 자식 클래스에게 구현을 강제해야 할 때** 적용
   - 부모 클래스에 abstract 메서드가 존재하면
   - 자식 클래스는 abstract method를 구현하거나 자신이 abstract class로 선언되어야 함
   - 직접 객체화 X
   - 하나 이상의 abstract method가 클래스 내에 존재하면 해당 클래스는 abstract class가 되어야 함	



**Template Method Design Pattern **

- Design Pattern
  - 소프트웨어 설계 패턴
  - 소프트웨어 설계단게에서 공통적으로 발생하는 문제에 대한 해결방안
- Template Method
  - 상위(부모)클래스 차원에서 작업공정 or 알고리즘 구조를 정의해 재사용하게 하고 특정 부분은 하위(자식) 클래스에서 구현 또는 재정의해서 사용하도록 하는 패턴
  - 상위 클래스에서 알고리즘의 구조를 정의해 재사용하게 하는 패턴



