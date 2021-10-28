# JOIN SQL :minidisc:

> **여러 테이블을 결합**하여 정보를 조회하기 위한 SQL 







## 1. INNER JOIN

- 일반적으로 `join`이라고 하는 SQL을 의미 

- **조인 조건에 부합되는 행**에 대해서만 조회

  ### 1. Equi Join

  - 조인 대상 테이블 간의 **상응하는 컬럼 정보가 정확하게 일치하는 경우**의 JOIN 

    - 부서 테이블과 사원 테이블간의 부서번호가 일치할 때 조인

    - 사원 정보 조회시 **사원이 속한 부서 정보**까지 함께 조회

    - ```sql
      select e.empno, e.ename, e.job, d.deptno, d.dname,d.loc
      from emp e, dept d 
      where e.deptno=d.deptno 
      ```

    - ```sql
      select e.empno, e.ename, e.job, d.deptno, d.dname,d.loc
      from emp e
      inner join dept d on e.deptno=d.deptno
      ```

      ![image-20211025195456473](C:\Users\MIN\TIL\SQL\KOSTA_1025.assets\image-20211025195456473.png)

      

  ### 2. Non Equi Join

  - 조인 대상 테이블 간의 **상응하는 컬럼 정보가 없을 때** 사용하는 JOIN

  - 테이블 간의 컬럼 값들이 **정확하게 일치하지 않을 때** 사용하는 JOIN 

    - 사원 테이블과 월급 등급 테이블간의 일치하는 컬럼은 없지만 사원의 월급 등급을 알기 위해 월급 등급 테이블의 hisal , losal 과 사원 테이블의 sal 을 비교 

    - ```sql
      select e.empno, e.ename, s.grade , e.sal , s.losal , s.hisal
      from emp e, salgrade s 
      where e.sal>=s.losal and e.sal<=s.hisal 
      and e.ename='SMITH'
      ```

    - emp 테이블의 empno, ename, sal을 가져오고, salgrade의 grade,losal, hisal을 조회한다
    - grade에서는 e.sal이 losal과 hisal의 범위 내에 있으며 ename은 스미스여야 한다

    

    - 조인하는 테이블 간의 **컬럼값이 일치되지 않는 경우는 조회되지 않는다** 

    - 사원이 존재하지 않는 40번 부서는 정보가 조회되지 않는다 

    - ```sql
      select e.empno,e.ename,e.deptno,d.deptno,d.dname
      from dept d, emp e 
      where d.deptno=e.deptno
      ```



## 2. Outer JOIN

- JOIN 조건에 부합되지 않더라도 **다른 행을 조회**하기 위해

  - 부서 테이블과 사원 테이블 조인시 INNER JOIN은 사원이 없는 부서는 제외 Outer JOIN 은 사원이 없는 부서라도 모두 조회

- **일반적인 조인 ( Inner Join ) 조건에 만족하지 않는 경우**에도 조회하기 위해 사용

- 부서와 사원 테이블 조인시 사원이 존재하지 않는 부서정보도 조회하기 위해 Outer Join을 이용

- JOIN 조건에 (+) 를 명시 -> 조인 시킬 값이 없는 측에 표기

- ```sql
  select column,column
  from table1 , table 2 
  where table1.컬럼(+)=table2.컬럼	
   						  
  select column,column
  from table1 
  left outer join table2 on 컬럼=컬럼  	
  ```

- (+) outer join 기호는 데이터가 없는 측에 명시 

- 40번 부서 정보는 부서 테이블에 존재 , 40번 부서에 속한 사원이 없으므로 사원테이블에 outer join 연산기호를 표시 

- outer join을 실행한 결과를 보면 사원이 존재하지 않는 40번 부서 정보까지 모두 조회가 된다 

- ```sql
  select e.empno,e.ename,e.deptno,d.deptno,d.dname,d.loc
  from dept d, emp e 
  where d.deptno=e.deptno(+)
  ```

  ![image-20211025201732079](C:\Users\MIN\TIL\SQL\KOSTA_1025.assets\image-20211025201732079.png)



## 3. Self JOIN

- **동일 테이블 상**에서의 조인
- 동일한 테이블이지만 **개념적으로 다른 정보**를 결합 
  - 사원 테이블의 매니저 컬럼의 정보는 또 다른 사원 정보이다. 이를 이용해 사원의 매니저의 사원번호, 사원명 등을 조회할 때 Self JOIN 을 사용

