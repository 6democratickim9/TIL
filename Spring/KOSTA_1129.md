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



- ### MyBatis Framework

  - Java Persistence Framework
  - 영속성 계층 프레임워크
  - 자바 어플리케이션과 데이터베이스 연동시 반복적인 작업을 프레임워크 차원에서 지원하여 생산성이 향상
    - Connection, PreparedStatement, ResultSet, close

- ### SpringMVC

  - Spring Framework 기반 java web application 구현을 위한 기술

  - MVC+FrontController Design Pattern

  - #### MVC 

    - Model: Data Access Logic + Business Logic
    - View: 클라이언트에게 응답하는 정보 (web page or data(text or json))
    - Controller: 클라이언트의 요청과 응답에 대한 제어자의 역할
      - 요청분석, 모델과 연동, 적절한 VIew 로 응답, 주기술: Servlet

  - #### Front Controller Pattern

    - 모든 클라이언트의 요청을 하나의 진입점으로 통합하여 처리하는 디자인 패턴
    - 공통 정책을 일관성있게 수행할 수 있음
      - 인증 및 인가, 인코딩, 예외처리 등



## SpringMVC 주요 구성요소

- **DispatcherServlet**

  - Front Controller Servlet
  - spring configuration을 로딩

- **HandlerMapping**

  - 요청을 처리할 컨트롤러를 매핑
  - 어노테이션 기반 RequestMappingHandlerMaping을 사용

- **HandlerAdapter**

  - HandlerMapping에서 결정된 컨트롤러를 실제로 실행시키는 역할
  - 컨트롤러 메서드에서 필요한 매개변수 인자값을 생성해서 제공
  - 어노테이션 기반 RequestMapping HandlerAdapter를 사용

- **ModelAndView**

  - 컨트롤러가 수행한 후 DispatcherServlet에게 반환하는 정보

  - Model과 연동한 정보와         View 정보를 할당해서 반환한다

    (request setAttribute)             (view name)

- **ViewResolver**

  - 컨트롤러가 반환한 ModelAndView의 view name을 바탕으로 클라이언트에게 응답할 적절한 view 방식을 제공
  - `InternationalResourceViewResolver:`` prefix `:point_right: `/WEB-INF/views` ,` suffix` :point_right: `.jsp`



아래 구성요소들은 개발자가 구현해야 하는 요소들이다

- Controller: 개발자가 컨트롤러 로직을 정의 (주요 설정: @Controller, @RequestMapping, @ResponseBody 등등)
- View: 개발자가 응답할 웹페이지 또는 데이터를 정의
