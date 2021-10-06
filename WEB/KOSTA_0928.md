# Session & Cookie :cookie:

### 일반적인 HTTP 특성

- stateless(사용자 상태 정보를 유지하지 않는다)



#### 세션 관리

- 사용자 정보를 일정 시간동안 유지



## 쿠키 :cookie:

- 사용자 **상태 정보를 클라이언트 측에 저장**
- **저장 용량의 제한(4kb)**
- 데이터 타입은 **문자열**로 한정
- 쿠키 유효 시간을 별도로 설정하지 않으면 **브라우저 실행시에만 유효**
- 쿠키 유효 시간을 설정하면 그 **유효 시간 내에서만 쿠키를 사용**할 수 있음



1. 서버측에서 쿠키를 생성해 클라이언트에게 전달하여 클라이언트 측에 쿠키가 저장됨

   ![image-20210928114712775](C:\Users\MIN\TIL\JAVA\KOSTA_0928.assets\image-20210928114712775.png)

2. 클라이언트가 접속하면 서버측에서 클라이언트의 쿠키를 확인해서 특정 쿠키(name=time)인 value를 얻어와 화면 출력

   ![image-20210928140627066](C:\Users\MIN\TIL\JAVA\KOSTA_0928.assets\image-20210928140627066.png)





## HTTP Session :lock_with_ink_pen:

- 사용자 상태 정보를 **서버 측에 저장**
- 저장 용량 및 데이터 타입의 **제한은 없음**
- **로그인, 로그아웃** 시에 세션이 이용됨
- WAS에 세션 **유지 시간이 별도로 설정**되어 있음

### Http Session 관련 주요 메서드

- HttpServletRequest 의 `getSession()` method: 기존 세션이 존재하면 기존 세션을 반환, 없으면 새로 생성해서 반황(reqeust.getSession(true)와 동일)
- HttpServletRequest의 getSession(false) method: 기존 세션이 존재하면 기존 세션을 반환, 없으면 null반환

- HttpSession의 setAttribute(name,value): 세션에 String 타입의 name과 Object타입의 값을 할당해서 저장
- HttpSession의 getAttribute(name): 세션에 저장된 속성 정보를 name으로 검색해서 값을 반환

- HttpSession의 invalidate(): 세션을 무효화시킨다(로그아웃 시 사용)

edge 브라우저와 크롬은 각각 다른 클라이언트로 인식한다(같은 기기에서 접속하더라도!)

#### 세션의 타임아웃 시간을 조절하고싶다면?

- `C:\apache-tomcat\WAS\web-tomcat\conf\web.xml` 에 있는 해당 부분에서 숫자를 설정해주자!

![image-20210928142944543](C:\Users\MIN\TIL\JAVA\KOSTA_0928.assets\image-20210928142944543.png)



#### 세션 유지기간

ex) 로그인 유지기간

1. 지정한 유효시간(tomcat 30min)
2. 브라우저 종료
3. 로그아웃 실행

-----

#### 로그인 과정에서 세션처리 흐름

![image-20210928155832365](C:\Users\MIN\TIL\JAVA\KOSTA_0928.assets\image-20210928155832365.png)

#### 로그인 후 다시 접속했을 때 세션처리 흐름

![image-20210928160314330](C:\Users\MIN\TIL\JAVA\KOSTA_0928.assets\image-20210928160314330.png)





`GetSession`

- false를 주면 null을 return
- 현재 세션이 없거나 create가  true면 새로운 세션을 만들어준다

`HttpSession`

- `getAttributeName()`
  - 

`HttpServletRequest`

- `getCookies`
  - return cookies' array
    - `class Cookie`
      - `getName()`
        - returns name of the cookie
- 쿠키의 정보를 확인. 쿠키의 정보는 여러 개 넣을 수 있음



```java
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		response.setContentType("text/html;charset=utf-8");
		PrintWriter out = response.getWriter();
		out.println("<!DOCTYPE html>");
		out.println("<html>");
		out.println("<head>");
		out.println("<meta charset=\"UTF-8\">");
		out.println("<title>home</title>");
		out.println("</head>");
		out.println("<body>");
		String name = getServletName();
		out.println("<h3>"+name+"</h3>");
		out.println("</body>");
		out.println("</html>");
        out.close();
```



---------------

# JSP

> Java Server Page

- 동적인 웹페이지를 위한 기술

- 서블릿과는 다르게 HTML 상에서 자바코드(or jsp tag)를 삽입하는 형태로 개발

- JSP는 WAS(Web Container)에 의해 java로 생성되고 컴파일되어 실행된다

- 생성된 java class 는 HttpServlet의 자식 클래스

  - **JSP is a Servlet**

- 생성된 자바 파일은 MVC에서 Model 은 java beans, View는 JSP, Controller는 Servlet이 담당

  

  ## JSP 기본 문법

  1. 주석

     ```jsp
     <%--JSP 주석이에용--%>
     ```

     - 참고: html주석 : `<!--html 주석이에용 -->`







`C:\KOSTA224\WAS\web-tomcat\work\Catalina\localhost\webstudy11-jsp-basic\org\apache\jsp`

에 들어가면 jsp가 java가 되는 과정을 볼 수 있음
