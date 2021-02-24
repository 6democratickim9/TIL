# 장고

* 정적인 웹과 동적인 웹의 차이: 웹 상에 표현되는 데이터를 DB에 저장했다가 불러올 수 있는가/없는가에 따름



* MVC 패턴: Model View Controller

  * model(DB연동)view(화면)controller(중재자-로직포함)

* MTV 패턴: Model Template View

  * model(DB연동)template(화면)view(중재자 로직포함)

* html 안에 python코드 삽입 시

  ​	``` {%파이썬 코드%}```

* manage.py는 건들이면 안됨

* 별도의 서버와 연결 시 asgi.py/wsgi.py 를 수정하면 된다.

* models--> 주로 데이터베이스에 대한 정보가 들어간다.

* view: 기능적인 부분 수행. 템플릿과 연결해서 사용한다.