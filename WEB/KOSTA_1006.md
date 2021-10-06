## Singleton Design Pattern

- 시스템 상에서 단 한 번 객체를 생성해서 공유하여 여러 곳에서 사용하고자 할 때 적용하는 설계 패턴
  - 스프링 프레임워크에서는 기본 객체 운용방식이 singleton 방식

### 적용 방안

1. private 생성자
   - constructor(생성자)에 private access modifier를 명시해 외부에서 객체 생성하는 것을 막음
2. private static 멤버변수로 자신의 객체를 생성
   - private static 멤버 변수차원에서 클래스 로딩 시점에 자신의 생성자를 이용해 단 한 번 객체를 생성하고 meta space 영역에 주소값을 저장
3. public static 메서드로 외부에 공유
   - public static 메서드로 외부에서 사용하는 측에 한 번 생성하여 meta space, 즉 static 변숭 저장된 객체의 주소값을 반환하여 사용하게 함

### jsp에서 세션 사용

- jsp는 기본적으로 session을 사용할 수 있다
- web container에 의해 jsp 가 java로 생성될 때 session 변수에 getSession()메서드를 이용해 세션 객체를 할당하는 코드가 생성되어 있음
  - getSession()메서드는 기존 세션이 존재하면 기존 세션을 반환하고 기존 세션이 존재하지 않으면 새로 생성해서 할당
  - 회원 인증시(로그인)에는 세션에 인증정보(주로 회원객체)를 할당
  - 이후 회원 인증 여부(로그인 체크) 를 확인할 때는
  - 해서 세션 유무와 함께 인증정보가 존재하는지를 확인해야 함

