# 시스템 콜

- 시민: 사용자 혹은 어플리케이션

- 도서관: 운영체제

- 책 요청(신청서): API

  - 시민이 도서관에 원하는 책을 신청서를 작성해 요청

  - 도서관은 책을 찾아서 시민에게 빌려줌

  - 기한이 만료되면 도서관이 책을 회수함

    :point_right: 사용자/어플리케이션은 운영체제에 원하는 자원을 API를 사용해 요청

    운영체제는 적절한 자원을 찾아 사용자/어플리케이션에 빌려줌

    자원 사용이 완료되면 운영체제는 해당 자원 회수

### 응용 프로그램, 운영체제, 컴퓨터 하드웨어

- 운영 체제 :point_right: 응용프로그램이 요청하는 **메모리를 허가하고 분배**
- 운영 체제 :point_right: 응용프로그램이 요청하는 **CPU 시간 제공**
- 운영 체제 :point_right: 응용프로그램이 요청하는 **IO Devices 사용 허가/제어**

### 쉘

- 하나의 응용 프로그램
- 사용자가 **운영체제 기능과 서비스를 조작**할 수 있도록 인터페이스 제공
- 터미널 환경과 GUI 두 종류로 구분됨



- 운영체제는 응용 프로그램을 위해서 인터페이스 제공

  :point_right:프로그래밍 언어로 제공 = API

  - 보통은 API들을 종류별로 묶어서 라이브러리 형태로 제공
  - Application/shell은 라이브러리를 기반으로 생성됨



### 시스템 콜

- 운영체제가 **운영체제의 각 기능을 사용할 수 있도록 시스템 콜이라는 명령 또는 함수 제공**
- **API 내부**에는 해당 운영체제 기능을 사용 가능하게 할 수 있는 **시스템콜을 호출하는 형태**로 만들어지는 경우가 대부분



### 운영체제를 만든다면?

1. 운영체제 개발
2. 시스템 콜 개발
3. C API 개발
4. Shell 프로그램 개발
5. 응용 프로그램 개발



### 운영체제와 시스템 콜

- API: 각 언어별 운영체제 기능 호출 **인터페이스 함수**
- 시스템콜: **운영체제 기능을 호출하는 함수**



### 정리

- 운영체제는 **컴퓨터 하드웨어와 응용 프로그램을 관리**
- 사용자 인터페이스를 제공하기 위해 **쉘 프로그램을 제공**
- 응용 프로그램이 운영체제 기능을 요청하기 위해 **운영체제는 시스템 콜 제공**
  - 일반적으로는 **시스템 콜 사용해서 만든 API 사용**