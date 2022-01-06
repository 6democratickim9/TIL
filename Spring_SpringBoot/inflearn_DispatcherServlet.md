# Spring Boot 작동원리

- `application.properties`
  - `설정이름=값`
- `application.yml`
  - `설정이름.값`
  - 데이터 중심으로 된 파일 작성용으로 사용됨



```yml
logging:
  level:
    org.springframework: DEBUG
```

- 로깅 레벨 디버깅모드로 적용
- ![image-20211129232909683](DispatcherServlet.assets\image-20211129232909683.png)
- 사용자 요청에 따른 비즈니스 로직 처리 후 결과값을 api를 호출한 쪽으로 다시 전달
  - 사용자 요청을 처리해주는 일종의 gate이다
  - 이런 DispatcherServlet을 관리해주는 configuration이 자동으로 실행됨
- `HttpMessageConveterAutoConfiguration`:  결과값 반환 위해 사용되고 있음
  - json 포맷으로 변환 후 클라이언트에게 반환해줌
- 이 외에도 bean 정보에 많은 것들이 로딩됨



## DispatcherServlet

- 클라이언트의 모든 요청을 한 곳으로 받아서 처리
- 요청에 맞는 Handler로 요청 전달
- Handler의 실행 결과를 Http Response 형태로 만들어서 반환
- Presentation 계층의 맨 앞에 위치함
- 사용자의 요청은 DispatcherServlet에서 시작되고 DispatcherServlet에서 끝난다



![image-20211203170237926](inflearn_DispatcherServlet.assets/image-20211203170237926.png)

1. Request가 디스패쳐 서블릿으로 전달됨
2. 디스패처 서블릿에서는 핸들러메ㅊ핑이나 컨트롤러로 전달
3. 처리된 결과값을 spring mvc에서는 Model형태로 반환
4. 사용자에게 보여주고자 하는 페이지 포맷에 따라 viewResolver가 페이지 생성
5. 페이지 값에 view를 포함시켜 반환



- spring mvc에서는 컨트롤러 생성을 위해 일반적인 컨트롤러 클래스를 spring 설정파일에 등록해서 사용했었음
- spring4부터는 어노테이션 등록 후 사용
- view를 가진 서비스가 아니라 json으로 결과값 전달만 하는 프로젝트..!





----------

## Java Bean이란?

- JavaBean은 JavaBean API Specification에 따른 Standard

1. **모든 필드는 private**이며, getter/setter메서드를 통해서만 접근이 가능하다.
2. **Argument가 없는(no-argument) 생성자가 존재**한다.
3. `java.io.Serializable` **인터페이스를 구현**한다.

이 세 가지 규칙을 지키는 클래스

### 왜  java.io.Serializable을 구현하는가?

- 메모리에 존재하는 오브젝트를 네트워크를 통해 전송하거나 파일에 저장하려면 **data stream(e.g, byte[])으로 이 오브젝트를 변환**시켜줘야 함

  :point_right: 이 변환 작업을 `Serialization`이라고 부른다

- 