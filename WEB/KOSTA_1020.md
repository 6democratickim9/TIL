## EL

> Expression Language, JSP 버전이 상향되면서 추가된 스크립트 언어

- 기존 Script tag 의 표현식 (`<%=%>`)의 업그레이드 된 버전(`${}`)
- JSP 속성영역 (request, session, aplication(ServletContext))에 저장된 객체의 proerty를 출력
  - import 과정 및 별도의 Object casting 절차가 필요없음
- 다양한 연산 가능(자동 형변환)
- JSTL과 연동 가능
- EL은 Model 객체의 get 계열 메서드와 is 계열 메서드에만 접근 가능



## JSTL

> JSP Standard Tag Library, JSP에서 자주 사용하는 기능을 미리 구현해 놓은 커스텀 태그 라이브러리

- JSP에서 자주 사용하는 기능을 미리 구현해 놓은 커스텀 태그 라이브러리
  - 반복, 조건, 자료구조, 데이터 표현
- EL과 함께 사용해서 데이터 표현

- `forEach`: jstl for loop
- `items`: 저장된 배열 또는 컬랙션
- `var`: 요소를 저장할 변수
- `varStatus`: index와 count 속성
  - `index`는 0부터 시작
  - `count`는 1부터 시작