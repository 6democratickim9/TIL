컨트롤러 영역의 요소

- FrontControllerServlet
  - 모든 클라이언트의 요청을 통합하는 진입점의 역할을 하는 서블릿
- HandlerMapping
  - 개별 컨트롤러 구현체들의 생성을 전담하는 객체
- Controller Interface
  - 컨트롤러 구현체들의 상위 인터페이스, 캡슐화, 표준화
- 개별 Controller 구현체





----

singleton이란?

- 인스턴스가 오직 1개만 생성되어야 하는 경우에 사용되는 패턴