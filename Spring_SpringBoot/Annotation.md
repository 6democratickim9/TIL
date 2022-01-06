# @Annotation 

### 의미있는 주석

- Annotation 은 컴파일과 런타임시에 **영향을 주는 의미있는 주석**
- 자바 소스 코드 상에 기술하는 **메타데이터** 

### 메타데이터 

- 데이터의 데이터 , **데이터들을 설명하기 위한 데이터** 
  - ex) 택배 상자 위에 붙는 택배 운송장( 택배상품들에 대한 정보 

 -  #### Spring Annotation

     -  설정 정보의 역할 
          - `@Component` 계열 어노테이션
            - 컴포넌트 계열 어노테이션이 적용된 클래스는 스프링 컨테이너에 의해 bean으로 생성됨 
            - `@Repository` : 영속성 계층에서 사용 
              - Data Access Logic 을 정의한 객체에 적용
            - `@Service` : 비즈니스 계층에서 사용  
              - Service or Business Logic 을 정의한 객체에 적용
            - `@Controller` : 프리젠테이션 계층의 컨트롤러에서 사용 
              - MVC 의 Controller Logic을 정의한 객체에 적용
	       - `@RestController`  // REST 서비스를 위한 컨트롤러 어노테이션  `@Controller + @ResponseBody`	
     
     - **RestController 에서 사용하는 어노테이션** 
       - `@GetMapping` : 조회  
       - `@PostMapping` : 생성 
       - `@PutMapping` :수정 
       - `@DeleteMapping` : 삭제 
     
     - `@Bean` : bean 생성을 위한 어노테이션 : 외부라이브러리를 통해 bean 생성하고자 할 때 사용하는 어노테이션 
       - 리턴하는 객체가 bean으로 등록된다 
       - `@Component` : 개발자가 작성한 클래스를 bean으로 등록할 때 사용 

- **DI(Dependency Injection) 계열 어노테이션**
  - 스프링 컨테이너로부터 의존성 주입(필요로 하는 bean을 주입) 받고자 할 때 명시 
- `@Autowired` 
  - 의존대상bean을 타입으로 검색해 주입 ( 생성자, 필드 , setter )
    - 동일한 인터페이스를 여러개의 클래스가 구현하는 상태에서는 `@Autowired + @Qualified("bean id")` 어노테이션을 추가적으로 명시한다 
- `@Resource`
  - 의존대상bean을 타입으로 검색해 주입 (필드와 setter ) 
    - 동일한 인터페이스를 여러개의 클래스가 구현하는 상태에서는 `@Resource(name="bean id") name` 속성을 추가적으로 명시한다

- 자바 클래스 기반 환경설정을 위한 어노테이션 
  - `@Configuration` // Java Class 기반의 **Spring 환경설정 클래스**임을 스프링 컨테이너에 알리는 어노테이션