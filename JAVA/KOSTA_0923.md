모든 서블릿과 jsp는 일반적으로 HttpServlet을 상속받는다

- `doGet()method`: 클라이언트 측에서 get 방식 요청시에 실행되는 메서드
- `HttpServletRequest`:클라이언트 요청 정보
- `HttpServletResponse`: 클라이언트에게 응답하기 위한 정보





Http Request Method

- get
  - 정보 조회용, url 상에 전송 정보가 노출됨, 전송 데이터 용량에 제한
- post
  - 정보 전달용, 주로 서버 자원의 데이터 변경시 사용
  - url 상에 전송 정보가 노출되지 않고 http request body 부분에 저장됨

### client(html form) 과 server(servlet) 연동

- client

  - ```html
    <form action="url pattern" method="get">
        <input type="text" name="food">
        <input type="submit" value="주문">
    </form>
    ```

  - submit을 누르면 아래와 같은 형식으로 전송됨

- server

  - url pattern 에 해당하는 서블릿의 doGet 메서드가 실행
  - 클라이언트가 보낸 정보를 얻기 위해



```html
<a href="GetTestServlet?food=김밥&count=7">get Test</a>
```

- 이와 같이 a tag를 이용한 링크로 데이터를 전송할 수 있음
- 링크 또한 get 요청방식

### DOM

- document.getElementByName(name)-> javascript array

