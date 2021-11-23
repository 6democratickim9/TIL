## Web Service & Web Application 

- Web Service
  - 네트워크 상에서 서로 다른 종류의 컴퓨터들 간에 상호작용하기 위한 소프트웨어 시스템
- Web Application
  - 웹 어플리케이션에서 서비스로 전달되는 요청 정보를 request
  - 서비스에서 처리된 결과값을 어플리케이션으로 전달되는 전달값을 response라고 함
  - 일반적으로 xml이나 json을 사용함



### SOAP

- XML 기반의 메세지를 전달하는 시스템을 얘기함
- 우리가 사용하는 기본적인 메세지 전달 수단
- Simple Object Access Protocol
- 오버헤드가 심하고 무거운 단점이 있어 REST 사용이 더 많아짐

### REST

- Representational State Tranfer
  - Resource의 Representation에 의한 전달
    - 컴퓨터가 가지고 있는 자원의 상태
    - 자원: 파일, db에 저장된 데이터 등 각각 고유하게 표현하기 위한 이름으로 구분한 후 그 자원이 가진 정보값 교환
- REST 서비스
  - 자원의 형태를 표현하기 위한 서비스
  - HTTP메소드를 이용해서 리소스를 처리하는 아키텍쳐
  - REST를 사용하기 위해 HTTP 프로토콜 사용
  - HTTP
    - HTTP Methods, HTTP Status Code로 구성됨
    - Method: 프로토콜을 통해 서버에 전달하는 목적, 수단을 알려줌
    - HTTP Status Code: 응답 코드와 함께 전달 결과를 받을 수 있음