AOP 
Aspect Oriented Programming  관점 지향 프로그래밍 
시스템을 핵심관심사(Core Concern)와 횡단관심사or 공통관심사(Cross-Cutting Concern)로 
구분해 설계 구현 테스트 운영하는 것을 말한다 

핵심관심사(Core Concern) : 시스템의 업무 목적에 해당하는 주요 로직 ( ex - 결제 등록 게시 ) 
횡단관심사(Cross Cutting Concern) : 시스템의 여러 부분에 걸쳐 적용되는 공통적인 로직 (ex - 트랜잭션, 로깅, 보안 ) 

why? AOP는 시스템의 여러 영역에 걸쳐 공통적이고 반복적으로 적용된 횡단관심사 로직을 분리하여
	  별도의 모듈에서 설계 구현 운영하는 프로그래밍 기법이다. 
	  -> 반복적인 작업을 피할 수 있어서 효율적인 개발이 가능하고 
	  	  이후 유지보수시  AOP 부분만 변경하면 되므로 유지보수성이 향상된다 

AOP 용어 
Advice : 적용시점 + Cross Cutting Concern( 공통 기능 )
		   어느 시점에 Cross Cutting Concern을 Core Concern 에 적용할 것인가를 정의 
		   ( advice 종류 : before, after , after-returning , after-throwing , around ) 
Weaving : Advice를 Core에 적용하는 것   	  
Pointcut : Advice 적용 대상을 지정 , AspectJ 기술을 이용 ( execution , within , bean ) 

- Proxy Design Pattern : AOP 에 적용된 주요 디자인 패턴 
  Proxy 대리인 , 대신해서 역할을 수행 
  사용하는 측과 서비스 제공하는 측의 인터페이스 역할을 Proxy가 한다 ( 팬 - 아이유매니저 - 아이유 ) 
  																							 Proxy 
  Core 객체를 사용하고자 할 때 , 사용하는 측에서 실제 Core 객체를 참조하는 것이 아니라 
  대리인 역할을 하는 Proxy 객체를 통해 Core 객체를 사용하게 함으로써 
  Proxy 객체가 Cross Cutting Concern을 수행하게 한다 
  
  - AOP 동작원리 
  Spring IOC Container는 AOP 적용시 실제 Target Core 객체가 아니라 Proxy 객체를 사용하는 측으로 반환해 
  Core 실행시 Cross-cutting Concern 이 실행되도록 하는 구조다 
  Proxy는 Core 가 implements 하는 인터페이스를 동일하게 implements 한다 
  만약 Core가 인터페이스를 implements 하지 않을 때는 Proxy가 Core 를 extends 하여 
  사용하는 측에서 서비스를 호출할 때 Proxy가 아닌 Core를 실행하는 것과 같게 한다 
  

-log4j: 프로그램 작성시 로그를 남기기 위해 사용되는 자바 기반 로깅 유틸리티(or 라이브러리)
설정 파일에서 팩키지별로 레벨 지정이 가능, 지정한 등급 이상의 로그만 저장하는 방식이다.

FATAL(가장 높은 로그레벨)
ERROR
WARN
INFO
DEBUG
TRACE(가장 낮은 로그레벨)