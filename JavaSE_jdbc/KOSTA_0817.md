**School Project List Version**

**리팩터링**(refactoring)은 소프트웨어 공학에서 '결과의 변경 없이 코드의 구조를 재조정함'을 뜻한다. 주로 가독성을 높이고 유지보수를 편하게 한다. 버그를 없애거나 새로운 기능을 추가하는 행위는 아니다.

SchoolProject List Version을  refatoring 해본다

Test class와 실행 결과는 기존과 동일

business logic을 정의한 School Service 가 리팩토링 대상





- 요구사항 
학교 구성원 정보를 관리하는 시스템을 구축하고자 한다 
학교 구성원은 학생, 교사 , 직원으로 구성된다 

학생은 전화번호, 이름, 주소, 학번으로 구성된다
교사는 전화번호, 이름, 주소, 과목으로 구성된다 
직원은 전화번호, 이름, 주소, 부서로 구성된다 

주요 기능 
1. 구성원 정보를 등록 
학교 구성원 정보(학생,교사,직원)를 등록할 수 있다 
등록시 기존 구성원 전화번호와 동일한 번호가 있을 경우 등록시키지 않는다  
( 중복시 메세지 : 01012341234 tel이 중복되므로 등록 불가합니다 ) 

2. 전체 구성원 리스트 출력 ( 상세정보가 모두 출력 ) 

3. 전화번호를 이용한 구성원 정보 검색 
    전화번호를 전달하면 그에 해당하는 구성원 정보를 반환 
    만약 전화번호에 해당하는 구성원 정보가 없다면 null을 반환 
    
4. 전화번호를 이용한 구성원 정보 삭제 
	전화번호를 전달하면 구성원 정보를 삭제한다 
	만약 전화번호에 해당하는 구성원 정보가 없어서 삭제할 수 없다면 아래와 같이 메세지를 제공한다 
	( 01012341234 tel에 해당하는 구성원 정보가 없어서 삭제 불가 ) 
	
-----------------------------------------
요구분석에 대한 설계 
1) 요구사항에 대한 토의 
2) 설계 - Class Diagram ( StarUML tool 이용 ) 
		   --> 주요 클래스명과 인스턴스 변수명 , 핵심 기능(메서드)을 표현 ( 예상가능한 것은 생략가능 - setter,getter,constructor) 

총 구현시간 (개인소요시간  ) 

------------

**14일차 주요목차**

- java.util.Map
- java.util.Stack, java.util.Queue
- Exception 기본 개념
- Exception 주요 키워드
  - try,catch

java Collection 계열의 주요 요소

- Set: 중복 인정x
- List: index로 관리
  - ArrayList: index로 관리, 검색에 유리
  - LinkedList: index로 관리, 추가, 삭제에 유리
- Map: key와 value 쌍으로 저장하고 key로 제어
  - 검색, 삭제, 수정 작업을 key 이용
  - key는 유일값
    - 만약 동일한 키로 저장될 경우 value가 업데이트 됨
  - TreeMap: key value 쌍으로 저장, key로 제어, 정렬 기능
  - LinkedHashMap: key value 쌍으로 저장, key로 제어, 입력 순서를 기억
- Stack
  - LIFO
  - 나중에 입력된 요소가 먼저 추출됨
- Queue
  - FIFO
  - 선입선출
- Iterator
  - Collection 계열의 모든 자료구조체들을 단일한 방식으로 반복, 열거할 수 있는 방법을 제공하는 인터페이스



Exception의 기본 개념

- java.lang.Throwable class의 sub class(자식 클래스)
  1. Exception
  2. Error
- Exception Handling(예외 처리)
  - 프로그램 실행 시 예외 상황 발생할 때 대안흐름을 실행하고 프로그램을 정상 수행하는 것이 예외처리의 목적이다
  - JVM은 실행 시 Exception 상황이 발생하면 Exception 객체를 생성해 실행창에 출력하고 프로그램 실행을 중단함



case 1

```java
package step6;

public class TestException1 {
	public static void main(String[] args) {
		String name = "아이유";
		name = null;
		System.out.println(name.length());
		System.out.println("프로그램정상수행");
	}

}
```

```java
Exception in thread "main" java.lang.NullPointerException
	at step6.TestException1.main(TestException1.java:7)
```

- 해당 메세지를 출력하고 프로그램은 비정상 종료됨





case 2

```java
package step6;

public class TestException2 {
	public static void main(String[] args) {
		String name = "아이유";
		name = null;
		try {
			System.out.println(name.length());
		}catch(NullPointerException ne) {
			System.out.println("프로그램정상수행");
		}
		
	}

}
```

- TestException1 상황에서 Exception Handling(예외처리) 하는 예제
- try와 catch 라는 자바 키워드를 통해 특정 예외 상황이 발생되면 대안흐름을 실행하고 프로그램은 정상 수행되도록 예외 처리

- case1 과 case2의 차이는 case2에서 try catch를 이용해 Exception Handling 해서 예외 상황 발생 시 프로그램이 비정상 종료되지 않고 대안흐름 실행한 후 프로그램은 정상 수행 되는데 있음
- Exception 관련 주요 자바 키워드
  - try,catch,finally,throw,throws
  - try
    - Exception 발생 예상 지점 영역 지정 시 사용
  - catch
    - Exception 발생 시 대안 흐름을 정의해서 실행

case3

```java
package step6;

import java.util.ArrayList;

public class TestException2 {
	public static void main(String[] args) {
		String name = "아이유";
//		name = null;
		ArrayList<String> list = new ArrayList<String>();
		try {
			System.out.println(name.length());
			System.out.println(list.get(0));
		}catch(NullPointerException ne) {
			System.out.println("정보가 없으므로 길이를 구할 수 없습니다");
			
		}catch(IndexOutOfBoundsException ie ) {
			System.out.println("리스트 요소가 존재하지 않아 반환할 수 없습니다");
		}catch(Exception e) {
			e.printStackTrace();
		}
		System.out.println("프로그램정상수행");
	}

}
```

- 하나의 try 블럭 내에 여러개의 Exception이 발생할 수 있다
- 하나의 try 블럭에 대한 여러 개의catch 구문이 정의될 수 있음
- Exception catch 대상이 상속관계에 있으면 구체적 예외(자식 예외 클래스)에서 추상적 예외(부모 예외 클래스) 순으로 정의해서 예외를 처리할 수 있음