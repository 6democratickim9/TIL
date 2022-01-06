### MyBatis Framework

- Java Persistence Framework
- 영속성 계층 프레임워크
- 자바 어플리케이션과 데이터베이스 연동 시 반복적인 작업을 프레임워크 차원에서 지원하여 생산성이 향상



#### 컬럼명과 인스턴스변수명이 불일치할 때 방법

1. 아래와 같이 별칭을 인스턴스 변수명으로 주면 된다 
2. spring mybatis 연동 설정에 underscore 와 camelCase 를 자동 연결하도록 정의

```xml
<select id="findProductByNo" resultType="ProductVO" parameterType="int">
		select product_no as productNo,name,maker,price from spring_product where product_no=#{value}
```

- `MyBatis Framework` 를 사용해서 개발시에는 해당 클래스의 매개변수가 있는 생성자가 별도로 정의되어 있을 때는 반드시 **기본생성자(디폴트 생성자) 를 명시**해야 한다

```sql
DROP TABLE SPRING_PRODUCT;
DROP SEQUENCE SPRING_PRODUCT_SEQ;
CREATE TABLE spring_product(
	product_no NUMBER PRIMARY KEY,
	name VARCHAR2(100) NOT NULL,
	maker VARCHAR2(100) NOT NULL,
	price NUMBER NOT NULL
)
CREATE SEQUENCE spring_product_seq;

INSERT INTO spring_product VALUES(spring_product_seq.nextval,'아이폰9','애플',150);
INSERT INTO spring_product VALUES(spring_product_seq.nextval,'갤럭시8','삼성',100);
INSERT INTO spring_product VALUES(spring_product_seq.nextval,'아이폰7','애플',50);
INSERT INTO spring_product VALUES(spring_product_seq.nextval,'아이폰2','애플',10);
INSERT INTO spring_product VALUES(spring_product_seq.nextval,'갤럭시9','삼성',120);
COMMIT

SELECT COUNT(*) FROM SPRING_PRODUCT;

```

- `private int productNo; `
- 컬럼명은 `product_no` , 인스턴스 변수명과 컬럼명은 불일치

```java
ClassPathXmlApplicationContext ctx=new ClassPathXmlApplicationContext("spring-mybatis-config.xml");
		ProductMapper m=(ProductMapper) ctx.getBean("productMapper");
		
		//System.out.println("총상품수:"+m.getTotalProductCount());
		//maker 종류 리스트를 조회 
		/*
		 * List<String> makerList=m.getMakerKindList(); for(String maker:makerList) {
		 * System.out.println(maker); }
		 */
		/*
		ProductVO vo=m.findProductByNo(1);
		System.out.println("상품검색:"+vo);
		*/
		ProductVO paramVO=new ProductVO();
		paramVO.setMaker("애플");
		paramVO.setPrice(30);
		
		List<ProductVO> list=m.findProductListByMakerAndPrice(paramVO);
		for(ProductVO vo:list)
			System.out.println(vo);
		ctx.close();
```

- `ProductMapper m=(ProductMapper) ctx.getBean("productMapper");`
  - Mapper Proxy( Mapper Interface 의 구현체 ) 의 bean id는 **소문자로 시작하는 인터페이스명**이다 
- `paramVO.setPrice(30);`
  - 애플 maker의 price가 30을 초과하는 상품리스트를 `product_no desc` 내림차순으로 조회 









- `spring-mybatis-config.xml`

- ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <beans xmlns="http://www.springframework.org/schema/beans"
  	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  	xmlns:context="http://www.springframework.org/schema/context"
  	xmlns:mybatis-spring="http://mybatis.org/schema/mybatis-spring"
  	xsi:schemaLocation="http://mybatis.org/schema/mybatis-spring http://mybatis.org/schema/mybatis-spring-1.2.xsd
  		http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd
  		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.3.xsd">
  <!-- dbcp -->
  <bean id="dbcp" class="org.apache.commons.dbcp2.BasicDataSource">
  <property name="driverClassName" value="oracle.jdbc.OracleDriver"/>
  <property name="url" value="jdbc:oracle:thin:@127.0.0.1:1521:xe"/>
  <property name="username" value="scott"/>
  <property name="password" value="tiger"/>
  </bean>
  
  <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">
  <property name="dataSource" ref="dbcp"/>
  <property name="typeAliasesPackage" value="org.kosta.model"/>
  <property name="configuration">
  	<bean class="org.apache.ibatis.session.Configuration">
  		<property name="mapUnderscoreToCamelCase" value="true"/>
  	</bean>
  </property>
  </bean>
  <!-- 
  		SqlSessionTemplate : MyBatis 개발 생산성을 위해 사용하는 객체(bean or component)
  								 반복적인 작업을 Template에서 지원 ( openSession ~ close ) 
  								 AOP 기반 트랜잭션을 지원 ( 선언적 방식의 트랜잭션을 지원 ) -> 이후 공부예정
  								 영속성 계층 ( Persistence Layer ) 에서 DI 방식으로 사용할 bean  
   -->
  <bean id="sqlSessionTemplate" class="org.mybatis.spring.SqlSessionTemplate">
  <constructor-arg ref="sqlSessionFactory"/>
  </bean>
  <!-- 
  		MyBatis Proxy를 위한 설정 ( DAO(Mapper) interface 를 implements 한 구현 객체 - DAOImpl)
  	  	DAOImpl 구현체를 Framework 차원으로 자동 생성 - @Mapper 어노테이션을 영속성 계층 인터페이스에 명시 
  	  	org.kosta.model 이하의 @Mapper 가 명시된 인터페이스를 검색해 구현체를 생성한다 
   -->
  <mybatis-spring:scan base-package="org.kosta.model"/>
  
  <!--  Annotation 기반 IOC(DI,DL)을 위한 설정 -->
  <context:component-scan base-package="org.kosta"/>
  
  </beans>
  
  ```

  

- ### spring과 mybatis framework 연동설정

- ![image-20211124200009081](C:\Users\MIN\TIL\Spring\KOSTA_1124.assets\image-20211124200009081.png)

- `<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">`

  - `SqlSessionFactoryBean` : MyBatis 의 주요 객체인 **SqlSession을 생성하는 Factory 역할**을 하는 객체 

- `<property name="dataSource" ref="dbcp"/>`

  - `dataSource` : database connection pool 을 setting 	  

- `<property name="typeAliasesPackage" value="org.kosta.model"/>`

  - `typeAliasesPackage` : `mapper xml`에서 편리하게 **vo or dto 를 사용하기 위해 별칭을 지정** 
    	  						   **org.kosta.model 이하의 클래스명이 별칭**으로 된다 
    	  						   `resultType="org.kosta.model.AccountVO"`  -> `resultType="AccountVO"`

- `<property name="mapUnderscoreToCamelCase" value="true"/>`
  - db column name의 underscore와  application instance variable name의 camelcase를 자동으로 연결 
    				ex) 컬럼명: `product_id`   변수명: `productId` 이 자동 매핑 