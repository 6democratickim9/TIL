# git command

> git 을 사용하기 위한 기본 명령어



# 

## 설정

### 1. init

* git init
* 현재 폴더를 git으로 관리 하겠다 => .git 폴더를 생성
* 최초에 한번만 실행하는 명령어



### 2. config

* git config --global user.email " email@email.com"
* --global 옵션과 --local 둘중 하나 선택해서 사용
  * 일반적으로 global 설정을 해놓으면 내 컴퓨터에서 추가적으로 변경할 일 없음

### 3. status

* git status
* 현재 git 의 상태를 출력해주는 명령어

### 4. diff

* git diff
* 마지막 커밋과 현재 폴더 상태를 비교해서 차이점을 출력

### 5. log

* git log
* 커밋 히스토리 출력

### 6. remote add

* ```git remote add origin <url>```
* 깃아, 원격저장 추가해줘, 별명은 오리진이고, 실제 주소는 <url>이야. --> 원격저장







# 저장

### 1. add

* ```git add``` <추가하려고 하는 파일>
  * ```git add . ``` : 한 번에 모든 파일과 모든 폴더를 add
* ```working directory```에서 변경점을 staging area로 이동

### 2. commit

* git commit
  * ```git commit -m "메세지":``` 한번에 메세지까지 남김

### 3. push

* ```git push origin master```
* 원격저장소에 master 브랜치의 데이터를 전송





##### * 순서

* cd directory (git init 할 폴더)-> git init -> git add . -> git status -> git commit -m "커밋info"

* --> 새로 만든 저장소 주소 || git clone <주소 붙여넣기>

* --> git push origin master



## GIT Branch

> git branch 는 내부를 보여주는 것으로, 여러 작업을 진행할 때 작업 흐름 파악하기에 유용하다.



#### 1. git branch 생성

* ```git branch <이름>```
  * 브랜치 생성
* ```git checkout <이름> || git switch <이름>```
  * <이름> 으로 브랜치 전환

#### 2. branch 삭제

* ```git branch --delete  <브랜치 이름>```
  * --d 도 가능하다.

#### 3. git branch 작업내역 보기

* ``` git log --oneline (+"--graph"도 가능)```





##### * 충돌이 발생했을 때

``` <<<<HEAD``` 

```충돌정보 ```

```=============```

```충돌정보 ```

```> 코드코드코드코드```



* 코드와 HEAD 부분 삭제하고 충돌부분 합의 후 수정
* push!



##### * 초대가 되지 않은 repository 에도 clone 이 될까?

* 된다!

