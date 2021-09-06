** jdbc basic**

# JDBC

> Java DataBase Connectivity

- 자바 어플리케이션과 데이터베이스 연동을 위한 기술

- 일반사용자 <> Java Application <> JDBC<> Database

- 생산성/유지보수성 :up:

- Prepared Statement

  - 객체를 캐시에 담아 재사용

- execute를 실행시킬 수 있는 메소드를 가지고 있음

  :point_right:overriding 된 메서드가 실행될 것

## JDBC 설계방식

- Sun 에서는 JDBC 표준(인터페이스)을 설계

- DB Vendor (회사) 에서는 JDBC표준에 의거해 개발(인터페이스를 implements 한 class를 정의)

- 자바 응용프로그램(어플리케이션) 개발자는 JDBC 사용

  :point_right: 하나의 사용방식만 익히면 됨(생산성 향상)

- 각 DB Vendor에서 자신의 시스템을 업데이트 해도 외부 영향은 최소화, 즉 결합도가 낮아져서 유지보수성이 향상

- 만약 데이터베이스 제품군이 변경되어야 하더라도 어플리케이션 변경은 최소화, JDBC 연동 부분은 같으므로 각 DB의 sql 특성만 고려하면 된다

- 하나의 메세지 방식(JDBC 표준 인터페이스) 으로 다양한 구현 객체( Oracle, Mysql, MS SQL, DB2 ) 들이 각자의 방식으로 동작하게 할 수 있다

## JDBC 프로그래밍 개발단계

- SELECT정보 조회
  1. JDBC Driver loading
  2. Connection
  3. PreparedStatement
  4. SQL 실행: executeQuery()
  5. ResultSet
  6. close

- ``INSERT,DELETE,UPDATE``

- 정보 생성, 삭제 수정

  1. JDBC Driver loading
  2. Connection
  3. PreparedStatement
  4. SQL 실행: executeUpdate()
  5. close

- ``PreparedStatement``

  - ``Statement`` 클래스의 기능 향상

  - 인자와 관련된 작업이 특화(매개변수)

  - 코드 안정성/ 가독성 높음

  - 코드량이 증가 -> 매개변수를 ``set``해줘야 해서

  - 텍스트SQL 호출

  - ```java
    	public void register(GuestBookDTO dto) throws SQLException {
    		Connection con=null;
    		PreparedStatement pstmt=null;
    		try {
    			con=DriverManager.getConnection(url, username, password);
    			StringBuilder sql=new StringBuilder();
    			sql.append("insert into guestbook(guestbook_no,title,content) ");
    			sql.append("values(guestbook_seq.nextval,?,?)");
    			pstmt=con.prepareStatement(sql.toString());
    			pstmt.setString(1, dto.getTitle());
    			pstmt.setString(2, dto.getContent());
    			pstmt.executeUpdate();
    		}finally {
    			closeAll(pstmt, con);
    		}
    ```

    - 코드는 위와 같이 작성됨