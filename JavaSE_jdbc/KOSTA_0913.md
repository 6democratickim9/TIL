https://techblog.woowahan.com/2551/



ERD ( Entity Relationship Diagram ) 

: 개체 관계 모델링 즉 데이터 모델링을 위한 다이어그램 



ERWIN : ERD(entity-relationship diagram) Tool





File -> New -> Logical/Physical 버튼 선택 

-> Logical 데이터 모델링부터 구성 



ERWIN 환경 설정 

메뉴 Model - Model Propertie 선택

Model Properties 대화상자- 세 번째 Notation탭에서 Logical Notation Physical Notation영역 모두 IE옵션 버튼을 선택







Entity명

\----------

기본키

\----------

일반속성영역





이미지 추출 

메뉴 Tools - Report Template Builder - Report Builder - Report Templates - Picture 선택후 화살표 클릭

\- File -run - brower 뜨면 이미지 다운 가능



HTML 안나올때는 경로 변경

Report Template Builder -> Edit -> Properties ->Export탭-> Generated File 위치변경





Physical 모드에서 컬럼타입보기

DataType display

Format Tab -> Table Display -> Column DataType 



기본데이터타입변경 

Model Tab -> Model Properties -> Defaults -> VARCHAR2(100) 으로 변경





ERD ( Entity Relationship Diagram ) 

: 개체 관계 모델링 , 관계형 데이터베이스 설계를 위한 다이어그램 



논리 데이터 모델링 

\- 논리적인 데이터 관리 및 관계를 정의한 모델.

전체 업무 범위와 업무 구성요소를 정의하고 확인할 수 있다. 



물리 데이터 모델링 

\- 논리 데이터 모델을 DBMS 특성에 맞게 구체화시킨 모델을 말한다 



식별관계 (identified relationship): 부모 테이블의 기본키 혹은 복합키가 자식 테이블의 기본키 혹은 복합키의 구성원으로 전이되는 관계 ( ex - 사원과 신체정보 ) 

- 장점
  - 데이터의 정합성 유지를 DB에서 검증함
- 단점
  - 구조 변경이 어려움

비식별관계(non-identified relationship): 부모 테이블의 기본키 혹은 복합키가 자식 테이블의 일반속성으로 전이되는 관계 (ex - 부서와 사원정보 ) 

- 장점
  - 구조 변경이 자유로움
  - 부모 데이터로부터 독립
- 단점
  - 데이터 정합성을 위한 로직 필요
  - 데이터 무결성 보장 하지 않음



### Foreign Key 제약조건과 Join SQL

- ERD: 관계형 데이터베이스 설계를 위한 다이어그램

- 정규화: 데이터베이스 설계 시 중복을 최소화하고 무결성을 보장하기 위해 데이터를 구조화하는 작업

- Foreign key 제약조건: 참조 무결성 보장을 위한 제약조건, 다른 테이블의 정보를 참조할 때 지정해야 하는 제약조건

  - 부모테이블: 부서
  - 자식 테이블: 사원

  사원 정보가 사원테이블에 저장되기 위해서는 반드시 부서테이블에 저장되어 있는 부서번호로만 사원의 부서번호 정보로 저장될 수 있다

  부서테이블에 존재하지 않는 부서번호로 사원테이블에 사원 정보의 부서번호로 저장될 수 없다