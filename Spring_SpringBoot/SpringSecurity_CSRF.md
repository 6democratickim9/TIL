https://taesan94.tistory.com/134

**AJAX적용시 CSRF토큰 전달방식**

- Ajax 요청 Header에 csrf token 정보를 포함시켜서 전송한다.

- 중복체크를 누르면 수행되는 함수에 아래코드를 추가해 주었다.

- **ajaxSend**는 Ajax요청을 보내기전 호출되는 메서드이다.

- ```js
  $(document).ajaxSend(function(e, xhr, options) {
  xhr.setRequestHeader( "${_csrf.headerName}", "${_csrf.token}" );
  });
  ```

  

**FORM태그 전송시 CSRF토큰 전달방식**

- 일반적인 경우에는 아래와같이 hiddne속성의 input태그의 value를 넘겨주면된다.

```html
<input type="hidden" name="${_csrf.parameterName}" value="${_csrf.token}" />
```

- multipart/form-data로 지정된 경우에는 아래와같이 action의 url정보에 토큰 값을 같이 넘겨주면된다.. 

- ```js
  form method="post" enctype="multipart/form-data" action="/com/userRegist.do?${_csrf.parameterName}=${_csrf.token}">
  ```



1. 게시글 삭제 또는 수정 권한 없는 a라는 이용자가 게시글에 스크립트 또는 테그를 삽입하게 됩니다.

2. 게시글 삭제 또는 수정 권한 있는 b라는 이용자가 a가 작성한 글을 열람시 게시글 삭제 및 수정 스크립트 또는 태그가 실행 되어 공격이 발생합니다.

3. 이를 막기 위해서 수정, 삭제 등 api에 페이지 이동시  **동적으로 변하는 파라미터인 1회성 인증키인 csrf토큰을 추가** 하여 공격을 방어합니다.