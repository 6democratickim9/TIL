##### 3 / 65



개발자는 Amazon DynamoDB 테이블과 상호 작용하는 AWS Lambda 함수로 Amazon API Gateway REST API 백엔드를 사용하여 애플리케이션을 구축하고 있습니다. 테스트하는 동안 개발자는 API에 요청할 때 높은 대기 시간을 관찰합니다.

개발자는 종단 간 대기 시간을 어떻게 평가하고 성능 병목 현상을 식별할 수 있습니까?

> API Gateway 및 Lambda 함수에서 AWS X-Ray 추적을 활성화하고 구성합니다. X-Ray를 사용하여 사용자 요청을 추적하고 분석합니다.

##### 5 / 65



Amazon EC2 인스턴스에서 실행되는 애플리케이션은 AWS KMS 암호화 키(SSE-KMS)를 사용하는 서버 측 암호화를 사용하여 암호화된 Amaon S3 버스킷 내의 객체에 액세스해야 합니다 . 애플리케이션은 **객체를 해독하기 위해 고객 마스터 키(CMK)에 액세스**할 수 있어야 합니다.

애플리케이션 액세스 권한을 부여하는 단계 조합은 무엇입니까? (2개를 선택하십시오.)

> 애플리케이션의 EC2 인스턴스에 연결된 **IAM EC2 역할의 키에 대한 액세스 권한을 부여**합니다.

> IAM 정책이 **키에 대한 액세스 권한을 부여할 수 있도록 하는 키 정책을 작성**합니다.

- IAM role needs access to the keys to decrypt the object and key policies must allow role access to the key. Key policies are the primary way to control access to customer master keys (CMKs) in AWS KMS. You need the permission to decrypt the AWS KMS key. When a user sends a GET request, Amazon S3 checks if the AWS Identity and Access Management (IAM) user or role that sent the request is authorized to decrypt the key associated with the object. If the IAM user or role belongs to the same AWS account as the key, then the permission to decrypt must be granted on the AWS KMS key’s policy. Even if the user has permission to decrypt the key in their IAM policy, the user still needs the permission on the key policy for the download to work.

:star::star::star:

##### 17 / 65



한 개발자가 매우 민감한 데이터가 포함된 10MB 문서를 처리하는 응용 프로그램에서 작업하고 있습니다. 애플리케이션은 **AWS KMS를 사용하여 클라이언트 측 암호화를 수행**합니다.

어떤 단계를 따라야 합니까?

> GenerateDataKey API를 호출하여 **데이터 암호화 키의 일반 텍스트 버전을 검색**하여 데이터를 암호화합니다.

- Use the following pattern to encrypt data locally in your application: 
  1. Use the `GenerateDataKey` operation to get a data encryption key. 
  2.  Use the **plaintext data key (returned in the Plaintext field of the response) to encrypt data locally**, then erase the **plaintext data key from memory.** 
  3.  Store the encrypted data key (returned in the CiphertextBlob field of the response) alongside the locally encrypted data.

:star::star::star:

##### 18 / 65



회사는 거래 요청을 처리하는 데 밀리초 미만의 대기 시간이 필요한 주식 거래 애플리케이션을 구축하고 있습니다. Amazon DynamoDB는 각 요청을 처리하는 데 사용되는 모든 거래 데이터를 저장하는 데 사용됩니다. 애플리케이션을 로드 테스트한 후 개발 팀은 데이터 검색 시간으로 인해 대기 시간 요구 사항이 충족되지 않음을 발견했습니다. **요청 수가 갑자기 급증**하기 때문에 제한을 피하기 위해 **DynamoDB 읽기 용량을 상당히 과도하게 프로비저닝**해야 합니다.

**대기 시간 요구 사항을 충족하고 애플리케이션 실행 비용을 줄이려면 어떤 조치를 취해야 합니까?**

> **DynamoDB Accelerator를 사용하여 거래 데이터를 캐시합니다.**



##### 19 / 65



회사에서 기존 3계층 **웹 애플리케이션을 컨테이너화 하여 Amazon ECS Fargate에 배포**하려고 합니다. 애플리케이션이 **세션 데이터를 사용하여 사용자 활동을 추적**하고 있습니다.

어떤 접근 방식이 최고의 사용자 경험을 제공할까요?

> Amazon ElastiCache에서 Redis 클러스터를 프로비저닝하고 클러스터에 세션 데이터를 저장합니다

- examtopics 에서는 위의 대답에 힘이실려있음
- 결론: 내가 맞았다!



##### 21 / 65



응용 프로그램은 많은 수의 작은 메시지를 수집하여 데이터베이스에 저장합니다. 애플리케이션은 AWS Lambda를 사용합니다. 개발 팀이 애플리케이션 처리 로직을 변경하고 있습니다. 테스트에서 **각 메시지를 처리하는 데 15분 이상 걸립니다**. 팀은 현재 백엔드가 **시간 초과**될 수 있다고 우려하고 있습니다.

각 메시지가 **가장 확장 가능한 방식으로 처리**되도록 하려면 백엔드 시스템에서 어떤 변경을 해야 합니까?

> Amazon SQS **대기열에 메시지를 추가**합니다. **Auto Scaling 그룹**에서 **Amazon EC2 인스턴스를 설정하여 대기열을 폴링하고 메시지가 도착하면 처리**합니다.



##### 28 / 65



개발자는 AWS CodeDeploy를 사용하여 Amazon EC2에서 실행되는 애플리케이션을 배포하고 있습니다. 개발자가 특정 **배포 파일에 대한 파일 권한을 변경**하려고 합니다.

개발자는 이 요구 사항을 충족하기 위해 어떤 수명 주기 이벤트를 사용해야 합니까?

> **AfterInstall**

- A. AfterInstall: You can use the AfterInstall deployment lifecycle event for tasks such as **configuring your application or changing file permissions.** 
- B. DownloadBundle: During this deployment lifecycle event, the agent copies the revision files to a temporary location on the instance. This deployment lifecycle event is r**eserved for the agent and cannot be used to run user scripts.** 
- C. BeforeInstall: You can use the BeforeInstall deployment lifecycle event for **preinstall tasks** such as decrypting files and creating a backup of the current version. 
- D. ValidateService: ValidateService is the **last deployment lifecycle event** and is an opportunity to verify that the **deployment completed successfully.**



##### 29 / 65



사진 공유 웹 사이트는 매주 수백만 개의 새로운 이미지를 얻습니다. 이미지는 형식이 지정된 날짜 접두사로 Amazon S3에 저장됩니다. 개발자는 분석 및 추가 처리를 위해 몇 개의 S3 버킷으로 이미지를 이동하려고 합니다. 이미지는 실시간으로 이동할 필요가 없습니다.

이 작업을 수행하는 가장 효율적인 방법은 무엇입니까?

> Amazon EC2를 사용하여 **여러 날의 이미지를 일괄적으로 가져와 다른 버킷에 복사**



##### 30 / 65



회사는 지속적 통합 및 지속적 전달 시스템을 사용하고 있습니다. 이제 개발자는 **Amazon EC2 인스턴스와 온프레미스에서 실행되는 가상 서버 모두**에 소프트웨어 패키지 배포를 자동화해야 합니다.

이를 위해 어떤 AWS 서비스를 사용해야 합니까?

> **AWS CodeDeploy**



##### 36 / 65



기상 시스템은 600개의 온도 게이지를 모니터링하여 1분마다 온도 샘플을 수집하고 각 샘플을 DynamoDB 테이블에 저장합니다. 각 샘플에는 1K의 데이터 쓰기가 포함되며 쓰기는 시간이 지남에 따라 고르게 분포됩니다.

대상 테이블에 필요한 쓰기 처리량은 얼마입니까

> 10 용량 읽기 단위

- 600 writes per minute, evenly spread 
- 600/60(minute) = 10 writes per second 
- size = 1k, needs 1 WCU per write then 
- WCU = 600/60 = 10



##### 42 / 65



개발자는 **새 사용자가 새 사용자 계정을 등록하고 만들 수 있도록** 하는 응용 프로그램을 빌드하려고 합니다. 또한 애플리케이션은 **소셜 미디어 계정이 있는 사용자가 소셜 미디어 자격 증명을 사용하여 로그인**할 수 있도록 허용해야 합니다.

이러한 요구 사항을 충족하기 위해 어떤 AWS 서비스 또는 기능을 사용할 수 있습니까?

> Amazon Cognito 사용자 풀

- User pools are for authentication (identify verification). With a user pool, your app users can sign in through the user pool or federate through a third-party identity provider (IdP). Identity pools are for authorization (access control). You can use identity pools to create unique identities for users and give them access to other AWS services.



##### 45 / 65



AWS Elastic Beanstalk의 다중 컨테이너 Docker 환경에서 환경의 컨테이너 인스턴스를 구성하려면 무엇이 필요합니까?

> Amazon ECS 작업 정의

- Amazon ECS Task Definition – Elastic Beanstalk uses the Dockerrun.aws.json file in your project to generate the Amazon ECS task definition that is used to configure container instances in the environment. 



##### 47 / 65



개발자는 저장 시 암호화가 필요한 민감한 문서를 Amazon S3에 저장하고 있습니다. 암호화 키는 최소한 매년 교체되어야 합니다.

이것을 달성하는 가장 쉬운 방법은 무엇입니까?

- 내가 선택한 답은 Import a custom key into AWS KMS with annual rotation enabled 였는데, import가 활성화로 번역되어있어서...C 비슷한거 아닌가 했다..ㅎㅎ아니넹

>  Use AWS KMS with automatic key rotation

- ou can choose to have AWS KMS automatically rotate CMKs every year, provided that those keys were generated within AWS KMS HSMs. Automatic key rotation is not supported for imported keys, asymmetric keys, or keys generated in an AWS CloudHSM cluster using the AWS KMS custom key store feature. If you choose to import keys to AWS KMS or asymmetric keys or use a custom key store, you can manually rotate them by creating a new CMK and mapping an existing key alias from the old CMK to the new CMK.



##### 48 / 65



공급업체는 고객이 주문 상태를 쿼리할 수 있는 새로운 RESTful API를 작성하고 있습니다. 고객은 다음 API 엔드포인트를 요청했습니다.

http://www.supplierdomain.com/status/customerID

다음 애플리케이션 디자인 중 요구 사항을 충족하는 것은 무엇입니까? (2개를 선택하세요.)

> Amazon API Gateway; AWS Lambda

> Elastic Load Balancing; Amazon EC2

- examtopics에서 답이 `Elastic Load Balancing; Amazon EC2`에 좀 더 힘이 실림
- 결론: 내가 맞았다!



##### 51 / 65



개발자는 AWS Elastic Beanstalk에서 실행할 Linux 기반 애플리케이션을 작성하고 있습니다. 애플리케이션 요구 사항에는 애플리케이션이 **비용을 최소화**하면서 업데이트 중에 전체 용량을 유지해야 한다고 명시되어 있습니다.

개발자는 환경에 대해 어떤 유형의 Elastic Beanstalk 배포 정책을 지정해야 합니까?

> Rolling with additional batch

-  Immutable (blue/green) no downtime but requires 2 fully functional stacks = higher cost. 
- Rolling with batch, no downtime or reduction in cost, **takes longer then immutable but the benefit is a cost saving**



##### 54 / 65



대기업에는 여러 AWS 계정에 **분산된 애플리케이션 구성 요소**가 있습니다. 회사는 이러한 계정에서 **추적 데이터를 수집하고 시각화**해야 합니다.

이러한 요구 사항을 충족하려면 무엇을 사용해야 합니까?

> AWS X-Ray



##### 55 / 65



개발자는 Amazon S3에 데이터를 업로드하려고 하며 전송 중인 데이터를 암호화해야 합니다.

다음 중 이 작업을 수행할 솔루션은 무엇입니까? (2개를 선택하세요.)

> AWS KMS 관리형 고객 마스터 키로 **클라이언트 측 암호화 설정**

> SSL 연결을 통해 데이터 전송



##### 57 / 65



개발자는 주간 뉴스레터를 동적으로 생성하여 100,000명의 사용자에게 보내는 AWS Lambda 함수를 구축하고 있습니다. 이 뉴스레터에는 정적 텍스트와 이미지가 모두 포함되어 있습니다. 개발자는 뉴스레터에 **하이퍼링크될 이미지를 저장할 수 있는 빠르고 확장성이 뛰어난 장소**가 필요합니다.

개발자는 이 이미지를 어디에 저장해야 합니까?

> TTL(Time-to-Live)이 높은 **Amazon S3 지원 Amazon CloudFront 배포를 사용**하여 캐싱을 최대화합니다.

- 이것 또한 examtopics에서 조금 더 힘이 실렸기에 얘로 정답 채택
- 결론: 얘두 내가 맞았다!!



##### 62 / 65



한 회사는 릴리스 파이프라인을 자동화하기 위해 AWS CodePipeline을 구현했습니다. 개발 팀은 단계에 있는 각 작업의 상태 변경에 대한 알림을 보낼 AWS Lambda 함수를 작성하고 있습니다.

Lambda 함수를 이벤트 소스와 연결하려면 어떤 단계를 수행해야 합니까?

> **CodePipeline을 이벤트 소스로 사용**하는 **Amazon CloudWatch Events 규칙을 생성**합니다.

- To configure AWS CodePipeline as an event source: Create an Amazon CloudWatch Events rule that uses CodePipeline as an event source. Create a target for your rule that uses one of the services available as targets in Amazon CloudWatch Events, such as AWS Lambda or Amazon SNS. Grant permissions to Amazon CloudWatch Events to allow it to invoke the selected target service.

--------

##### 11 / 65



전자 상거래 사이트에서는 재방문 사용자가 로그인하여 사용자 정의된 웹 페이지를 표시할 수 있습니다. 워크플로는 아래 이미지에 나와 있습니다.

1. User logs in

   - display user login page

   - authenticate and authorize user access

     ```
     ↓ user login data
     ```

2. Database queried for user

   - create query for user table

   - query user table for account & preferences

     ```
     ↓ user account data
     ```

3. Display customized entry page.

애플리케이션이 EC2 인스턴스에서 실행 중입니다. Amazon RDS는 사용자 계정 및 기본 설정을 저장하는 데이터베이스에 사용됩니다. 로그인 단계가 완료될 때까지 기다리는 동안 웹 사이트가 멈추거나 로드 속도가 느립니다. 사이트의 나머지 구성 요소는 잘 최적화되어 있습니다.

다음 기술 중 이 문제를 해결할 수 있는 방법은 무엇입니까? (2개를 선택합니다.)

>MemCached용 Amazon ElastiCache를 사용하여 사용자 데이터를 캐시합니다.

> 코드가 계속 실행될 수 있도록 데이터베이스를 비동기적으로 호출합니다.



##### 24 / 65



개발자가 여러 AWS 서비스를 사용하여 서버리스 애플리케이션을 작성했습니다. 비즈니스 로직은 타사 라이브러리에 종속된 Lambda 함수로 작성됩니다. Lambda 함수 엔드포인트는 Amazon API Gateway를 사용하여 노출됩니다. Lambda 함수는 Amazon DynamoDB에 정보를 씁니다.

개발자는 애플리케이션을 배포할 준비가 되었지만 롤백할 수 있는 능력이 있어야 합니다. 이러한 요구 사항을 기반으로 이 배포를 어떻게 자동화할 수 있습니까?

> AWS CloudFormation 템플릿의 서버리스 애플리케이션 모델을 준수하는 구문을 사용하여 Lambda 함수 리소스를 정의합니다.

- Sam will use Codedeploy to to build Serverless applications. You can create a SAM template (YAML) with the desired configuration and SAM will go through the steps to set the infrastructure.



##### 27 / 65



애플리케이션은 S3 버킷에 이미지를 저장합니다. Amazon S3 이벤트 알림은 이미지 크기를 조정하는 Lambda 함수를 트리거하는 데 사용됩니다. 각 이미지를 처리하는 데 1초도 채 걸리지 않습니다.

AWS Lambda는 추가 트래픽을 어떻게 처리합니까?

> Lambda는 요청을 동시에 실행하도록 확장됩니다.



##### 31 / 65



회사가 모놀리식 아키텍처에서 마이크로서비스 기반 아키텍처로 마이그레이션하고 있습니다. 개발자는 많은 마이크로서비스가 성능에 영향을 주지 않고 서로 비동기식으로 통신할 수 있도록 애플리케이션을 리팩토링해야 합니다.

어떤 관리형 AWS 서비스를 사용하면 비동기식 메시지 전달이 가능합니까? (2개를 선택하세요.)

> Amazon SQS

> Amazon SNS



##### 35 / 65



개발자는 10분마다 AWS Lambda 함수를 호출해야 하는 서버리스 애플리케이션을 작성하고 있습니다.

기능을 트리거하는 자동화된 서버리스 방법은 무엇입니까?

> 정기적인 일정에 따라 Lambda 함수를 호출하는 Amazon CloudWatch Events 규칙을 생성합니다.





##### 38 / 65



개발 팀은 다단계 인증이 필요한 모바일 앱을 설계하고 있습니다.

이를 달성하기 위해 어떤 조치를 취해야 합니까? (2개를 선택하세요.)

> Amazon Cognito를 사용하여 사용자 풀을 생성하고 사용자 풀에 사용자를 생성합니다.

> Amazon Cognito 사용자 풀에 대해 다단계 인증을 활성화합니다.



##### 40 / 65



개발자는 애플리케이션 로드 밸런서(ALB) 뒤에서 실행되는 애플리케이션을 구축하고 있습니다. 애플리케이션은 Amazon CloudFront 배포의 오리진으로 구성됩니다. 사용자는 소셜 미디어 계정을 사용하여 애플리케이션에 로그인합니다.

개발자는 어떻게 사용자를 인증하고 권한을 부여할 수 있습니까?

> Amazon Cognito를 인증 공급자 중 하나로 사용하도록 Cloudfront 구성



##### 44 / 65



get_store라는 핸들러 함수와 다음 AWS CloudFormation 템플릿이 포함된 로컬 store.py의 AWS Lambda 함수에 대한 소스 코드가 주어지면,

```
Transform: AWS::Serverless-2016-10-31
Resources:
    StoreFunc:
        Type: AWS::Serverless::Function
        Properties:
            Handler: store.get_store
            Runtime: python3.6
```

AWS CLI 명령 aws cloudformation deploy를 사용하여 배포할 수 있도록 템플릿을 준비하려면 어떻게 해야 합니까?

> aws cloudformation 패키지를 사용하여 소스 코드를 Amazon S3 버킷에 업로드하고 수정된 CloudFormation 템플릿을 생성합니다.



##### 45 / 65



개발자는 Amazon API Gateway와 AWS Lambda 함수를 통합하는 애플리케이션을 구축하고 있습니다. API를 호출할 때 개발자는 다음 오류를 수신합니다.

```
Wed Nov 08 01:13:00 UTC 2017 : Method completed with status: 502
```

오류를 해결하려면 개발자가 어떻게 해야 합니까?

> API 호출에 대한 Lambda 함수 응답 형식 변경



##### 47 / 65



개발 팀은 현재 인메모리 저장소를 사용하여 누적된 게임 결과를 저장하는 응용 프로그램을 지원합니다. 개별 결과는 데이터베이스에 저장됩니다. AWS로 마이그레이션하는 과정에서 팀은 자동 조정을 사용해야 합니다. 팀은 이것이 일관성 없는 결과를 초래할 것임을 알고 있습니다.

팀은 성능에 영향을 미치지 않고 일관된 결과를 얻을 수 있도록 이러한 누적 게임 결과를 어디에 저장해야 합니까?

> Amazon ElastiCache



##### 55 / 65



개발 팀은 사용자가 Amazon S3에 사진을 업로드할 수 있는 모바일 앱을 개발 중입니다. 팀은 단일 이벤트 동안 수십만 명의 사용자가 앱을 동시에 사용할 것으로 예상합니다. 사진이 업로드되면 백엔드 서비스는 부적절한 콘텐츠가 있는지 사진을 스캔하고 구문 분석합니다.

백엔드 서비스에 대한 일시적인 볼륨 급증을 완화하는 이 목표를 달성하기 위한 가장 탄력적인 방법은 무엇입니까?

> 사진이 Amazon S3에 업로드되면 이벤트를 Amazon SQS 대기열에 게시합니다. 대기열을 이벤트 소스로 사용하여 AWS Lambda 함수를 트리거합니다. Lambda 함수에서 사진을 스캔하고 구문 분석합니다.



##### 56 / 65



IAM 역할은 모든 Amazon S3 API 작업에 대한 액세스를 명시적으로 거부하는 Amazon EC2 인스턴스에 연결됩니다. EC2 인스턴스 자격 증명 파일은 전체 관리 액세스를 허용하는 IAM 액세스 키와 보안 액세스 키를 지정합니다.

이 EC2 인스턴스에 대해 여러 IAM 액세스 모드가 있는 경우 다음 중 올바른 것은 무엇입니까?

> EC2 인스턴스는 모든 S3 버킷에서 모든 작업을 수행할 수 있습니다.

- C ---> Credentials have a higher precedence than role credentials



##### 61 / 65



애플리케이션은 Amazon SQS를 사용하여 여러 독립 발신자의 메시지를 관리하도록 설계되었습니다. 각 발신인은 메시지를 받은 순서대로 처리해야 합니다.

개발자가 구현해야 하는 SQS 기능은 무엇입니까?

> 고유한 MessageGroupId로 각 발신자를 구성하십시오.



##### 62 / 65



개발자는 버킷에 새 객체가 생성될 때 Lambda 함수를 호출하는 이벤트 소스로 Amazon S3를 사용하고 있습니다. 이벤트 소스 매핑 정보는 버킷 알림 구성에 저장됩니다. 개발자는 다양한 버전의 Lambda 함수로 작업하고 있으며 Amazon S3가 올바른 버전을 호출하도록 알림 구성을 지속적으로 업데이트해야 합니다.

S3 이벤트와 Lambda 간의 매핑을 달성하는 가장 효율적이고 효과적인 방법은 무엇입니까?

> 다른 Lambda 트리거 사용



##### 63 / 65



한 회사는 AWS 서버리스 애플리케이션 모델(AWS SAM) CLI를 사용하여 배포될 AWS Lambda 함수를 사용하여 새로운 서버리스 애플리케이션을 개발했습니다 .

개발자는 애플리케이션을 배포하기 전에 어떤 단계를 완료해야 합니까?

> SAM 패키지를 사용하여 서버리스 애플리케이션 번들 구성



##### 64 / 65



개발 팀은 10명의 팀원으로 구성됩니다. 각 팀 구성원의 홈 디렉터리와 유사하게 관리자는 Amazon S3 버킷의 사용자별 폴더에 대한 액세스 권한을 부여하려고 합니다. 사용자 이름이 "TeamMemberX"인 팀 구성원의 경우 IAM 정책 스니펫은 다음과 같습니다.

```
{
  "sid": "AllowS3ActionToFolders",
  "Effect": "Allow",
  "Action": [ "S3:*" ],
  "Resource": [ "arn:aws:s3::companyname/home/TeamMemberX/*" ] 
}
```

각 팀 구성원에 대해 고유한 정책을 생성하는 대신 이 정책 스니펫을 모든 팀 구성원에게 일반화하는 데 사용할 수 있는 접근 방식은 무엇입니까?

> IAM 정책 변수 사용