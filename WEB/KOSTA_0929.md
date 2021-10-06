client(html form)과 server (servlet) 연동

`client`

```html
<form action="url pattern"  method="get">															
   	 <input type="text" name="food">																	   
   	 <input type="submit" value="주문">																   
   	 </form>	 
```

`Server`

```
url pattern에 해당하는 서블릿의 doGet 메서드가 실행 
클라이언트가 보낸 정보를 입력받기 위해 
request.getParameter(name) 즉 request.getParameter("food") 과 같이 입력받는다
```

- ubmit 을 누르면 아래와 같은 형식으로 전송된다 	 
  - http://localhost:8888/webstudy06-servlet-basic/url-pattern?name=value&name=value





## JSP

> Java Server Page: 동적인 웹페이지를 위한 기술

- 서블릿과는 다르게 HTML 상에서 자바코드( or jsp tag ) 를 삽입하는 형태로 개발 
- JSP는 WAS(Web Container)에 의해 java 로 생성되고 컴파일되어 실행된다
- 생성된 java class는 HttpServlet의 자식 클래스이다. 
  - JSP is a Servlet 
- 생성된 자바 파일은 tomcat/work 디렉토리에 저장된다



- Model2 Architecture MVC 에서는 Model 은 java beans , View 는 JSP , Controller 는 Servlet 이 담당



### JSP 기본 문법

- jsp **주석** `<%--    --%>`  
  - 참고) html 주석 `<!--    -->` 
- scriptlet 스크립틀릿 `<%  java code %>`  **service 메서드 내에 자바 코드**로 삽입 
- expression `<%=  %>`  `out.print()` 의 역할 , **화면 출력**용 
- declaration **선언**  `<%!   %>`  멤버 변수 , **메서드 정의**시 사용 
5) directive **지시자**   `<%@   %>`  jsp **문서 정보를 웹컨테이너에 전달**  , 한글처리방식 , 문서타입 , import , errorPage 등을 기술



JSP LifeCycle - Servlet과 동일 ( 차이점은  jsp 를 이용해  .java 를 생성하고 .class 로 컴파일해서 실행 : tomcat/work 디렉토리에 생성 ) 

![image-20210929214359476](C:\Users\MIN\TIL\JAVA\KOSTA_0929.assets\image-20210929214359476.png)

### Query String:

> 사용자가 입력 데이터를 전달하는 방법 중 하나

- url 주소에 **미리 협의된 데이터**를 **파라미터**를 통해 넘기는 것

- ```jsp
  <%@ page language="java" contentType="text/html; charset=UTF-8"
      pageEncoding="UTF-8"%>
  <!DOCTYPE html>
  <html>
  <head>
  <meta charset="UTF-8">
  <title>query string</title>
  </head>
  <body>
  <a href="step2-2-querystring-action.jsp?no=2&food=갈비">step2 action test1</a>
  </body>
  </html>
  ```

  

- ```jsp
  <%@ page language="java" contentType="text/html; charset=UTF-8"
      pageEncoding="UTF-8"%>
  <!DOCTYPE html>
  <html>
  <head>
  <meta charset="UTF-8">
  <title>step2-2-querystring-action.jsp</title>
  </head>
  <body>
  client가 보낸 no : <%=request.getParameter("no") %><br>
  client가 보낸 food : <%=request.getParameter("food") %>
  </body>
  </html>
  ```

  - ```
    client가 보낸 no : 2
    client가 보낸 food : 갈비
    ```

    



