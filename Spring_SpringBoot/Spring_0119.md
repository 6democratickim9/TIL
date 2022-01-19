# **Template Engine : Thymeleaf** :leaves:

> SpringBoot 에서 지원하는 템플릿 엔진 

- Thymeleaf : 유지보수성이 높은 템플릿 생성 방법을 제공
- HTML의 구조상에서 개발하여 기존 HTML 코드를 변경하지 않고  개발하는 방식(Natural Templates)
  - 디자인 팀과 개발 팀 간의 협업이 보다 용이해짐

- Thymeleaf 와 함께 Spring에서 사용하는 템플릿 엔진 : jsp(jstl) , freemaker , mustache , groovy ,velocity 등이 있다     
      

#  Spring Handler Interceptor 

> DispatcherServlet이 해당 컨트롤러를 호출하기 전,후에 요청과 응답을 제어하는 역할  할 수 있음 

- Handler Interceptor를 이용하면 요청한 클라이언트의 **로그인 여부에 따른 인증 , 인가**를 처리

# **ORM, JPA, Hibernate**

- **ORM**
  - Object  -  ORM -  RDBMS 
  - 객체와 데이터베이스의 연결 역할  
  - 객체가 **테이블이 되도록 매핑** 시켜주는 것
- **영속성 계층 프레임워크(Persistence Layer Framework)** : MyBatis는 SQL Mapper Framework ,  JPA(Hibernate)는 ORM Framework 이다 

## JPA (Java Persistence API) 

>  자바 진영 ORM 기술 표준 명세 -> 자바 어플리케이션에서 DB를 연동하는 방식을 정의한 인터페이스(명세)

- 과거 EJB 3.0에서 기존 EntityBean 을 대체한 ORM 기술 표준으로 등장
- Hibernate : JPA의 대표적인 ORM 구현체 ( Library ) 
- JPA(Interface) , Hibernate(Implementation) 
- **ORM 은 객체 지향과 관계형 데이터베이스 기반 위에 있으므로 두 영역에 대한 이해가 있어야 한다**										  				   					   

 - ### ORM Framework( JPA , Hibernate ) 장점

   - 객체 지향적인 개발이 가능하여 비즈니스 로직에 집중할 수 있게 함
      - 즉, SQL 이 아닌 **객체의 메서드로 데이터를 제어**함 
      - 각 DBMS에 대한 종속성이 낮아진다
      - JPQL ( Java Persistence Query Language ) / QueryDSL :
          복잡도가 있는 섬세한 쿼리 작성을 위해 JPA의 객체지향 쿼리언어 학습이 필요      
         JPQL : 객체지향 SQL , JPQL을 사용하면 JPA가 적절한 SQL을 만들어 데이터베이스를 제어 
         QueryDSL : JPQL을 효율적으로 작성할 수 있도록 지원하는 빌더 API


#  **Java lambda**    		    			   

- 람다(lambda) : 익명 함수(Anonymous functions)를 지칭하는 용어		   
- 람다 표현식(lambda expression) : **메소드를 하나의 식으로 표현**한 것. 
  - 람다식을 사용하면 함수를 단순하게 표현할 수 있음
  - (매개변수목록) -> { 함수몸체 } 
-  **why?**
   - 개발 생산성 - 간결한 표현이 가능 
   - 파라미터에 행위를 전달할 수 있다 
     - 메서드 매개변수로 행동방식을 전달할 수 있다 
       - 런타임(실행시점)에 행위를 전달 받아서 제어 흐름을 수행할 수 있다.
     - 메서드의 추상화가 가능하다 
       - 알고리즘 자체의 변경을 동적으로 함수 형태로 할당 받아 적용할 수 있다. 
   - jdk 1.8 이상 지원

# **MSA**  

> 독립적으로 개발 , 배포할 수 있는 **서비스의 모음**으로 애플리케이션을 설계하는 방식 
> 각각 자체 프로세스에서 실행 , 경량 메커니즘( REST/JSON  )으로 통신하는 느슨한 결합의 서비스 모음으로 단일 애플리케이션을 개발

### 장점 

- MSA 는 **상호 독립적으로 구축될 수 있어 결합도가 낮음** 
- 특정 서비스에만 집중, 해당 서비스에 가장 적합한 환경과 기술을 선택할 수 있음 
- 변경 및 이슈 사항이 있는 마이크로 서비스만 빠르게 수정,배포할 수 있음 
- **비즈니스 요구에 신속 대응**
- 사용자 요청 증감에 따른 서비스 자원 자동 조정하여 비용 절감 및 만족도 향상		    

## MSA / Netflix OSS / Spring Cloud **

- **MSA** : MicroService Architecture , **서비스 단위로 분리해 개발**하고 운영, 각각 자체의 서버(프로세스)에서 배포 실행
  - 이들의 모음으로 **단일 애플리케이션을 설계**하는 방식 
- **Netflix OSS** :  MSA 구축을 위한 **Netfilx 사의 Open Source Software**
  - Hystrix(Circuit Breaker) , Ribbon(Load Balancer), Zuul(API Gateway), Eureka(Service Discovery) 등이 있음                    
- **Spring Cloud** :  Spring Boot + Netflix OSS ( Spring boot를 기반으로 MSA 구축에 특화된 라이브러리들의 집합 ) 
  - **MSA 를 위한 스프링 프로젝트**
  - 독립적인 프로젝트들로 구성된 상위 프로젝트 ( Spring Cloud is an umbrella project consisting of independent projects ) 

# **yaml/yml/야믈** 

>  데이터 직렬화 언어 

- `.xml` 및` json`과 같이 주로 환경설정 역할 
- springboot에서 설정파일로 `.properties` 와 함께 `yaml` or  `.yml `이 사용됨
-  xml 과 json 에 비해 **직관적**  
- 주석은 # , tab은 사용하지 않고 들여쓰기(space bar) 2칸 지원
- 데이터 정의 `key:value` 
- 배열 - 으로 정의