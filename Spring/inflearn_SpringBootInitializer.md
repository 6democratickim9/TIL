- 나는 커뮤니티 버전이라 spring-boot initializr이 따로...보이지 않아서
-  https://start.spring.io/
- 여기서 따로 생성해서 해야됨. 캐안습 ㄱ-

![image-20211124203055932](C:\Users\MIN\TIL\inflearn_spring\SpringBootInitializr.assets\image-20211124203055932.png)

- Group
  - 개발하고자 하는 팀 이름, 회사 이름 지정
  - 도메인 이름으로 사용됨
  - 패키지 이름으로도 같이 사용될 수 있음
- Articfact
  - 개발하고자 하는 프로젝트/어플리케이션 이름 입력
  - restful-web-service
- Type
  - Maven Project
- Language
  - 개발언어
  - Java
- Package
  - 패키징 형태
  - war파일 형태로 패키징할 경우에는 우리가 만들었던 spring boot 프로젝트가 다른 웹 어플리케이션 서버에 배포될 경우에는 war
  - 독립적인 서버라면 jar로 배포 선택
- java version은 8



![image-20211124203546389](C:\Users\MIN\TIL\inflearn_spring\SpringBootInitializr.assets\image-20211124203546389.png)

- Dependency 추가
- ![image-20211124203818439](C:\Users\MIN\TIL\inflearn_spring\SpringBootInitializr.assets\image-20211124203818439.png)

이렇게 선택 후 generate

내 프로젝트 관련 리소스들은 

- `C:\Users\사용자이름\.m2\repository\org` 여기서 확인 가능