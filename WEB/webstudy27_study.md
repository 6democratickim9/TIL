```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<%@taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>회원관리</title>
</head>
<body>
	<h3>회원관리( MVC , FrontController , DBCP, EL, JSTL )</h3>
	1. <form action="FindMemberByIdController.do">//Find
		<input type="text" name="id" placeholder="아이디" required="required">
		<button>검색</button>
	</form>

	<br>
	<br>
	<c:choose>
		<c:when test="${sessionScope.mvo==null}">
			<form action="LoginController.do" method="post">
				<input type="text" name="id" placeholder="아이디" required="required"><br>
				<input type="password" name="password" placeholder="패스워드"
					required="required"><br>
				<button type="submit">로그인</button>
			</form>
			<br>
			<br>
			<a href="register-member.jsp">회원가입</a>
		</c:when>
		<c:otherwise>
 		${sessionScope.mvo.name} 님 로그인 상태 <br>
			<br>
			<a href="LogoutController.do">로그아웃</a>
			<br>
			<br>
			<form action="FindMemberListByAddressController.do">
				<input type="text" name="address" placeholder="주소"
					required="required">
				<button>검색</button>
			</form>
			<br>
			<br>
			<a href="update-member.jsp">회원정보수정</a>
		</c:otherwise>
	</c:choose>
</body>
</html>


```

- ```jsp
  1. <form action="FindMemberByIdController.do">
  	<input type="text" name="id" placeholder="아이디" required="required">
  	<button>검색</button>
  </form>
  ```

  - 클릭하면 FIndMemberByIdController로 이동