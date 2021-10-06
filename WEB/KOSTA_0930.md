- JSP : Client의 요청을 분석 , Java Beans와 연동, 적절한 결과를 Client에게 응답 
- Java Beans : Java Class(or Object) 들로 구성된 컴포넌트를 말한다
  - Java Beans는 DB 연동 로직과 Business 로직을 수행
  - 컴포넌트란 **객체들이 상호 연동되어 독립적 기능 단위를 구성**하는 것



## Query String

- 웹프로그램에 **입력데이터를 전달**하는 방법
- `URL ? Query String(name=value&name=value)`와 같은 형식
  - `http://localhost:8888/step2-2-querystring-action.jsp?no=2&food=갈비`
- `?`: URL 주소와 Query String을 구분
- `&`: 여러 쌍의 데이터를 전달할 때 사용

### JS 이벤트 처리 시

- `onclick`: form 요소에 마우스 클릭 시 발생하는 이벤트
- `onchange`: form 요소의 value가 변경되었을 때 발생하는 이벤트
- `onsubmit`: form 전송 시 발생하는 이벤트
- `onkeyup`: 키보드의 키를 눌렀다가 뗄 때 발생하는 이벤트

