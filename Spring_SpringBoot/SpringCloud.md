## REST(REpresentational State Transfer)  🔐

>  분산 환경에서 시스템 간의 통신을 위한 소프트웨어 아키텍쳐 

- 분산 환경에서 다양한 시스템 간의 통신을 위해 **자원에 식별자 부여**하고 자원정보를 **표준화된 HTTP Method로 제어**하는 소프트웨어 아키텍쳐  
- 식별자(URI)가 부여된 자원정보를 **표준화된 HTTP 메서드로 제어**한다
  - GET : 데이터를 **읽거나(\**Read)\**** **검색(\**Retrieve\**)**할 때에 사용되는 메소드
  - POST : 새로운 리소스를 **생성(create)**할 때 사용
  - PUT : 서버의 데이터를 **갱신, 작성**
  - DELETE : 서버의 데이터를 **삭제**

### 특징  :file_folder:

1. 웹에 존재하는 모든 자원에 **고유한 URI(통합자원식별자:Uniform Resource Identifier)를 부여해 활용** 
HTTP GET(조회) , POST(생성) , PUT(수정), DELELTE(삭제) Method를 통해 제어
2. "다양한 클라이언트"에게 서비스를 제공, 클라이언트와 **서버 역할의 명확한 분리가 가능.**  
  - 모바일 , 태블릿, PC , TV 등과 같은 다양한 디바이스 및 시스템에게 HTTP기반 서비스를 제공하기 위해 사용됨
  - 클라이언트는 REST API를 통해 서버와 정보를 주고 받는다 

- **REST API** : REST 기반 서비스 API (어플리케이션 간의 데이터 통신을 위한 어플리케이션 프로그래밍 인터페이스)

- **RESTful** : REST API 제공하는 웹서비스 시스템을 지칭 , "A 서비스 시스템은 'RESTful' 하다"

- Spring REST Annotation : `@RestController`
  - `@Controller`(컨트롤러 객체 생성을 위한 어노테이션) + `@ResponseBody`( 페이지 응답이 아닌 응답response 본문body 에 필요한 데이터(문자열 or json)로 응답하기 위한 어노테이션 ) 
    -  `@RequestBody` : json 을 http request body로 저장해 전송할 때 컨트롤러에서 자바 객체로 전달받기 위한 어노테이션 
    - **ResponseEntity class** : **응답 메세지와 상태코드** ( 200,404,500 .. )를 저장해 응답하고 싶을 때 사용하는 클래스 ( 컨트롤러 메서드의 반환형으로 쓰인다 ) 

- **Spring  RestTemplate class** :  REST API Server와 통신할 수 있도록 지원하는 클래스 ,  HTTP  GET, POST, DELETE, PUT 방식에 대한 메서드를 제공 
- 스프링에서 제공하는 여러 템플릿 클래스(ex- SqlSessionTemplate,JDBCTempleate)와 동일한 원칙으로 설계되어 **REST 서비스 연동작업을 용이**하게 함
  - 참고 )  REST API 개발 및 테스트 Tool -> POST MAN (https://www.postman.com/downloads/)

#  **MSA**  🥪

- ### MicroService Architecture란?   

  > 독립적으로 개발 , 배포할 수 있는 서비스의 모음으로 애플리케이션을 설계하는 방식 

  - 각각 자체 프로세스에서 실행 , 경량 메커니즘( REST/JSON  )으로 통신하는 **느슨한 결합의 서비스 모음**으로 단일 애플리케이션을 개발

###  장점  :smile:

- MSA 는 상호 독립적으로 구축될 수 있어 **결합도가 낮음** 
- **특정 서비스에만 집중**, 해당 서비스에 가장 적합한 환경과 기술을 선택할 수 있음 
- 변경 및 이슈 사항이 있는 **마이크로 서비스만 빠르게 수정,배포할 수 있음** 

- **Service Mesh** 
   - Mesh의 사전적 의미는 그물망 , 망사    
   - 비즈니스 로직과 분리된 **마이크로 서비스 간 커뮤니케이션 인프라 레이어** 
   - 마이크로 서비스 간의 **통신을 최적화**하기 위함 


####  주요기능 :bouquet:

- `Circuit Breaker` : 장애 전파 방지 
- `Service Discovery` : Client or API Gateway가 서비스를 검색하여  서비스의 위치( IP , Port )를 제공 
- `Configuration Management` :  설정 변경시 마이크로 서비스가 재빌드와 부팅 없이 즉시 반영
- `Load Balancer` : 서비스간 부하 분산 
- `API Gateway`  : API 엔드포인트 단일화 및 라우팅 기능 담당   

# Spring Cloud :cloud:

 - Spring Boot + Netflix OSS => Spring Cloud (Spring boot를 기반으로 MSA 구축에 특화된 라이브러리들의 집합)
     MSA 를 위한 스프링 프로젝트 
 - 독립적인 프로젝트들로 구성된 상위 프로젝트 ( Spring Cloud is an umbrella project consisting of independent projects ) 
 - MSA의 Service Mesh 를 위한 **Netflix OOS 기반 기술을 제공** 

###  Spring Cloud 의 주요 기술  :cloud_with_lightning:

1. `Hystrix(Circuit Breaker)` 
   - 특정 마이크로 서비스 장애 발생시 **확산 차단**
   - fallback(사전적 의미: 대비책)을 이용해 **장애에 유연하게 대처**
   - 각 마이크로 서비스의 오류, 복구 상태를 파악해 통신  
      								
2. `Ribbon(Load Balancer)` : 과부하 방지를 위해 **여러 자원에 작업을 분산** 
3. `Zuul(API Gateway)` : API 엔드포인트 단일화 및 라우팅 기능 담당
   - 클라이언트 요청에 대해 적절한 서비스를 연결하고 응답하는 단일한 진입점(front)의 역할
   - 데이터 통계 분석, 모니터링 
4. `Eureka(Service Discovery)` : Client or API Gateway가 **서비스를 검색**하여  서비스의 위치( IP , Port )를 제공. 서비스 **인스턴스 상태를 동적으로 관리** 
5. `Auto Scale-out` (특정 서비스 부하 증가 , 감소시 인스턴스 생성,삭제를 통해 시스템 자원 활용 최적화) 지원
6. S`pring Cloud Config Server`(Configuration Management) :  설정 변경시 마이크로 서비스가 재빌드와 부팅 없이 **즉시 반영**
