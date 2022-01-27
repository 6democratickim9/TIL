```java
package com.example.springboot4aws.web.dto;

import com.example.springboot4aws.domain.posts.Posts;
import lombok.Builder;
import lombok.Getter;
import lombok.NoArgsConstructor;

@Getter
@NoArgsConstructor
public class PostsSaveRequestDto {
    private String title;
    private String content;
    private String author;

    @Builder
    public PostsSaveRequestDto(String title, String content,String author){
        this.title = title;
        this.content = content;
        this.author = author;
    }
    public Posts toEntity(){
        return Posts.builder()
                .title(title)
                .content(content)
                .author(author)
                .build();
    }

}

```

- Entity 클래스와 거의 유사한 형태임에도 DTO 클래스 새로 생성

- 절대로 Entity 클래스를 Request/Response 클래스로 사용해서는 안됨

- Entity 클래스는 **데이터베이스와 맞닿은 핵심 클래스**

- Entity 클래스를 기준으로 **테이블 생성되고 스키마 변경됨**

- Request 와 Response용 DTO는 View를 위한 클래스 -> 자주 변경됨

- View Layer와  DB Layer의 역할 분리를 철저하게 하는 것이 좋음

  - 실제로 Controller에서 결괏값으로 여러 테이블을 조인해서 줘야 할 경우가 빈번함

    :point_right: Entity 클래스만으로 표현하기 어려운 경우 많음

- 꼭 Entity 클래스와 Controller 에서 쓸 DTO는 분리해서 사용해야 함