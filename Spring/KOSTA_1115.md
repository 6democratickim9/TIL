# **Spring Framework** :white_flower:

### 주요목차

- Spring IOC/DI 
- Spring AOP
- MyBatis Framework  
- SpringMVC ( Spring Legacy project ) 
- Ajax / JQuery / JSON / REST 
- SpringBoot 
- Thymeleaf 
- SpringSecurity 
- Spring Cloud ( MSA ) , RestTemplate, JPA 

-----------------------------------------

## 개념정리 



- **높은 응집도 (high cohesion), 낮은 결합도 ( loose coupling )** 

  > "모듈 간의 결합도는 최소화하고 모듈 내 요소들 간의 **응집도를 최대화**" 

  - 응집도 : 자신의 역할에 집중하는 정도
    - 모듈 내의 기능 수행을 위해 요소간에 얼마만큼 연관된 책 임이 집중되어 있는지를 나타내는 정도 
  - 결합도 : 모듈 간의 상호 의존 정도 

- 객체지향 ( Object-Oriented )

  - 시스템 분석 설계 기법 
  - 객체를 **독립적인 기본단위로 채택**하고, 객체와 객체의 **관계를 중심으로 분석,설계**하는 기법 

- `Class` : Object의 설계도 

- `Object` : 속성과 기능으로 구성, 시스템의 기본 단위 

- `package` : 클래스들을 분류 

- `library` : 라이브러리 , **재사용 가능한 프로그램들의 모음** ( jar : 자바 프로그램 압축 파일 확장자 ) 

- `component` : 프로그램이 실행될 때 하나의 독립적 기능단위를 이루어 부품화되는 것 ( bean : 자바 컴포넌트 )

- `API` : Application Programming Interface 

    - **응용프로그램을 개발하기 위해 제공하는 인터페이스** 

- `Framework` : 사전적 의미 -> 뼈대 , 틀 , 기반 (infrastructure)

- `Spring Framework` : java 어플리케이션의 설계 , 구현 , 테스트 , 운영(유지보수) 전반에 대한 
      기반 (infrastructure)을 제공

     - 다양한 컴포넌트(or 라이브러리)를 제공하고 디자인 패턴을 지원 
     - 프레임워크는 **반완전한 어플리케이션**이다 
     - 개발자는 비즈니스 로직에 집중하도록 하는 것이 목적

     - IOC/DI , AOP , MVC , Security , SpringBoot 등을 지원하고 MyBatis , JUnit 등과 같은 오픈 소스 프레임워크와의 통합을 지원한다 

- `IOC` : Inversion Of Control 

    -  제어의 반전(역행) , 역제어
    - 컴포넌트를 구성하는 **인스턴스 생성과 의존 관계 연결처리를 IOC 컨테이너에 위임** 

- `DI` : Dependency Injection 

   - 의존성 주입
   - 필요로 하는 **의존대상(컴포넌트 or 객체 or bean)을 injection(주입)을 통해 확보**한다 

- `DL` : Dependency Lookup 

   - 의존성 검색 
   - **필요로 하는 의존대상(컴포넌트 or 객체 or bean)을 lookup(검색)을 통해 확보**한다 	

- IOC , DI , DL 의 목적 -> Loose Coupling (느슨한 결합도 ) 	

- Spring IOC Container는 Singleton 방식으로 객체를 운용한다 
   참고)  Singleton Design Pattern : 시스템 상에서 단 하나의 **객체를 생성하고 공유해 사용**하기 위한 디자인 패턴 	 	  	














​	        
