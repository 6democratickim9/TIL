# AWS Elastic Beanstalk? :thinking:

> Java, .NET, PHP, Node.js, Python, Ruby, Go, Docker를 사용하여 **Apache, Nginx, Passenger, IIS와 같은 친숙한 서버에서 개발된 웹 애플리케이션 및 서비스를 간편하게 배포하고 조정**할 수 있는 서비스

## 장점 

1. 빠르고 간편한 시작
   - AWS에 애플리케이션을 배포하는 가장 빠르면서 간편한 방법
   - AWS Management Console, Git 리포지토리 또는 Eclipse나 Visual Studio와 같은 IDE(통합 개발 환경)를 통해 애플리케이션을 업**로드하기만 하면 Elastic Beanstalk가 용량 프로비저닝, 로드 밸런싱, Auto Scaling, 애플리케이션 상태 모니터링에 대한 배포 정보를 자동으로 처리**
2. 개발자 생산성
   - 사용자 대신 인프라를 **프로비저닝하고 운영할 뿐만 아니라 애플리케이션 스택(플랫폼)을 관리**
   - 사용자는 시간을 따로 들이거나 익숙해지기 위해 애쓸 필요가 없음
   - 애플리케이션이 실행되는 **기본 플랫폼을 최신 패치와 업데이트**를 통해 **최신 상태로 유지**

3. 적절한 규모 유지
   - 손쉽게 조정할 수 있는 **Auto Scaling 설정**을 사용
   - Elastic Beanstalk를 사용하면 애**플리케이션에서 비용을 최소화하면서 높은 워크로드나 트래픽을 처리**
4. 완벽한 리소스 제어
   - 인스턴스 유형 및 워크로드를 실행할 프로세서 유형과 같이 **애플리케이션에 가장 적합한 AWS 리소스를 자유롭게 선택**
   - 애플리케이션을 실행하는 **AWS 리소스를 완벽하게 제어**

## 기능

- Elastic Beanstalk은 40개 이상의 핵심 지표 및 속성을 수집하여 애플리케이션의 상태를 판단
- Amazon CloudWatch 및 AWS X-Ray와 Elastic Beanstalk의 통합으로 모니터링 대시보드 사용
- 지표가 설정된 임계값을 초과할 때 알림을 수신하도록 CloudWatch 경보를 설정
- Elastic Beanstalk은 Elastic Load Balancing 및 Auto Scaling을 사용하여 **애플리케이션의 특정 요구사항에 따라 애플리케이션을 자동으로 확장 및 축소**
- Elastic Beanstalk을 통해 **스팟 인스턴스를 포함하여 Amazon EC2 인스턴스 유형 등 애플리케이션에 가장 적합한 AWS 리소스를 자유롭게 선택**
- ISO, PCI, SOC 1, SOC 2 및 SOC 3 규정 준수 기준 및 HIPAA 적격 기준에 부합합니다. 즉, Elastic Beanstalk에서 실행되는 애플리케이션은 규제되는 **재무 데이터 또는 PHI(보호 대상 건강 정보) 처리 가능**