DATE 타입: 데이터베이스 시간(년,월,일,시,분,초)를 관리하는 데이터 타입

주요 함수

1. to_char(): 데이터베이스에 저장된 DATE 형의 정보를 문자열로 반환받을 때 사용하는 함수
2. to_date(): 문자타입의 시간 정보를 데이터베이스의 DATE 형으로 변환해 저장할 때 사용하는 함수

SYSDATE 예약어: 현재 시간을 표현하는 키워드

참고) Oracle DUAL 테이블: 오라클에서 제공하는 기본 테이블, 함수 및 키워드를 실행할 때 사용

```sql
SELECT SYSDATE FROM DUAL;
```

TO_CHAR()를 이용해 원하는 시간 포맷을 설정해 문자열로 반환받아 본다

```sql
SELECT TO_CHAR(SYSDATE,'YYYY-MM-DD') FROM DUAL;
```

