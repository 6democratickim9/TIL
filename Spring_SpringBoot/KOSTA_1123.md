- 스프링 설정 방식 
   `xml , annotation , java config , properties , yaml `
   
 - ## Annotation 
   
   - 의미있는 주석
     -  Annotation 은 컴파일과 런타임시에 영향을 주는 의미있는 주석이다 
   - 자바 소스 코드 상에 기술하는 메타데이터 
     - 메타데이터 -> 데이터의 데이터 , 데이터들을 설명하기 위한 데이터 ex) 택배 상자 위에 붙는 택배 운송장( 택배상품들에 대한 정보 ) 
   
 -  Spring Annotation : 설정 정보의 역할 

     `@Component` 계열 어노테이션 -> 컴포넌트 계열 어노테이션이 적용된 클래스는 스프링 컨
     `@Repository `: 영속성 계층에서 사용 ( Data Access Logic 을 정의한 객체에 적용 ) 
     `@Service` : 비즈니스 계층에서 사용 ( Service or Business Logic 을 정의한 객체에 적용 ) 
     `@Controller` : 프리젠테이션 계층의 컨트롤러에서 사용 ( MVC 의 Controller Logic을 정의한 객체에 적용)

## DI(Dependency Injection) 계열 어노테이션

> 스프링 컨테이너로부터 의존성 주입(필요로 하는 bean을 주입)받고자 할 때 명시

- `@Autowired` 
  - 의존대상 bean을 타입으로 검색해 주입(생성자, 필드, setter) -> 동일한 인터페이스를 여러 개의 클래스가 구현하는 상태에서는 `@Autowired+ @Qualified("bean id")` 어노테이션을 추가적으로 명시한다

- `@Resource`
  - 의존대상 bean을 타입으로 검색해 주입 (필드와 setter) -> 동일한 인터페이스를 여러개의 클래스가 구현하는 상태에서는 `@Resource(name="bean id")` name 속성을 추가적으로 명시한다

- spring-config.xml에서 IOC, DI, DL 에 대한 설정

  - `<context:component-scan base-package="org.kosta">`

    :point_right:`org.kosta` 패키지 및 하위 팩키지의 컴포넌트 계열 어노테이션이 명시된 클래스를 탐색해서 bean 생성해 저장하고 DI 계열 어노테이션 명시된 대상에 대해 의존성 주입을 한다 