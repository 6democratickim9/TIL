**18일차 주요목치**

- 객체 직렬화
- IO를 이용한 Mini Project

----------

### 객체 직렬화

> 메모리 상에 있는 객체 정보를 연속적인 데이터로 변경하여 외부로 전송할 수 있는 상태를 만드는 것

객체 역직렬화

> 외부에 저장되어 있는 정보를 객체로 복원하여 메모리에 적재

객체 직렬화 특징

> 객체 직렬화를 위해서는(객체가 외부로 전송되기 위해서는) 해당 클래스가 반드시java.io.Serializable Interface를 implements 해야 한다

- java.io.Serializable Interface 계층구조 하에 있어야 한다



객체 직렬화를 위한 Processing Stream: Object OutputStream writeObject

객체 역직렬화를 위한 Processing Stream: Object Input Stream readObject(): Object

