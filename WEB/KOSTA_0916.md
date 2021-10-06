# Servlet



## 1. HTTP

- HyperText Transfer Protocol

## 2. WAS

- Web Application Server
- Web Server+Web container
- Web Server -> HTTP에 의거해 HTML을 서비스하는 서버
- Web Container -> Servlet/JSP 실행환경을 제공

우리는 WAS 제품 중 아파치톤캣 사용

## 4. Web 환경설정

WAS 설치

1. Port 설정
   - apache-

2. 한글처리
3. 자동reload

## 5. Servlet

- Java Web Programming 기술
- java class 로 표현
- Model2 Architecture(MVC) 에서 Controller 의 역할을 함
  - Spring Framework의 웹기술 SpringMVC의 FrontController인 DIspatcherServlet도 서블릿임

## 6. JSP

- Java Server Page
- 동적인 웹페이지 생성을 위한 기술
- HTML 구조 상에서 JSP tag(java code)를 삽입 -> View를 구현하는 측면에서 장점
- MVC에서 View 의 역할을 함

JSP is a Servlet

- JSP는 Web Container에 의해 java class로 생성되어 컴파일, 실행됨
- 이 자바 클래스는 Servlet Interface의 하위, HttpServlet class의 자식