Stream

: 입출력을 위한 장치/파이프라인, 빨대와 같음

**16일차 주요목차**

- String/StringBuilder/StringBuffer 

---------------



## 문자열을 다루는 String 과 StringBuilder 의 특징  

- ``String ``: 불변 , 상수 -> 문자열 상수영역( literal pool )에 저장 , 한번 생성된 문자열을 여러 곳에서 공유해서 사용 

  :point_right: **동일한 문자열이 자주 사용**될 경우 **메모리를 효율**적으로 사용

  - String 문자열을 메서드를 이용해 데이터를 추가 또는 삭제 또는 수정할 경우
    - **자체가 변경되지 않고 새로 생성** 

- ``StringBuilder`` : 가변 , StringBuilder 메서드를 이용해 추가 또는 삭제 또는 수정할 경우 자체가 변경 
  - **동일한 문자열이 자주 변경될 때 유리** 

|  String  | StringBuilder | StringBuffer |
| :------: | :-----------: | :----------: |
|   불변   |     가변      |     가변     |
| 새로생성 |  자체가 변경  | 자체가 변경  |
|          |               | 동기화 지원  |



## **IO**

- ### IO 

  - Input(입력) , Output(출력) 

- ### Stream 

  - 사전적 의미는 줄기 , 관 (pipe line) 
  - 입출력을 위한 장치 (파이프라인) 

- ###  IO 계열의 4가지 Abstract class 				 

|     1byte     |    2byte    |
| :-----------: | :---------: |
| 바이트 스트림 | 문자 스트림 |
|  InputStream  |   Reader    |
| OutputStream  |   Writer    |

 										 

- NodeStream 계열 
  - 직접 Device(장치)에 연결되는 스트림 , 필수적 
- ProcessingStream 계열 
  - 다양한 기능을 지원 , NodeStream계열의 스트림을 필요로 한다 	