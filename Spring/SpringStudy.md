- `application.properties`

- ```properties
  spring.mvc.view.prefix=/WEB-INF/views/ 
  spring.mvc.view.suffix=.jsp
  ```

  - 생성한 jsp 경로를 prefix로 선언, 확장자를 suffix로 선언

- ```properties
  spring.datasource.url=jdbc:oracle:thin:@127.0.0.1:1521:xe 
  spring.datasource.username=scott 
  spring.datasource.password=tiger 
  ```

  - db 세팅

- ```properties
  server.port=7777
  ```

  - 서버의 포트는 7777로 열어둠

- `org.kosta.myproject.controller.HomeController.java`

- ```java
  package org.kosta.myproject.controller;
  
  import org.springframework.stereotype.Controller;
  import org.springframework.web.bind.annotation.RequestMapping;
  
  @Controller
  public class HomeController {
  	@RequestMapping("/") 
  	public String home() {
  		return "index";
  	}
  }
  
  ```

  - `src/main/java/webapp/WEB-INF/views/index.jsp`로 위에 세팅해둔 경로를 통해 찾아서 매핑 후 보여줌

  - `src/main/java/webapp/WEB-INF/views/index.jsp`

  - ```jsp
    <%@ page language="java" contentType="text/html; charset=UTF-8"
        pageEncoding="UTF-8"%>
    <!DOCTYPE html>
    <html>
    <head>
    <meta charset="UTF-8">
    <title>spring ajax</title>
    </head>
    <body>
    SpringBoot Home
    <a href="getTotalDepartmentCount">부서수</a>
    <%--
    	DepartmentController -- DepartmentMapper
    	|
    	views/department/dept-count.jsp
     --%>
    </body>
    </html>
    ```

    - `a href="getTotalDepartmentCount"`를 누르면

    - `org.kosta.myproject.controller.DepartemtnController.java`에 있는

    - ```java
      package org.kosta.myproject.controller;
      
      import org.kosta.myproject.model.mapper.DepartmentMapper;
      import org.springframework.beans.factory.annotation.Autowired;
      import org.springframework.stereotype.Controller;
      import org.springframework.ui.Model;
      import org.springframework.web.bind.annotation.RequestMapping;
      
      @Controller
      public class DepartmentController {
      	private DepartmentMapper departmentMapper;
      
      	@Autowired
      	public DepartmentController(DepartmentMapper departmentMapper) {
      		super();
      		this.departmentMapper = departmentMapper;
      	}
      
      	@RequestMapping("getTotalDepartmentCount")
      	public String getTotalDepartmentCount(Model model) {
      		model.addAttribute("totalDepartmentCount", departmentMapper.getTotalDepartmentCount());
      		return "department/dept-count";
      	}
      
      }
      
      ```

      - ```java
        	@RequestMapping("getTotalDepartmentCount")
        	public String getTotalDepartmentCount(Model model) {
        		model.addAttribute("totalDepartmentCount", departmentMapper.getTotalDepartmentCount());
        		return "department/dept-count";
        	}
        ```

        - 여기로 알아서 들어감

        - `model.addAttribute("totalDepartmentCount", departmentMapper.getTotalDepartmentCount());`

        - 이 줄에서 ` departmentMapper`를 통헤

        - `org.kosta.myproject.model.mapper.DepartmentMapper.java`

        - ```java
          package org.kosta.myproject.model.mapper;
          
          import org.apache.ibatis.annotations.Mapper;
          
          @Mapper
          public interface DepartmentMapper {
          
          	int getTotalDepartmentCount();
          
          }
          ```

          - `@Mapper`: 

          - Interface를 매퍼로 등록하기 위해 @Mapper 어노테이션을 사용

          - Mapper 설정 파일(xml)에 있는 SQL 쿼리문을 호출하기 위한 인터페이스

          - Mybatis3.0 이후부터 지원하는 방식

            - `@Mapper`를 통해 `org.kosta.myproject.model.mapper.DepartMapper.xml`로 이동

            - ```xml
              <?xml version="1.0" encoding="UTF-8"?>
              <!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
              <mapper
              	namespace="org.kosta.myproject.model.mapper.DepartmentMapper">
              	<select id="getTotalDepartmentCount" resultType="int">
              		select count(*) from springboot_department
              	</select>
              </mapper>
              ```

              - `select count(*) from springboot_department` 해당 쿼리문 실행 후

              - ```java
                	@RequestMapping("getTotalDepartmentCount")
                	public String getTotalDepartmentCount(Model model) {
                		model.addAttribute("totalDepartmentCount", departmentMapper.getTotalDepartmentCount());
                		return "department/dept-count";
                	}
                ```

                - 여기로 돌아옴

                - `departmentMapper.getTotalDepartmentCount()`에서 받아온 값을 `totalDepartmentCount`로 매핑해줌

                - `return "department/dept-count"`를 통해

                - `src/main/java/webapp/WEB-INF/views/departemt/dept-count.jsp` 로 보냄

                - ```jsp
                  <%@ page language="java" contentType="text/html; charset=UTF-8"
                      pageEncoding="UTF-8"%>
                  <!DOCTYPE html>
                  <html>
                  <head>
                  <meta charset="UTF-8">
                  <title>Insert title here</title>
                  </head>
                  <body>
                  ${totalDepartmentCount}
                  </body>
                  </html>
                  ```

                  `${totalDepartmentCount}`그럼 여기서 받아온 값 출력

