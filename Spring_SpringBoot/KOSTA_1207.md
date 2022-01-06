## `@SpringBootApplication`

- 스프링 부트 프로젝트의 기본적인 설정 선언
- 내부적으로 `@ComponentScan` 역할
  -  IOC, DI, DL
- 컴포넌트 계열 어노테이션을 bean으로 생성, DI 관련 어노테이션은 DI 처리

- `@EnableAutoConfiguration`

  - 사전에 정의된(Maven pom.xml) 라이브러리들을 bean으로 등록 

    ​	:point_right: 자동설정(springmvc, mybatis, aop, transaction등에 대한 자동 설정 담당)

  - base package 는 현 패키지가 되므로 현 패키지 또는 현 패키지의 하위에서 application을 정의하고 어노테이션을 정의해야 반영됨

`org.kosta.myproject`

- 이게 루트가 된다



- `org.kosta.myproject.controller`

- ```java
  @Controller
  public class HomeController{
  @RequestMapping("/")
  public String home(){
  	return "index";
  }
  }
  ```

- `src/main/webapp/WEB-INF/views`

  - `index.jsp` 생성