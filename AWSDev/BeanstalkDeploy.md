- **한 번에 모두(All at once)** 

  - Blue/Green 배포 방식과 유사
  - 가장 빠른 배포 방법
  - 단기간의 **서비스 손실이 허용**될 수 있고 **빠른 배포가 중요한 경우에 적합**합니다. 
  - Elastic Beanstalk에서 각 인스턴스에 **새 애플리케이션 버전을 배포**합니다. 그런 다음 웹 프록시 또는 애플리케이션 서버를 다시 시작해야 할 수 있습니다. 결과적으로 짧은 시간 동안 사용자가 애플리케이션을 사용할 수 없거나 가용성이 감소할 수 있습니다.

  

- **롤링(Rolling)** 

  - **가동 중지를 방지하고 가용성 감소를 최소화**하는 대신 배포 시간이 길어짐
  - **완전한 서비스 손실이 *허용될 수 없는 경우***에 적합 
  - 이 방법을 사용하면 애플리케이션이 **한 번에 한 인스턴스 배치**로 사용자 환경에 배포
  - 배포 전반에 걸쳐 **대부분의 대역폭이 유지**됩니다.

  

- **추가 배치를 사용한 롤링(Rolling with additional batch)** 

  - **가용성 감소를 방지**하지만 배포 시간이 ***롤링* 방법보다도 오래 걸림**
  - 배포 전반에 걸쳐 동일한 **대역폭을 유지해야 하는 경우에 적합**합니다
  - 추가 인스턴스 배치를 시작한 다음 **롤링 배포를 수행**합니다. 추가 배치를 시작하는 데는 시간이 걸리며 **배포 전반에 걸쳐 동일한 대역폭이 유지**

  

- **변경 불가능(Immutable)** 

  - *기존 인스턴스를 업데이트*하는 대신 **새 애플리케이션 버전이 항상 새 인스턴스에 배포되도록 하는 더 느린 배포 방법**
  - 배포가 실패할 경우 **빠르고 안전하게 롤백할 수 있다는 추가 이점**
  - [변경 불가능한 업데이트](https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/environmentmgmt-updates-immutable.html)를 수행하여 애플리케이션을 배포
  - 변경이 불가능한 업데이트에서 두 번째 Auto Scaling 그룹이 사용자 환경에서 시작되고 **새 인스턴스가 상태 확인을 통과할 때까지 새 버전과 기존 버전이 함께 트래픽을 처리**합니다.

  

- **트래픽 분할(Traffic splitting)** 

  - **canary 테스트 배포 방법**
  - 이전 애플리케이션 버전을 통해 **나머지 트래픽을 계속 처리**하면서 수신 트래픽의 일부를 사용
  - 새 애플리케이션 **버전의 상태를 테스트**하려는 경우에 적합합니다.





|          배포 방법          |                                                              |                                                              |                    |                   |                                     |                              |
| :-------------------------: | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------- | :---------------- | :---------------------------------- | :--------------------------- |
|          **방법**           | **배포 실패로 인한 영향**                                    | **배포 시간**                                                | **가동 중지 없음** | **DNS 변경 없음** | **롤백 프로세스**                   | **코드 배포 위치**           |
|      **한 번에 모두**       | 가동 중지                                                    | ![img](https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/images/clock.png) | ☓아니요            | ✓예               | 수동 재배포                         | 기존 인스턴스                |
|          **롤링**           | 단일 배치가 서비스에서 제외됨. 실패하기 전 성공한 배치가 새 애플리케이션 버전 실행 | ![img](https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/images/clock.png) ![img](https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/images/clock.png) † | ✓예                | ✓예               | 수동 재배포                         | 기존 인스턴스                |
| **추가 배치를 사용한 롤링** | 첫 번째 배치가 실패할 경우 최소화. 그렇지 않은 경우 **롤링**과 유사함 | ![img](https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/images/clock.png) ![img](https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/images/clock.png) ![img](https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/images/clock.png) † | ✓예                | ✓예               | 수동 재배포                         | 새 인스턴스 및 기존 인스턴스 |
|       **변경 불가능**       | 최소화                                                       | ![img](https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/images/clock.png) ![img](https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/images/clock.png) ![img](https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/images/clock.png) ![img](https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/images/clock.png) | ✓예                | ✓예               | 새 인스턴스 종료                    | 새 인스턴스                  |
|       **트래픽 분할**       | 일시적으로 영향을 받는 새 버전으로 라우팅되는 클라이언트 트래픽의 비율 | ![img](https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/images/clock.png) ![img](https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/images/clock.png) ![img](https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/images/clock.png) ![img](https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/images/clock.png) †† | ✓예                | ✓예               | 트래픽 재라우팅 및 새 인스턴스 종료 | 새 인스턴스                  |
|        **블루/그린**        | 최소화                                                       | ![img](https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/images/clock.png) ![img](BeanstalkDeploy.assets/clock.png) ![img](https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/images/clock.png)![img](https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/images/clock.png) | ✓예                | ☓아니요           | Swap URL                            | 새 인스턴                    |