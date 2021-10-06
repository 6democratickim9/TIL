https://www.youtube.com/watch?v=1QiOXWEbqYQ&list=PLpO7kx5DnyIFQ4XuYirD--DvRyUgaHD9w&index=20

https://mangkyu.tistory.com/56

# Session,Token&JWT 💡

- 인증
  - Authentication
  - 로그인/ 특정 권한이 주어진 사용자임을 인증받음
- 인가
  - Authorization
  - 인증 받은 사용자가 계정으로만 할 수 있는 활동
  - 서버는 사용자를 알아보고 활동 할 수 있게 해줌!
  - JWT와 연관깊음



1. 사용자가 로그인 성공 시 → (서버)세션 표딱지 출력
2. 표딱지는 각각 서버와 클라이언트 측에 반씩 저장됨
3. 브라우저: SessionID 란 이름의 쿠키로 저장
   - 쿠키: 브라우저에 저장되는 정보
4. 브라우저는 사이트에 요청을 보낼 때 마다 해당 표딱지를 실어보냄
5. 서버는 맞는 짝이 있는지 찾아보고 Authorization 해줌
6. 서버에 로그인 되어있음이 지속되는 상태: 세션

#### :warning: 서버가 재부팅될 시 메모리에 있는 것들은 다 날아가게 됨



## JWT

- Json 포맷을 이용하여 사용자에 대한 속성을 저장하는 Claim기반의 Web Token

- 토큰 자체를 정보로 사용하는 Self-Contained 방식으로 정보를 안전하게 전달

- Header,Payload,Signature 세 부분으로 구성되며, 각 부분은 Base64로 인코딩 되어 표현됨

  - 각각의 부분을 이어주기 위해서는 구분자를 사용함
  - Bse64는 같은 문자열에 대해 항상 같은 인코딩 문자열 반환

- ### Header

  - **typ**과 **alg** 두 가지 정보로 구성
    - alg: Signature를 해싱하기 위한 알고리즘을 지정
    - typ: 토큰의 타입을 지정

- ### PayLoad

  - 토큰에서 사용할 정보의 조각들인 **클레임(Claim)**이 담겨있음

    - 클레임은 총 3가지로 나누어지며, Json 형태로 다수의 정보 삽입 가능

  - **등록된 클레임**

    - 토큰 정보를 표현하기 위해 이미 정해진 종류의 데이터들
    - 선택적 작성 가능, 사용 권장됨
      - iss: 토큰 발급자(issuer)
      - sub: 토큰 제목(subject)
      - aud: 토큰 대상자(audience)
      - exp: 토큰 만료 시간(expiration), NumericDate 형식으로 되어 있어야 함 ex) 1480849147370
      - nbf: 토큰 활성 날짜(not before), 이 날이 지나기 전의 토큰은 활성화되지 않음
      - iat: 토큰 발급 시간(issued at), 토큰 발급 이후의 경과 시간을 알 수 있음
      - jti: JWT 토큰 식별자(JWT ID), 중복 방지를 위해 사용하며, 일회용 토큰(Access Token) 등에 사용

  - **공개 클레임**

    - 사용자 정의 클레임으로, 공개용 정보를 위해 사용됨

    - 충돌 방지를 위해 URI 포맷 이용

      - ```json
         scheme:[//[user[:password]@]host[:port]][/path][?query][#fragment]
        ```

  - **비공개 클레임**

    - 사용자 정의 클레임

    - 서버와 클라이언트 사이에 임의로 지정한 정보 저장

    - ```json
       "token_type": access 
      ```

- ### Signature

  - 토큰을 인코딩하거나 유효성 검증을 할 때 사용하는 고유한 암호화 코드

    1. 위에서 만든 헤더와 페이로드의 값을 각각 BASE64로 인코딩
    2. 인코딩 값을 비밀 키를 이용해 헤더에서 정의한 알고리즘으로 해싱
    3. 해싱 값을 다시 BASE64로 인코딩하여 생성

    - 생성된 토큰은 HTTP 통신 시 Authorization이라는 key의 value로 사용됨

    - ```json
      "Authorization": "Bearer {생성된 토큰 값}",
      ```

      