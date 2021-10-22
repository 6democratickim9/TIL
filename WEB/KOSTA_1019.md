.do의 의미?

https://okky.kr/article/262795

관습이군아

- jsp에서 사용하는 가상의 주소

  1) test.jsp 페이지에서 test.do가 링크 되어있는 요소를 클릭하면

  2) 이동하는 페이지는 웹서버에서 test.do가 있는 java파일을 확인하고,

  3) test.do를 사용하는 어노테이션을 가진 메소드로 이동해서 처리한다.

  4) 이후 메소드 안에서 지정해놓은 jsp파일로 이동한다.

- MVC+Front Controller Design Pattern 상에서 Datebase의 date 형을 이용

- SQL함수: to_char()와 to_date() 함수를 학습하고 적용

- 링크 부여시에 컨트롤러 url과 query string을 이용해서 상품 상세 컴트롤러로 동작되도록 명시

## DBCP

> Database Connection Pool

- **시스템 성능 향상이 목적**
- 커넥션을 생성하고 소멸하는 방식이 아니라 미리 커넥션들을 생성해놓고 필요시 빌려주고 반납받는 형식으로 커넥션 운영

- `javax.sql.DataSource Interface`
  - 다양한 dbcp 구현체들이 implements 하는 인터페이스
  - dbcp 구현체를 사용하는 어플리케이션 측에서 단일한 방식으로 다양한 dbcp 구현체를 실행할 수 있게 한다
  - 결합도를 느슨하게 해 dbcp 구현체가 변경되어도 영향은 최소화된다

