# maven과 gradle의 차이점 비교해보기

1. ## 빌드 관리 도구

   - 빌드 자동화 도구

     - java 코드를 포함해 각종 xml ,properties, jar 파일들을 JVM이나 WAS가 인식할 수 있도록 패키징 해주는 빌드 과정

   - 프로젝트 생성, 테스트 빌드, 배포 등의 작업을 위한 전용 프로그램

   - 대규모 프로젝트에선 빌드프로세스를 수동으로 호출이 실용적이지 않음

     - 무엇을 빌드할지, 어떤 순서로 할지, 어떤 의존성이 있는지 모두 추적하기 쉽지 않기 때문

       :point_right: 빌드도구를 사용하면 **무엇을 빌드할지, 어떤 순서로 할지, 어떤 의존성이 있는지 모두 추적하는 것을 일관되게 할 수 있음**



2. ## Maven

   - Maven은 java용 프로젝트 관리 도구
   - 아파치의 ant 대안으로 만들어짐
     - 톰캣처럼 jakarta 프로젝트의 일환으로 만들어진 산출물로 C에서 말하는 make파일과 같은 java 프로그램용 build
     - OS와 상관없이 사용
     - configuration 파일이 xml로 되어 있어 애플리케이션 구조에 맞게 적용하기에 편리하게 되어 있음
   - 빌드 중인 프로젝트, 빌드 순서, 다양한 외부 라이브러리 종속성 관계를 `pom.xml`파일에 명시
   - Maven은 **외부저장소에서 필요한 라이브러리와 플러그인들을 다운로드** 한 다음, **로컬시스템의 캐시에 모두 저장**



3. ## Gradle

   -  Apacahe Maven과 Apache Ant에서 볼수 있는 개념들을 사용하는 대안으로써 나온 **프로젝트 빌드 관리 툴**
   - Groovy 언어를 사용한 Domain-specific-language를 사용
   - 2007년에 처음 개발됨
   - 2013년에 구글에 의해 안드로이드 프로젝트의 빌드 시스템으로 채택
   - 꽤 큰규모로 예상되는 multi-project 빌드를 도울 수 있도록 디자인됨
   - 빌드에 점진적으로 추가할 수 있음
   - 업데이트가 이미 반영된 빌드의 부분은 즉 더이상 재실행되지 않음

   

4. ## 차이점

   - #### 근본적인 차이점

     - Gradle: **작업 의존성 그래프 기반**
     - Maven: **고정적이고 선형적인 단계의 모델 기반**

   - #### Gradle

     - 어떤 task가 업데이트되었고 안되었는지 체크

       **:point_right:incremental build 허용**

     - 이미 업데이트된 테스크에 대해서는 작업이 실행되지 않음

       :point_right:빌드 시간 단축

     - 빌드 설정 규모가 커질수록 Maven과 비교하여 격차 벌어 질 수 있음

     - **concurrent에 안전한 캐시**를 허용

       :point_right:2개 이상의 프로젝트에서 동일한 캐시를 사용할 경우, 서로 overwrite되지 않도록 **checksum 기반의 캐시를 사용**하고, **캐시를 repository와 동기화**

     - 고도로 사용자 정의된 빌드를 작성하기 위해서는 **커스터마이징이** 간편한 Gradle을 사용하는게 훨씬 나음

   - #### 특정 설정을 다른 모듈에서 사용 시

     - Gradle: 설정 주입
     - Maven: 상속 받음

참고글: https://jisooo.tistory.com/entry/Spring-%EB%B9%8C%EB%93%9C-%EA%B4%80%EB%A6%AC-%EB%8F%84%EA%B5%AC-Maven%EA%B3%BC-Gradle-%EB%B9%84%EA%B5%90%ED%95%98%EA%B8%B0

https://wangmin.tistory.com/50