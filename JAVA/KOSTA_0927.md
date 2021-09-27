초기 파라미터는 ServletConfig에 할당되어지는 정보이다

context-param은 SerlvetContext에 할당되어지는 정보



각 지역에 맞는 자기 초기화 작업이 있을 것

-> 이 때 개별 설정 서블릿config로 가는데 전체 웹 어플리케이션에서 ㅏ용하는 것은 serlvet context가 됨

각 현지에 맞는 것은 init에서 받음

전체 회사의 초기화 작업은 어디서 하는가? 백업에 대한 작업은 어디서 하는가?

contextdestroyed: web application destroy 직전에 호출됨

웹 어플리케이션 시작 시점에 contextinitialized가 실행됨



web application 종료 직전에 호출





## ServletContextListener

- 웹 어플리케이션 **LifeCycle event 발생 시 실행되는 메서드**를 가진 Interface 
- 어플리케이션 차원에서 **시작시점에 필요한 초기화 작업**과 **종료시점에 필요한 백업, 로길 작업을 처리**하는 데 용이
  - `contextInitialized(event)`: 웹어플리케이션 시작 시점에 호출되어 실행되는 메서드
  - `contextDestroyed(event)` : 웹어플리케이션 종료 직전에 호출되어 실행되는 메서드



## ServletAnnotiation

- **서블릿 3.0 이상에서 지원**하는 기술

- WebServlet(url-pattern)이 어노테이션을 **서블릿 상단부에 명시**하면 기존 **`web.xml`의 url-pattern설정과 동일한 효과**를 가짐

- 어노테이션 `@`: **의미있는 주석**, 컴파일 및 런타인 시점에 시스템에 영향을 주기 위한 의미있는 주석

- 설정 정보(meta data)

  1. **XML: 소스코드와 설정의 분리**

  2. **Annotation: 소스코드 상에 설정정보를 기술**

  - 일반적으로 전역적인 설정은 `xml`에 기술, 설계 시 확정되는 부분은 어노테이션으로 설정

- 서비스 메소드에서 get방식이면 doGet을 호출해주는 형태(doGet은 서비스 메소드)
- 컨테이너가 호출해 줄 때 http를 상속받은 객체가 getPost를 
- web container가 service 메서드를 호출
- 상속받은 HttpServlet의 service 메소드가 클라이언트의 요청 방식에 따라 doGet() or doPost()를 실행





```html
  <servlet>
    <description></description>
    <display-name>LifeCycleServlet</display-name>
    <servlet-name>LifeCycleServlet</servlet-name>
    <servlet-class>step1.LifeCycleServlet</servlet-class>
    <load-on-startup>1</load-on-startup>
  </servlet>
```

- `web.xml`의 `load-on-startup`은 WAS **실행 시점에 해당 서블릿 객체 생성 및 init 실행해서 초기화** 작업을 해두기 위한 코드
- 명시 이유: 최초 해당 서블릿을 서비스 받기 위해 접속하는 **클라이언트에게 신속하게 서비스** 하기 위해서

- 서비스 처음 실행 시 is loaded? 물어보고 시작
- 두 번째 클라이언트부터는 바로 서비스 로드 됨
- 첫 번째 클라이언트는 객체 생성하고 이닛이 되니까 어쩔 수없이 초기화 작업을 할 동안 기다려야 하나?
  - 기본 작동 원리는 그렇지만 `load-on-startup`을 어노테이션 등에 사용하여  처음 웹 어플리케이션 시작 시점에 초기화 시킬 수 있도록 만들 수 있다



- 어노테이션이 무엇이냐고 질문이 오면 **컴파일 시 영향을 주는 의미있는 주석**이라고 대답하자!

- 웹어플리케이션 실행시점에 미리 해당 서블릿을 초기화하도록 `web.xml`에서 `load-on-startup` 설정을 어노테이션 방식으로 설정해본다

  ```java
  @WebServlet(urlPatterns="/LifeSycleServlet",loadOnStartup=1)
  public class LifeSycleServlet extends HttpServlet {
  ```

- listener은 서블릿 컨텍스트의 라이프사이클

- 서블릿컨텍스트가 만들어지고 나서 바로 첫 시점에 웹 어플리케이션 시점에 초기화 자원

- 어플리케이션 서비스 실행 직전 백업 작업에 작업을 정리하기 위해서는 