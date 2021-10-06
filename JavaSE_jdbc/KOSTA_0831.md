**19일차 주요목차**
- Thread 개념
- Thread 생성 방법 
- Thread 동작원리 : start() 와 run()
- Multi-Threading 
- synchronized ( 동기화 처리 ) 

-------------------------------------------------------------

- Thread : 프로세스 내부의 세부적 실행단위 
			 사전적 의미 - 실 ( 실이 여러개 모여서 옷을 만든다 ) 
			 
			 프로세스(process) - 현재 실행 중인 프로그램 
			 
			 하나의 프로세스는 여러 개의 스레드가 실행되면서 구성될 수 있다 
			 
			 ex) 동영상 플레이어가 현재 실행 중이다 ( 동영상 플레이어 프로세스 ) 
			      동영상 서비스를 위해서는 영상서비스(Thread) , 음향서비스(Thread) , 자막서비스(Thread)가
			      필요하다. 이러한 동영상 플레이어 프로세스 내의 세부적 실행단위를 스레드라고 한다 
			      이 스레드들이 동시에 실행되는 것을 멀티 스레딩이라고 한다 
	
- Thread 생성 방법 2가지  			       
    1) extends Thread    
    2) implements Runnable 
    
    
  - Thread 동작원리 : start() 와 run()
     start() : 스레드를 실행가능상태(Runnable)로 보낸다
     		    이후 JVM이 스케줄링을 해서 실행상태로 전이된다 
     		    
     run() : 스레드의 실행 내용을 정의한다 
     		 JVM이 스케줄링을 하면 실행되는 메서드 
     		 run() 메서드가 수행을 종료하면 스레드는 종료된다 		       
    
  - Thread 별로 Stack 메모리가 생성된다 ( 스레드 별로 지역 변수를 별도로 가지게 된다 ) 
  
  - Thread 는 우선 순위 방식을 채택 ( 가장 낮은 우선순위 1  , 기본 우선순위 5, 가장 높은 우선순위 10 ) 
    운영체제 별로 우선 순위가 적용되는 여부는 다르므로 참고로 한다   
    
  - Thread 의 setDaemon(true) : 해당 스레드를 실행시킨 스레드가 종료되면 해당 스레드도 종료되도록 처리   
    
  - 다수의 스레드가 자원(객체)을 공유해 사용할 수 있다 : 멀티 스레딩의 장점 
  	 스레드는 자신의 스레드 별로  stack 메모리 영역을 가지고 
  	 객체(공유 대상 자원)는 하나의 heap 영역에 저장되어 공유된다 
  	
  - 멀티 스레딩시 동기화 처리 ( synchronized ) -> 특정 영역을 단일 스레드 환경으로 만드는 것 
    동기화 ( synchronized ) 는 다수의 스레드가 공유 자원을 사용할 때 작업의 신뢰성을 위해 사용하고  
    공유 자원에 대해 특정 스레드가 작업 중에는 다른 스레드들이 참여 할 수 없도록 처리하는 것을 말한다 	 
    
    동기화 처리 방법 
    1. 메서드 단위에서 동기화 처리 :   public synchronzied void use(){} -> use 메서드는 단일 스레드 환경으로 실행 
    2. 특정 코드 블럭에만 동기화 처리 : synchronzied(this){ } -> 메서드 내의 특정 영역에만 동기화 처리  
    
    실세계의 예 
    ex1)  카페 
    	   여러 손님들(다수의 스레드)이 카페의 공연을 함께 관람하는 것은 문제가 없다 
           여러 손님들(다수의 스레드)이 하나의 화장실을 사용할 때는 순차적으로 사용해야 한다 -> 동기화 처리의 필요 
           
    ex2)  영화예매 
           영화 좌석 정보를 인터넷 예매 시스템과 현장 예매 시스템(멀티 스레드)이 공유할 때에는 
           예매 현황을 조회할 때는 문제가 없다 
           예매 작업 시점에는 단일 스레드 환경으로 순차적으로 예매 처리를 하도록 해야 한다 	-> 동기화 처리의 필요 
    
    -> 특정 A열 1번 좌석을 예매처리하는 영역에서는 단일 스레드 환경으로 처리할 필요
    
    ​	- 만약 동기화 처리가 되지 않아 다수의 슬드가 접근해서 특정 좌석을 예매한다면 동일한 좌석을 여러 고객이 예매하는 문제가 발생할 수 있음
    
    -----------
    
    
  
  - 동기화 처리(synchronized)
	  - thread-safe
	  - 다수의 스레드가 특정한 영역을 공유할 떄에는 동기화 처리의 필요성이 있다
	  - ``StringBuilder`` vs ``StringBuffer``
	    - 공통점
	      -  자체가 변경, 가변, 시스템 상에서 동일한 문자열이 자주 변경될 때 유리하다
	    - 차이점
	      - StringBuilder: 동기화처리:x:
	      - StringBuffer:  동기화처리 :o: (thread-safe)
	        - 불필요하게 동기화 처리 시 속도 저하 위험이 있음
	        - 멀티스레딩 시 안전하다
	        - String buffers are safe for use by multiple threads. The methods are synchronized where necessary so that all the operations on any particular instance behave as if they occur in some serial order that is consistent with the order of the method calls made by each of the individual threads involved.
	  - java Collection 계열
	    - ArrayList vs Vector
	    - HashMap vs Hashtable
	    - 동기화처리x  동기화처리(thread-safe)
	    - 최근에는 Vector와 HashTable은 잘 사용하지 않고 동기화 처리된Collection 계열이 필요한 경우에는
	    - java.util.Collection의 synchronized()와 synchronizedMap()을 이용해서 thread-safe 하게 한다

- ``--``
  - sql 한줄 주석
- ``/**/ ``
  - sql 여러줄 주석
- sql은 대소문자 구별하지 않는다
- sql: 데이터베이스를 제어하는 언어
  - 데이터베이스를 정의, 조작, 제어하는 언어

SQL은 다음과 같은 범주로 구분될 수 있다

1. DDL
   - Data Definition Language
   - 데이터 정의어
   - ``CREATE, DROP, ALTER``
2. DML
   - Data Manipulatio Language
   - 데이터 조작어
   - ``SELECT, INSERT, DELETE,UPDATE``
   - CRUD
     - Create,Read,Update,Delete
3. DCL
   - Data Control Language
   - 데이터 제어어
   - COMMIT, ROLLBACK(작업을 취소하고 원상태로 되돌린다),GRANT,REVOKE(권한취소)



TABLE

- 데이터 저장 공간

COLUMN

- 속성(attribute)

CONSTRAINT

- 제약조건