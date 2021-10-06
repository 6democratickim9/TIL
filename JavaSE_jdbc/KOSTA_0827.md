step 4 

: review

step 5

: 로컬 테스트

Echo Server 와 Echo Client(1:1-> 지속적 통신)

Echo Client사 Echo Server에 접속하여 메세지를 출력하면

메세지를 다시 Echo Server가 입력받아 다시 Client로 출력하는 프로그램

Echo Server에 필요한 요소

ServerSocket :accept)

Socket

BufferedReader>InputStreamReader>socket.getInputStream()



EchoClient에 필요한 요소

- Socket(ip.port)
- Scanner(Systrm.in)
- printWriter>socket.getOutputStream()
- BufferedReader>InputStreamReader>socket.getInutStream()







step6

다수의 Client에게 지속적으로 메아리 서비스

Step5의 EchoClient 프로그램은 그대로 유지되고

step5의 EchoServer 프로그램을 업데이트한다

하나의 서버가 지속적으로 접속을 유지하면서 다수의 클라이언트에서 서비스 하기 위해서는 세부적 실행단위인 Thread를 ㅣ용해야 한다

MultiServer 에서는 클라이언트 접속을 대기하다가 접속하면 해당 클라이언트와 통신하기 위한 소켓을 반환받아ServerWorker 객체 생성 시에 할당하고 스레드를 생성해 start 시킨다

Runnable Inteface의 하위인 ServerWorker는 할당받은 소켓으로 클라이언트와 메아리 서비스를 진행한다

---------

인터페이스는 내용은 없고 메소드 선언만 있다!

