Web Architecture



<img src="C:\Users\MIN\TIL\JAVA\KOSTA_0924.assets\슬라이드2.PNG" alt="슬라이드2" style="zoom:50%;" />

![image-20210924104604971](C:\Users\MIN\TIL\JAVA\KOSTA_0924.assets\image-20210924104604971.png)

우리가 만드는 서블릿은 다 http로 상속받게 되어있음

<<interface>>

- `Servlet`: 서블릿 인터페이스는 모든 서블릿(jsp 포함) implements 해야 하는 메서드를 정의한 인터페이스로 모든 서블릿과 jsp의 최상위 인터페이스

<<abstract>>

- `GenericServlet`: Servlet interface 를 implements하는 abstract class로, 프로토콜에 독립적인 abstract class임

  - 일반적으로 서블릿이 가져야 하는 메서드를 구현해 자식 클래스에게 물려주고 자식 차원에서 구현해야 하는 abstract method(service 메서드)를 정의하고 있음

- `HttpServlet`: GenericServlet을 상속받는 클래스

  - Http Protocol에 특화된 서비스를 구현하는 데 유용한 기능을 제공한다
  - 일반적으로 web application개발시에는 이 클래스를 상속받아 개발함

- Servlet Interface (Servlet, Servlet Request, Servlet Response, HttpSession, etc)들을 중심으로 Servlet API, 즉 인터페이스를 보고 개발하고 실제 동작은 개별 WAS 제품군에서 구현한 클래스가 동작하는 방식으로 WAS가 변경되더라도 특정한 프로그램의 수정없이 배포되어 실행될 수 있다는 장점이 있음

  :point_right: Web application과 개별 WAS 제품군과의 결합도를 낮춰 유지보수성을 향상시킬 수 있다는 의미



## Servlet LifeCycle

- Servlet/JSP 계층구조의 최상위 인터페이스 Servlet의 LifeCycle abstract method
- init(), service(), destroy()



- 서블릿의 라이프 사이클을 관리하는 주체는 WAS이다

  - `web.xml`(Deployment Descriptor:웹어플리케이션 설정정보)를 로딩하고 서블릿 객체를 생성하고 

    ``init()``,``service() ``->``doGet() ``or ``doPost()``, ``destroy()``를 실행하는 주체는 Web Container(Servlet Container)이다

  - ``init()``: 해당 서블릿의 **초기화 작업**, 서블릿 당 **한 번 실행**
  - `sevice()`: 해당 서블릿이 **클라이언트에게 서비스하기 위해 실행** ( 내부적으로` doGet()` or `doPost()`로 연결 )
    - 클라이언트 요청시마다 매번 실행
  - `destroy()`: 해당 서블릿이 **서비스 종료되기 직전에 호출**(WAS를 중지할 때 실행)

  ![슬라이드1](C:\Users\MIN\TIL\JAVA\KOSTA_0924.assets\슬라이드1-16324842861452.PNG)

  ex) LifeCycleServlet 에 클라이언트가 10명이 접곧해서 서비스를 받았다

  - LifeCycleServlet 객체는 몇 개 생성? 1개
  - init() 몇 번 실행? 1번
  - service() 몇 번 실행?10번
  - destroy() 몇 번 실행? 서비스 종료 직전 1번 실행

## ServletConfig 

- 개별 서블릿의 **설정 정보를 저장하는 객체** 

- **서블릿 당 하나 생성** 

- Web Container(Servlet Container) 에 의해 init 호출시점에 ServletConfig 객체가 주입된다 

- 초기 파라미터 ( init-param ) , ServletContext 객체 주소값 등이 ServletConfig에 저장되어 전달된다

  ex) 사원(서블릿) 당 사원증(ServletConfig) 

## ServletContext

- 웹어플리케이션 내의 **모든 서블릿과 jsp가 공유하는 자원** ( 필요시 정보를 set/get 할 수 있다 )

- 웹어플리케이션 당 하나 생성

- 웹어플리케이션 시작 시점에 생성되고 **종료 직전에 소멸됨**

  ex) 회사 사내 인트라넷



https://ehdvudee.tistory.com/8
