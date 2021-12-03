SpringBoot

- 간단한 프로젝트
- 스프링 부트 프로젝트를 사용할 때는 어떤 설정파일이 사용되고 로딩되는지 확인해보자
- springboot 에서 설정파일을 확인해보기 위해서는 자바 클래스를 사용해 볼 수도 있지만
  - `resources/application.properites` 이나 `application.yml`을 통해 확인 가능

- 자바에서는 일반적으로 설정값 지정에 있어서 text.properties 를 채용해왔다
- 이런 `properties` 항목에 설정을 넣기 위해 이름과 값 두 사이에 `=`를구분자로 사용
- yml은 xml이나 json파일 포맷처럼 `설정이름:값` 사용



- `application.yml`

```yml
server:
  port: 8888
  
logging:
  level:
    org.springframework: DEBUG
```



- ```
     DispatcherServletAutoConfiguration matched:
        - @ConditionalOnClass found required class 'org.springframework.web.servlet.DispatcherServlet' (OnClassCondition)
        - found 'session' scope (OnWebApplicationCondition)
  ```

  - 사용자 요청에 따른 비즈니스 로직 처리 후 결과값을 api를 호출한 쪽으로 다시 보내준다
  - DispatcherServlet은 사용자 요청을 처리하는 일종의 gateway라고 생각하면 좋음

- ```
  HttpMessageConvertersAutoConfiguration matched:
        - @ConditionalOnClass found required class 'org.springframework.http.converter.HttpMessageConverter' (OnClassCondition)
        - NoneNestedConditions 0 matched 1 did not; NestedCondition on HttpMessageConvertersAutoConfiguration.NotReactiveWebApplicationCondition.ReactiveWebApplication did not find reactive web application classes (HttpMessageConvertersAutoConfiguration.NotReactiveWebApplicationCondition)
  ```

  - 결과값을 반환해주기 위해 사용하는 autoconfiguration file은 `HttpMessageConvertersAutoConfiguration `를 사용