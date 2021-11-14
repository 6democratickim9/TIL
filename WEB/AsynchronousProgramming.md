https://www.youtube.com/watch?v=m0icCqHY39U

## 동기와 비동기

- ### 동기

  - 순차적으로 -> 실행이 완료되면 다음 순서로 진행됨다
  - 코드는 작성 순서대로

  

- ### 비동기

  - 순서대로 실행되지는 않음

예시) 짜장면과 배달부

- 주문자가 식사를 할 동안 배달부는 다른 일을 한다?

  =스레드!

  - 프로그램이 비동기로 일을 한다 = 쓰레드나 프로세스가 여럿이 돌고 있다는 말

  - 멀티태스킹 구현



![image-20211114230905717](C:\Users\MIN\TIL\WEB\AsynchronousProgramming.assets\image-20211114230905717.png)

- js 예시

  - 배달부가 짜장면을 배달하자마자 배달원은 다음 장소로 떠남

  - 1초 뒤 식사 완료 로그

  - 인자로 function() 이 들어감

    = 비동기로 주어진 일을 다 마친 다음에는 이 함수 실행하도록 맡겨둠

    ### = 콜백 함수

  

- ### 자바스크립트는 싱글 쓰레드 아닌가? :thinking:

  - 자바스크립트는 웹 브라우저나 노드 js의 자바스크립트 엔진에서 실행됨
    - 엔진 안에는 자바스크립트를 돌리는 하나의 스레드가 존재
  - 자바스크립트가 도는 환경에는 엔진 뿐만 아니라 Web API도 같이 동작
    - 타이머 작업/ ajax로 http 요청을 보내거나 파일에서 데이터를 읽어오는 등의 작업을 함
    - 이 중 하나에 해당하는 태스크가 선로 진입부로 들어오면 컴퓨터는 비동기 작업용 선로에 올려놓음
    - 선로는 한 번에 여러 개가 만들어질 수 있음
    - 이 태스크들은 보통 콜백을 가지고 있음
    - ![image-20211114232334679](C:\Users\MIN\TIL\WEB\AsynchronousProgramming.assets\image-20211114232334679.png)

이런 모양으로 운영된다

![image-20211114232356478](C:\Users\MIN\TIL\WEB\AsynchronousProgramming.assets\image-20211114232356478.png)- 이 장치는 이벤트 루프라고 불림

- 태스크 큐를 타고 들어오는 콜백 칸들을 기다리고 있음
- 콜백이 도착하는 대로 js 전용 칸으로 올려줌
- 대학생인 학생의 고등학교 수학 교사를 찾는 코드 예시
- ![image-20211114232639542](C:\Users\MIN\TIL\WEB\AsynchronousProgramming.assets\image-20211114232639542.png)

콜백 안에 콜백 안에 콜백...

- 콜백 지옥,,,이라고 이런 코드를 부른다

- 이런 문제 해결을 위해 자바스크립트는 ES6 버전부터 Promise를 도입

- ![image-20211114232911112](C:\Users\MIN\TIL\WEB\AsynchronousProgramming.assets\image-20211114232911112.png)

  - 비동기 작업 수행 함수가 Promise 객체 반환

    - `.then(function(parameter))`

  - 생성자에 인자로 들어가는 함수

    - 첫 번째 인자로는 수행할 **비동기 작업**
    - 두 번째 인자로는 그 **결과물을 콜백에 전달**

    -> 라이브러리 없이는 익스플로러에서 작동하지 않음

  - ES7 에는 `Async/await` 등장

![image-20211114233153882](C:\Users\MIN\TIL\WEB\AsynchronousProgramming.assets\image-20211114233153882.png)

