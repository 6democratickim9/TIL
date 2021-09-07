# 오라클 시퀀스 :notebook_with_decorative_cover:

- 순차적으로 증가, 유일한 값을 생성하기 위한 객체 

- 주로 primary key ( unique + not null ) 를 생성하기 위해 사용

  - Mysql의 `auto_increment`랑 비슷한듯

- 테이블과는 독립적인 구조

- 실제 적용 시 ``시퀀스명.nextval``

  :point_right: **다음 시퀀스 값이 반환**
  - 실제 DAO 적용사례

    - ```sql
      insert into guestbook(guestbook_no,title)values(guestbook_seq.nextval,?)
      ```

- ``시퀀스명.currval``
  - **현재 시퀀스 값을 반환** 
  - 단, `currval`은 시퀀스를 `nextval` 한 세션 내에서만 사용가능
    - 연결시작~연결종료 까지 `nextval` 한 커넥션 내에서만 curval을 이용할 수 있다

- ### **session**

  - database에 사용자가 접속~ 종료 시까지 유지되는 정보

- ### **트랜잭션**

  - 작업단위(or 업무단위) **데이터베이스의 상태를 변경**시키기 위해 수행하는 작업단위

- ```sql
  CREATE SEQUENCE 시퀀스명 
  [START WITH 시작번호]
  [INCREMENT BY 증가값]
  [MAXVALUE 최대값] 
  [MINVALUE 최소값]
  [ CYCLE or NOCYCLE ] 
  [ NOCACHE ] 
  ```

## 

### Oracle dual table

- 오라클에서 제공하는 기본 테이블
- 컬럼 하나만 존재
- 주로 시퀀스 또는 날짜함수, 산술연산에 사용
- sys Admin 계정에서 관리하고 수정 및 삭제 등 조작은 불가

### DCL 

`COMMIT,ROLLBACK`

- **COMMIT**: 변경된 작업 내용을 **실제 데이터베이스에 반영**(실제 저장)
- **ROLLBACK**: 변경된 작업 내용을 취소하고 이전 상태로 되돌림

- Application에서 트랜잭션 처리

- JDBC 기본 트랜잭션 설정
  - Auto Commit -  True에서 수동모드로 변경
  - Connection의 Method: setAutoCommit(false)

트랜잭션의 기본 설정인 `AutoCommit` 모드를 **수동으로 변경**한 후 트랜잭션 내 모든 작업이 정상적을 진행되었을 때

## SubQuery

- 서브 쿼리

- SQL내의 SQL

- 예시 코드

- ```sql
  -- 연습)  product 중 가장 낮은 price 의 상품의 maker는 ?  오뚜기 
  select maker from product where price=(select min(price) from product);
  ```

  

----------

## 쿠키,세션,캐시가 뭔가요? :thinking:

https://www.youtube.com/watch?v=OpoVuwxGRDI

## 쿠키 :cookie:

- **사이트를 방문하고 이용할 때 브라우저에 저장되는 내용들**

- 사용자가 임의로 수정/삭제 가능

- 외부인이 훔쳐보거나 도둑질 용이

- 민감하거나 중요한 정보는 X

- 사용자의 브라우저에 저장되고, 통신할 때 **HTTP헤더에 포함되는 텍스트 데이터 파일**

- 키-값으로 구성됨

  - 해당 사용자의 컴퓨터 사용시 누구나 입력값 열람 가능

    :point_right: 보안성이 낮음

    

  ### 쿠키 통신 방법:telephone_receiver:

  1. 최초 통신에는 쿠키값 :x:, 클라이언트는 Request 보냄
  2. 서버에서 클라이언트가 보낸 Request Header에 쿠키가 없음을 판별/ 통신 상태를 저장한 쿠키를 반환(Response)
  3. 클라이언트의 브라우저가 받은 쿠키를 생성/보존
  4. 두번째 연결부터 HTTP Header에 쿠키를 실어서 서버에 Request 전송

  

  ### 쿠키 제약 조건 ⛔

  - 클라이언트는 총 300개의 쿠키를 저장할 수 있음
  - 하나의 도메인 당 20개의 쿠키를 가질 수 있다
    - 20개가 넘으면 가장 적게 사용되는 것 부터 삭제됨
  - 하나의 쿠키는 4KB 저장가능



### 세션 :computer:

- 서버에 저장되는 쿠키

- 쿠키에 저장하기 곤란한 정보들을 저장

- 세션을 사용하는 사이트에 접속하면 서버에서는 사용자 구분용으로 기한이 짧은 임시 키를 브라우저에 보내서 쿠키로 저장

  :point_right:사용자의 중요한 정보는 서버의 메모리나 데이터베이스에 저장

  브라우저가 해당 사이트의 페이지들에 접속할 때마다 http요청에 키를 실어서 전송

  서버는 키를 통해 사용자 인식-> 정보 가공 후 응답으로 전송

- 보안성이 비교적 높음



### 캐시 :moneybag:

- 리소스 파일들의 임시 저장소

- 같은 웹페이지에 접속할 때 사용자의 PC에서 로드하므로 서버를 거치지 않아도 됨

- 다양한 분야에서 사용되됨

  - 거의 공통적인 의미로 **가져오는데 비용이 드는 데이터를 한 번 가져온 뒤에는 임시로 저장**

- 웹 캐시는 이미지 등의 정보를 불러올 때 데이터 사용량도 발생하고 시간도 든다

  :point_right: 사용자가 여러 번 방문할 법한 사이트에서는 **한 번 받아온 데이터를 사용자의 컴퓨터/중간 서버에 저장**해둠

  

  #### 캐시 히트

  - CPU가 참조하려는 **메모리가 캐시에 존재**하고 있는 경우

  #### 캐시 미스

  - 캐시 히트와 반대로, **메모리에 캐시가 존재하지 않는** 경우

  #### 사용 방식

  - 홈페이지 재접속 시 css/js 파일을 사용자의 PC에서 로드, 서버를 거치지 않아도 됨





hmmmmm 더 찾아보고싶당 ( •̀ ω •́ )✧( •̀ ω •́ )✧

https://ryusae.tistory.com/7

### 쿠키와 세션을 사용하는 이유? :thinking:

- 기본적으로 HTTP는 *stateless 프로토콜*과 *Connectionless 프로토콜* 을 사용한다

  - **stateless 프로토콜**
    - 상태 정보를 가지지 않는 서버 처리 방식
    - 클라이언트와의 통신에서 연속적으로 데이터를 유지하지 않음
  - **Connectionless 프로토콜**
    - 클라이언트가 서버 요청 -> 요청에 맞는 응답을 보낸 후 연결 끊음
    - HTTP1.1 버전에서 keep-alive 값으로 변경 가능해짐

  :point_right: 실제로는 데이터 유지가 필요해서 Stateful 경우에 대처하기 위해 쿠키와 세션 사용

- 쿠키와 세션의 차이점?
  - 상태 정보의 저장 위치
  - **쿠키: 클라이언트**
  - **세션: 서버**



## 



