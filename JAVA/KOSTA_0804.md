주석 처리 단축기

:ctrl+shift+/

데이터타입:클래스



Array

> 다수의 데이터를 효과적으로 관리하기 위해 사용ㅇ

1. primitive data type의 데이터를 저장하는 배열

   - 배열 선언 ``int[] age; `` or ``int age[];``

   - 배열 생성 ``age=new int[3];`` 

     - 3개의 공간이 있는 배열 객체 생성

   - 배열 요소를 할당 ``age[0]=22;`` ``age[1]=24; age[2]=18;``

     - 배열 인덱스는 0부터 시작

     ``age.length;``: 배열의 사이즈 반환

자동완성: ctrl+space

```java
package step5;

public class TestArray4 {
	public static void main(String[] args) {
		String food[]= {"고기국수","참이슬","테라"};
		for(int i=0; i<food.length;i++)
			System.out.println(food[i]);
	}

}
```

- 실행문이 한 줄이면 중괄호 생략가능



2. reference data type 의 데이터를 저장하는 배열

   - 배열 선언: ``Person[] pa; `` or ``Person pa[];``

   - 배열 생성: ``pa=new Person[3];``

   - 배열 요소 할당: ``pa[0]=new Person("아이유",28);``

     