# 디자인 패턴 :necktie:

> 자주 사용하는 **설계 형태를 정형화**해서 이를 **유형별로 설계 템플릿**을 만들어둔 것

- 효율성과 재사용성을 높일 수 있음
- 구조적인 문제를 해결할 수 있는 방안을 제시해줌

1. ## 생성 패턴(Creational Pattern)

   - ### singleton

     > 단 하나의 인스턴스를 생성해 사용하는 디자인 패턴

     - 하나의 인스턴스를 사용하기 때문에 메모리 효율적 사용 가능
     - 전역 인스턴스를 다른 클래스의 인스턴스들이 데이터를 공유
     - 싱글톤 인스턴스가 **너무 많은 일을 하거나 데이터를 공유**시킬 경우 수정과 테스트가 어려워짐
     - **공통된 객체**를 여러 개 생성해서 사용해야 하는 상황에 사용
     - **전역에서 사용될 하나의 객체**를 만들어야 하는 상황

3. ## 행위 패턴

   - ### Template Design Method

     > 특정 작업을 처리하는 일부분을 서브 클래스로 캡슐화하여 전체적인 구조는 바꾸지 않으면서 특정 단계에서 수행하는 내용을 바꾸는 패턴

     - 구현별로 달라질 수 있는 메소드들은 구현 클래스에서 선언 후 호출하는 방식으로 사용
     - 상위 클래스에서 틀을 정의하고, 하위 클래스에서 구체화하는 패턴
     - 유지보수 용이
     - 코드 중복 감소
     - 자식 클래스의 역할을 감소시키면서 핵심로직 관리 용이
     - 객체 추가 및 확장 쉽게 가능



web container

front controller

mvc

proxy





## Redirect

- Web Container로 명령이 들어오면, 웹 브라우저에게 다른 페이지로 이동하라고 명령을 내림

  :point_right: URL을 지시된 주소로 바꾸고 해당 주소로 이동

- 다른 웹 컨테이넝 있는 주소로 이동하며 새로운 페이지에서는 Request객체와 Response객체가 새롭게 생성됨

- 최초의 Request와 Response객체는 유효하지 않고 새롭게 생성됨

- 시스템에 변화가 생기는 요청의 경우에 사용

## Forward

- Forward는 Web Container 차원에서 페이지의 이동만 존재
- 웹 브라우저에는 최초에 호출한 URL이 표시되고, 이동한 페이지의 URL 정보는 확인할 수 없음
- 현재 실행중인 페이지와 forward에 의해 호출될 페이지는 Request 객체와 Response객체를 공유
- 시스템에 변화가 생기지 않는 단슨 조회 요청의 경우에 사용



getinstance

.instance



HandlerMapping

https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=todoskr&logNo=220845006916



사내 인트라넷: ServletContext

사원증: ServletConfig