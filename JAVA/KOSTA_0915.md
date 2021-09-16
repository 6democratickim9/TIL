내PC-> 설정-> 고급 시스템 설정 -> 환경변수 새로만들기 -> 

![image-20210915092711940](C:\Users\MIN\TIL\JAVA\KOSTA_0915.assets\image-20210915092711940.png)

startup.bat 실행

![image-20210915102700415](C:\Users\MIN\TIL\JAVA\KOSTA_0915.assets\image-20210915102700415.png)

![image-20210915142509962](C:\Users\MIN\TIL\JAVA\KOSTA_0915.assets\image-20210915142509962.png)

![image-20210915102805356](C:\Users\MIN\TIL\JAVA\KOSTA_0915.assets\image-20210915102805356.png)

![image-20210915103105997](C:\Users\MIN\TIL\JAVA\KOSTA_0915.assets\image-20210915103105997.png)

![image-20210915103235147](C:\Users\MIN\TIL\JAVA\KOSTA_0915.assets\image-20210915103235147.png)

startup.bat 으로 실행하면 서버를 띄울 수 있다!

-----

### Ecma 인터내셔널

- 정보 통신 표준을 제정하는 포준화 기구

### Javascript

- ECMAScript 표준을 준수하는 스크립트 언어

### ECMAScript

- 다양한 브라우저에서 일관성 있는 동작을 위한 스크립트 표준

ES5(ECMA5, 2009) : 변수 선언  var -> 중복선언 가능 ( Function-level scope ) 
ES6(ECMA6, 2015) : 변수 선언 추가  let -> 중복선언 불가 ( Block-level scope ) , 상수 선언 const 등이 추가 

### DOM

- HTML 문서를 제어하기 위한 프로그래밍 인터페이스
- 웹브라우저에서 지원, html문서 요소를 계층적으로 표현, 각 요소를 조작하기 위한 방법 제공

-----------

### 방과후 따로공부타임 :pencil:

https://hianna.tistory.com/480

### 1. innerText와 innerHTML의 차이점? :thinking:

- `innerText`

  - `element` 안의 text 값들만 가져옴

    ​	:point_right: html을 포함한 문자열 입력 시 html코드가 문자열 그대로 **element 안에 포함**됨

- `innerHTML`

  - element 안의 HTML이나 XML을 가져옴



https://stackoverflow.com/questions/8823498/setting-innerhtml-vs-setting-value-with-javascript

### 2. `innerHTML`과 `value`의 차이점?:thinking:

- `value`는 일반적으로 `input/form` `element`에 사용됨(입출력 elements들)
- `innerHTML`은 일반적으로 `div,span,td`와 비슷한 `element`에 사용된다
  - `form`을 제외한 모든 `element`들에 사용가능함

