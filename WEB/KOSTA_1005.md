- 최상위 인터페이스 이름이 서블릿
- 서블릿 인터페이스에서 라이프사이클 관련 세 가지 메서드가 있ㅇ므
  - init(),service(),destroy()
- 이 모든 것은 웹 컨테이너가 호출한다
  - servlet lifecycle 을 담당하는 당사자는 web container이다



## Model 2 Architecture MVC Design Pattern

- Model 2 설계방식의 근간을 이루는 디자인 패턴이 MVC
- 통상적으로 Model2 or MVC or Web MVS or Model2 MVC 라고 부른다

![image-20211006142111072](C:\Users\MIN\TIL\WEB\KOSTA_1005.assets\image-20211006142111072.png)



## Model2 MVC or Web MVC

> web application 설계방식 ( or Architecture or 구조) 으로서 Model, View, Controller 영역으로 분리해서 설계 구현하는 것

- Model: Java Beans( or Java Component ) - DAO , Service , VO , DTO 등
  - **비즈니스 로직과 데이터 액세스 로직**을 정의
- View: JSP 담당
  - 클라이언트에게 **동적인 웹페이지**를 제공
- Controller: Servlet 담당
  - 웹 어플리케이션의 **제어자** 역할
  - 클라이언트의 요청을 분석
  - 모델과 연동
  - 적절한 이동방식으로 View를 선택해 **클라이언트에게 응답하게 함**





## Controller(Servlet)에서 View(JSP)로 이동하는 방식

> 포워드 방식: request와 response가 유지되면서 이동되는 방식으로, 재요청시 기존 동작 반복

- request 와 response가 **유지되면서 이동**되는 방식
- **WAS(Web Container) 상에서 이동**되고 클라이언트 측은 이동여부를 **모름**
- 필요 시 Model과의 연동 결과를 request 객체 정보를 할당 `request.setAttribute(name,value)` 해서 View에서 정보를 이용 `request.getAttribute(name)` 해서 클라이언트에게 응답하게 한다

> redirect 방식: 기존 request와 response 가 유지되지 않음. 재요청시 **기존 동작을 반복하지 않음**

- 이동 시 client 에게 `url` 을 전달해서 **client가 다시 이동**하게 하는 방식
- 기존 request 와 response가 유지되지 않음
- client가 지정한 url로 다시 이동하므로 **새로운 request와 response 생성**됨





컨트롤러 로직

1. 클라이언트가 전달한 아이디를 받아옴
2. Model(MemberDAO)과 연동해서 결과를 반환받음
3. 받환받은 MemberVO가 null이면 findMemberById-fail.jsp로 이동시킴(forward)
4. 반환받는 MemberVO가 null이 아니면 request에 MemberVO를 할당하고 findMemberById-ok.jsp로 이동시킴

