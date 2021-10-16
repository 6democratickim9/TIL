**12일차 주요목차**

- abstract / interface review

- java.util.Collection 
	1) java.util.Set 
    2) java.util.List

-------

## abstract 와 interface

## 1. 공통점 :family_woman_girl:

- 계층구조 형성을 통한 **다형성 적용**
- ``abstract method``를 통해 **하위 클래스에게 구현을 강제**
- 직접 객체 생성 불가(new를 통함)

## 2.  차이점 :family_woman_boy:

> ``abstract`` 는 **단일 계층구조**, ``interface``는 **다양한 계층 구조 형성**이 가능

- ``abstract``는 ``Object`` 의`` member(instance variable, 구현된 method)``를 상속시킬 수 있음
- ``interface``는 오직`` static final ``상수와 ``abstract method``만 가질 수 있음
  - (참고 - jdk 1.8 이상에서는 ``default``, ``static`` 메서드 추가)

## java.util.Collection

- ``java.util.collection interface``는 ``Collection`` 계층 구조의 **최상위 인터페이스**
- 모든 java 자료구조 객체 (ArrayList,TreeSet, HashMap class) 는 최상위 인터페이스인 ``Collection``에서 명시한`` abstract method``를 **모두 구현하고 있다는 것을 보장**

- ``Collection API`` or  ``Framework`` 는 다양한 데이터들을 효과적으로 제어하고 관리하기 위한 **인터페이스 및 클래스의 모음**
  - Library
    - **재사용 가능한 프로그램들의 모음**

### Collection 계열의 대표적인 인터페이스

- Set, List, Map

## Generic

- **미리 타입을 지정**해서 **데이터 안정성**을 보장

- 객체 캐스팅 **절차를 감소**시킬 수 있음

- ```java
  LinkedHashSet<String> set=new LinkedHashSet<String>();
  ArrayList<FriendDTO> list=new ArrayList<FriendDTO>();
  ```
  

1. ### ``java.util.Set Interface``

   - **중복 허용 x**
     - 동일한 데이터를 중복해서 저장하지 않음
   - ``LinkedHashSet class``
     - 중복 허용 x, **추가 순서** 보장
   - ``TreeSet class``
     - 중복 허용 x, **정렬 기능** 내장
   
2. ### ``java.util.List``

   - **인덱스로 관리**

   - ``ArrayList``: 인덱스로 관리, **검색**에 용이

   - ``LinkedList``: 인덱스로 관리, **추가, 삭제**에 용이
