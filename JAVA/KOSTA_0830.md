**Network**

Java 기반의 TCP/IP 네트워크 프로그래밍 

주요 클래스 : java.net.*   Socket , ServerSocket 

Protocol : 프로토콜 , 약속 , 통신규약 

TCP/IP : 인터넷 통신 규약 

TCP : Transmission Control Protocol 전송 제어 프로토콜 
		신뢰성이 높다 -> 데이터 전달을 보증 
IP : Internet Protocol  ,  ip address -> 127.0.0.1 ( localhost) : 자신의 컴퓨터의 IP 	
    
      DNS( Domain Name System ) : 사용자들이 ip를 기억하기에 불편함이 있으므로 주로 Domain Name을 이용한다( www.google.com , www.naver.com .. ) 

Port : 가상의 연결단위 , 서버의 서비스 번호(입구) 
		ex)  http://127.0.0.1:8888
			 http : protocol 
			 127.0.0.1 : ip 
			 8888 : port 
			 
Socket : 소켓이란 네트워크 연결의 양 끝단위(end-point)로서 통신을 하기 위한 인터페이스를 제공한다 ( 실세계 예 - 전화기 ) 	
		   코드 예 )
		   Socket socket=new Socket(serverIp,port);	
		   socket.getOutputStream() -> 출력스트림 
		   socket.getInputStream() -> 입력스트림 	
		   
ServerSocket : 통신 서버를 구현하기 위한 객체 
				  코드 예 ) ServerSocket serverSocket=new ServerSocket(port);	
				  			Socket socket=serverSocket.accept(); //접속을 대기하다가 클라이언트 접속하면 실행된다. 실행 후 일반 Socket을 반환한다
				  			//반환받은 일반 socket으로 실제 클라이언트와 통신하게 된다  	 
				  			//ServerSocket은 대표전화 , Socket은 상담원 전화기(실제 고객과 통신)   	 


step1
서버는 클라이언트의 접속을 대기하다가 클라이언트가 접속하면 
메세지를 출력하고 그 메세지를 클라이언트는 입력받아 화면에 출력하고 
서버 , 클라이언트 모두 종료되는 프로그램 

ServerSocket : 대표전화, 접수처 역할 		 Socket : 실제 통신 역할 


Server 											Client
------											-----
ServerSocket(port) 생성
Socket socket=serverSocket.accept();       Socket socket=new Socket(IP,PORT);  
socket.getOutputStream()					   socket.getInputStream() 
close()											   close()

--------------------------------------------------------------
step2
서버는 다수의 클라이언트의 접속을 처리해 메세지를 출력하도록 step1을 변경해본다 ( 동시 접속 처리는 아니고 , 순차적으로 처리한다 ) 
클라이언트는 step1과 변화가 없다 

--------------------------------------------------------------
step3
step2 역할을 서버 , 클라이언트가 바꿔본다 

서버는 접속을 대기, 클라이언트가 접속해서 메세지를 출력하면 그 메세지를 입력받아 서버 콘솔에 출력하고 연결 종료한 후
다음 클라이언트의 접속을 대기한다( 반복 ) 

클라이언트는 서버에 접속해서 메세지를 출력하고 자신은 종료한다  

-------------------------------------------------------------
step4 : review 

-------------------------------------------------------------

step5 : EchoServer 와 EchoClient ( 1 대 1 지속적 통신 )
		 EchoClient가 EchoServer에 접속하여 
		 메세지를 출력하면
		 그 메세지를 EchoServer가 입력받아 
		 다시 EchoClient로 메세지를 출력하는 프로그램 
		 
		 EchoServer			EchoClient
		 			  <----- 안녕 	
					  ------> 안녕 *server*
					  
					  <------ 불금
					  ------> 불금 *server*
					  
		 EchoServer에 필요한 요소 
		 ServerSocket : accept() 
		 Socket 
		 BufferedReader>InputStreamReader>socket.getInputStream() 
		 PrintWriter>socket.getOutStream() 
		 
		 EchoClient에 필요한 요소 
		 Socket(ip,port)
		 Scanner(System.in)
		 PrintWriter>socket.getOutputStream()
		 BufferedReader>InputStreamReader>socket.getInputStream() 

----------------------------------------------
step6  MultiServer :  다수의 Client에게 지속적으로 메아리 서비스 
		step5 의 EchoClient 프로그램은 그대로 유지되고 
		step5 의 EchoServer 프로그램을 업데이트한다 
		
		하나의 서버가 지속적으로 접속을 유지하면서 다수의 클라이언트에게 서비스 하기 위해서는 
		프로세스 내부의 세부적 실행단위인 Thread를 이용해야 한다 	
		(ex - 콜센터에서 다수의 고객과 동시에 상담서비스를 하기 위해 직원을 다수 채용해야 하는 것과 같다)
		
		MultiServer 에서는 클라이언트 접속을 대기하다가 접속하면 해당 클라이언트와 통신하기 위한
		Socket(전화기)을 반환받아 ServerWorker(직원) 객체 생성시에 할당하고 
		Thread를 생성해 start 시킨다  ( 이를 반복 ) 
		
		Runnable Interface 의 하위인 ServerWorker 는 할당받은 소켓으로
		클라이언트와 메아리 서비스를 진행한다 			


​	 
​		 
​		 
​		

--------

step 7

채팅 프로그램 구현하기

다수의 클라이언트에게 지속적으로 채팅 서비스하는 서버





---------------

# 방과후 따로공부 :pencil:



## 제네릭 사용 이유

- 컴파일 시 강한 타입 체크

- 타입 변환 제거

- ```java
  List list = new ArrayList();
  list.add("hello");
  String str = (String) list.get(0);
  ```

  - 제네릭을 사용하지 않은 리스트 요소 반환 코드

- ```java
  List<String> list = new ArrayList<String>();
  list.add("hello");
  String str = list.get(0); // 타입 변환을 하지 않습니다.
  ```

  - 제네릭을 사용한 리스트 요소 반환 코드

### 제네릭 타입(class, interface)

- 타입을 파라미터로 가지는 클래스와 인터페이스

- 제네릭 타입은 클래스 또는 인터페이스 이름 뒤에 ``<타입 파라미터>``가 붙음

  ``public class 클래스명 <T> {메소드 내용}``

