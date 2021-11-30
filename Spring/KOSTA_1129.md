`load-on-startup`

- 톰캣 컨테이너가 실행되면서 미리 서블렛 실행
- 지정한 숫자가 0보다 크면 톰켓컨테이너가 실행되면서 서블릿이 초기화 됨
- 지정한 숫자는 우선순위를 의미하며 작은숫자부터 초기화 됨
- Servlet LifeCycle에서 위 설정이 없으면 클라이언트의 첫번째 요청시에 DispatcherServlet의 객체생성 - init - service가 이루어지므로 웹어플리케이션 시작시점에 DispatcherServlet이 초기화되도록 설정한 것



.do 스타일로 요청되면 DispatcherServlet이 처리하도록 url-pattern을 설정



- DispatcherServlet
  - SpringMVC에서 제공하는 FrontControllerServlet
  - 모든 클라이언트의 요청을 하나의 진입점으로 통합해서 처리
    - FrontController Design Pattern
  - FrontController인 DispatcherServlet은 자신의 설정파일(spring configuration)을 서블릿 이름-servlet.xml로 찾아서 로드함



아래 구성요소들은 개발자가 구현해야 하는 요소들이다

- Controller: 개발자가 컨트롤러 로직을 정의 (주요 설정: @Controller, @RequestMapping, @ResponseBody 등등)
- View: 개발자가 응답할 웹페이지 또는 데이터를 정의