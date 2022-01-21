- 관계형 데이터베이스: 어떻게 데이터를 저장할지 초점이 맞춰진 기술
- 객체지향 프로그래밍 언어: 메세지를 기반으로 기능과 속성을 한 곳에서 관리하는 기술

:point_right:웹 애플리케이션 개발이 데이터베이스 모델링에만 집중하게 됨

- JPA : 문제점을 해결하기 위해 등장
  - 서로 지향하는 바가 다른 2개 영역을 **중간에서 패러다임 일치 시켜줌**
  - 개발자: 객체지향적으로 프로그래밍
  - JPA: 관계형 데이터베이스에 맞게 SQL을 대신 생성해서 실행

## Spring Data JPA

```
JPA<- Hibernate <- Spring Data JPA
```

- Hibernate를 쓰는 것과 Spring Data JPA를 쓰는 것 사이에는 큰 차이 없음
- Spring에서는 Spring Data JPA 쓰는 것 권장
  - **구현체 교체의 용이성**
    - Hibernate 외에 다른 구현체로 쉽게 교체 가능
  - **저장소 교체의 용이성**
    - 관계형 데이터베이스 외에 다른 저장소로 쉽게 교체하기 위함
    - Spring Data의 하위 프로젝트들은 공통적인 인터페이스를 갖고 있음

```java
package com.example.springboot4aws.domain.posts;

import lombok.Builder;
import lombok.Getter;
import lombok.NoArgsConstructor;

import javax.persistence.*;

@Getter
@NoArgsConstructor //기본 생성자 자동 추가 , public Posts(){}와 같은 효과
@Entity //JPA 어노테이션
public class Posts {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(length = 500, nullable = false)
    private String title;

    @Column(columnDefinition = "TEXT",nullable = false)
    private String content;

    private String author;

    @Builder// 해당 클래스의 빌더 패턴 클래스 생성, 생성자 상단에 선언 시 생성자에 포함된 필드만 빌더에 포함
    public Posts(String title, String content, String author){
        this.title = title;
        this.content = content;
        this.author = author;
    }
}
```

- **Setter 메서드 없음**

  - getter/setter 를 무작정 생성하는 경우 :point_right: 해당 클래스의 인스턴스 값들이 언제 어디서 변해야 하는지 코드상으로 명확하게 구분할 수 없어 차후 기능 변경 시 복잡해짐
  - Entity 클래스에서는 절대 Setter 메서드를 만들지 않음
  - 해당 필드의 값 변경이 필요하면 명확히 그 목적과 의도를 나타낼 수 있는 메서드를 추가해야 함

  **:thinking:Setter가 없으면 어떻게 값을 채워 DB에 삽입하나?**

  - 기본적인 구조는 **생성자를 통해 최종값을 채운 후 DB에 삽입**
  - 값 변경이 필요한 경우 **해당 이벤트에 맞는 public 메서드를 호출**하여 변경하는 것을 전제로 함
  - 여기서는 `@Builder`를 통해 제공되는 빌더 클래스 사용
    - `@Builder` 사용 시 **어느 필드에 어떤 값을 채워야 할 지** 명확하게 인지 할 수 있음
  
- **DAO**

  - ibatis나 MyBatis 등에서 DAO라고 불리는 DBLayer 접근자

- JPA에서는 **Repository**라고 부르며 **인터페이스로 생성**

  - 인터페이스 생성 후 JpaRepository<Entity 클래스, PK타입> 을 상속하면 기본적인 CRUD 메소드가 자동으로 생성됨
  - `@Repository` 추가할 필요 없음
  - Entity 클래스는 기본 Repository 없이는 제대로 역할 할 수 없음
  - 도메인 패키지에서 함께 관리