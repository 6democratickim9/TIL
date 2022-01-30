##### 8.  봉투 암호화는 AWS KMS에서 어떻게 작동합니까?

> 고객 마스터 키는 데이터 키를 암호화/복호화하는 데 사용됩니다. 일반 텍스트 데이터 키는 고객 데이터를 암호화하는 데 사용됩니다.

>  The Customer Master Key is used to encrypt/decrypt a data key. The Plaintext Data Key is used to encrypt customer data.

- Envelope encryption When you encrypt your data, your data is protected, but you have to protect your encryption key. One strategy is to encrypt it. 
- Envelope encryption is the practice of encrypting **plaintext data with a data key, and then encrypting the data key under another key.** "



11. **Elastic Beanstalk는 어떤 AWS 제품과 기능을 배포할 수 있습니까? (3개를 선택하세요.)**

> Auto Scaling 그룹 / Elastic Load Balancer / RDS 인스턴스

- Beanstalk is an orchestration service offered by Amazon Web Services for **deploying applications which orchestrates various AWS services, including EC2, S3, Simple Notification Service (SNS), CloudWatch, autoscaling, and Elastic Load Balancers.**



12. **개발자가 회사 제품에 대해 Amazon API Gateway를 설정하고 있습니다. API는 등록된 개발자가 환경을 쿼리하고 업데이트하는 데 사용됩니다. 회사는 비용 및 보안상의 이유로 최종 사용자가 보낼 수 있는 요청의 양을 제한하려고 합니다. 경영진은 등록된 개발자에게 더 많은 요청을 허용하는 더 큰 패키지를 구매할 수 있는 옵션을 제공하고자 합니다.**

    개발자는 **최소한**의 오버헤드 관리로 어떻게 이를 달성할 수 있습니까?

    > 기본 사용 계획을 설정하고 속도 및 버스트 용량에 대한 값을 지정하고 이를 단계와 연결합니다. 등록된 사용자가 더 큰 패키지를 선택하는 경우 적절한 값으로 사용자 지정 계획을 만들고 해당 계획을 사용자와 연결합니다.

- After you create, test, and deploy your APIs, you can use API Gateway usage plans to make them available as product offerings for your customers. **You can configure usage plans and API keys to allow customers to access selected APIs at agreed-upon request rates and quotas that meet their business requirements and budget constraints**. If desired, you can set default method-level throttling limits for an API or set throttling limits for individual API methods.



35. **개발자가 웹 애플리케이션 백엔드용 Lambda 함수를 생성했습니다. AWS Lambda 콘솔에서 Lambda 함수를 테스트할 때 개발자는 함수가 실행되고 있는 것을 볼 수 있지만 몇 분이 지나도 Amazon CloudWatch Logs에 로그 데이터가 생성되지 않습니다.**

    **이 상황의 원인은 무엇입니까?**

> Lambda 함수의 실행 역할에 CloudWatch Logs에 로그 데이터를 쓸 수 있는 권한이 없습니다.

- A. The Lambda function does not have any explicit log statements for the log data to send it to CloudWatch Logs. -- If lambda was executed, it will always have some logs to send. For example execution time and memory usage will be always send after execution is done. [Incorrect] 
- B. The Lambda function is missing CloudWatch Logs as a source trigger to send log data. -- Lambda is connected to CloudWatch by default and you cannot disable it. [Incorrect] 
- C. **The execution role for the Lambda function is missing permissions to write log data to the CloudWatch Logs. -- You have to explicitly define a IAM role with IAM policy which allows Lambda to send logs to CloudWatch. [Correct]** 
- D. The Lambda function is missing a target CloudWatch Log group. -- See explanation in answer B. [Incorrect]



37. **개발자가 모놀리식 애플리케이션을 리팩토링하고 있습니다. 애플리케이션은 POST 요청을 받고 여러 작업을 수행합니다. 일부 작업은 병렬로 실행되고 다른 작업은 순차적으로 실행됩니다. 이러한 작업은 개별 AWS Lambda 함수로 리팩터링되었습니다. POST 요청은 Amazon API Gateway에서 처리됩니다.**

    **개발자는 API Gateway를 사용하여 동일한 순서로 Lambda 함수를 어떻게 호출해야 합니까?**

> AWS Step Functions 상태 머신을 사용하여 Lambda 함수 조정

- AWS Step Functions provides **serverless orchestration for modern applications.** Orchestration centrally manages a workflow by breaking it into multiple steps, adding flow logic, and tracking the inputs and outputs between the steps.



46. **한 회사는 직원이 개인 Amazon S3 버킷에 프로필 사진을 업로드할 수 있는 웹 애플리케이션을 개발하고 있습니다. 프로필 사진에는 크기 제한이 없으며 직원이 로그인할 때마다 표시되어야 합니다. 보안상의 이유로 사진은 공개적으로 액세스할 수 없습니다.**

    **이 시나리오에 대한 실행 가능한 장기 솔루션은 무엇입니까?**

    > 사진의 S3 키를 Amazon DynamoDB 테이블에 저장합니다. 함수를 사용하여 직원이 로그인할 때마다 미리 서명된 URL을 생성합니다. URL을 브라우저에 반환합니다.

- the object owner can **optionally share objects with others by creating a presigned URL,** using their own security credentials, to grant time-limited permission to download the objects



47. **다음 중 EC2 인스턴스에 배포된 애플리케이션이 DynamoDB 테이블에 데이터를 쓸 수 있도록 하려면 어떤 항목이 필요합니까?**

    **EC2 인스턴스에 저장할 수 있는 보안 키가 없다고 가정합니다. (2개를 선택하세요.)**

    > 실행 중인 EC2 인스턴스에 IAM 역할을 추가합니다.
    >
    > DynamoDB 테이블에 대한 쓰기 액세스를 허용하는 IAM 역할을 생성합니다.

- **outdated question.** The option B is now supported B. 
- **Add an IAM Role to a running EC2 instance D**. 
- Launch an EC2 Instance with the IAM Role included in the launch configuration. E. 
- **Create an IAM Role that allows write access to the DynamoDB table.**



59. **Amazon Linux EC2 인스턴스에서 실행되는 애플리케이션은 AWS 인프라를 관리해야 합니다.**

    **AWS API를 안전하게 호출하도록 EC2 인스턴스를 구성하려면 어떻게 해야 합니까?**

    > 필요한 권한이 있는 EC2 인스턴스의 역할을 지정합니다.

- "We designed IAM roles so that your **applications can securely make API requests from your instance**s, without requiring you to manage the security credentials that the applications use. "



---------------



5. **개발자가 모놀리식 애플리케이션을 리팩토링하고 있습니다. 애플리케이션은 POST 요청을 받고 여러 작업을 수행합니다. 일부 작업은 병렬로 실행되고 다른 작업은 순차적으로 실행됩니다. 이러한 작업은 개별 AWS Lambda 함수로 리팩터링되었습니다. POST 요청은 Amazon API Gateway에서 처리됩니다.**

   **개발자는 API Gateway를 사용하여 동일한 순서로 Lambda 함수를 어떻게 호출해야 합니까?**

> AWS Step Functions 상태 머신을 사용하여 Lambda 함수 조정

- AWS Step Functions provides serverless orchestration for modern applications. Orchestration centrally manages a workflow by breaking it into multiple steps, adding flow logic, and tracking the inputs and outputs between the steps.



8. **Amazon Linux EC2 인스턴스에서 실행되는 애플리케이션은 AWS 인프라를 관리해야 합니다.**

   **AWS API를 안전하게 호출하도록 EC2 인스턴스를 구성하려면 어떻게 해야 합니까?**

> 필요한 권한이 있는 EC2 인스턴스의 역할을 지정합니다.

- We designed IAM roles so that your applications can securely make API requests from your instances, without requiring you to manage the security credentials that the applications use. "



----



12. **AWS X-Ray로 Lambda 기반 애플리케이션을 추적하려면 무엇이 필요합니까?**

> IAM 실행 역할을 사용하여 Lambda 함수 권한을 부여하고 추적을 활성화합니다.

- Your function needs **permission to upload trace data to X-Ray**. 
- When you enable active tracing in the Lambda console, **Lambda adds the required permissions to your function's execution role**. Otherwise, **add the `AWSXRayDaemonWriteAccess` policy to the execution role**. 



28. **애플리케이션은 API를 통해 수신되는 수백만 개의 이벤트를 실시간으로 처리합니다.**

    **여러 소비자가 데이터를 동시에 가장 비용 효율적으로 처리할 수 있도록 하려면 어떤 서비스를 사용할 수 있습니까?**

    > Amazon Kinesis 스트림

- **We recommend Amazon Kinesis Data Streams** for use cases with requirements that are similar to the following: Ability for **multiple applications to consume the same stream concurrently.** For example, you have one application that updates a real-time dashboard and another that archives data to Amazon Redshift. You want both applications to consume data from the same stream concurrently and independently.



34. **애플리케이션 개발 팀은 AWS X-Ray를 사용하여 애플리케이션 코드를 모니터링하여 성능을 분석하고 근본 원인 분석을 수행하기로 결정했습니다.**

    **X-Ray 사용을 시작하려면 팀에서 무엇을 해야 합니까? (2개를 선택하세요.)**

    > AWS SDK를 사용하여 애플리케이션 코드를 계측합니다.
    >
    > 응용 프로그램 서버에 X-Ray 에이전트를 설치합니다

    

35. **개발자가 AWS CloudFormation을 사용하여 애플리케이션을 배포하는 템플릿을 생성하고 있습니다. 이 애플리케이션은 서버리스이며 Amazon API Gateway, Amazon DynamoDB 및 AWS Lambda를 사용합니다.**

    **개발자는 서버리스 리소스를 표현하기 위한 단순화된 구문을 정의하기 위해 어떤 도구를 사용해야 합니까?**

> AWS 서버리스 애플리케이션 모델

- The AWS Serverless Application Model(SAM) is an open-source framework for building serverless applications. It **provides shorthand syntax to express functions**, APIs, databases, and event source mappings. With just a few lines per resource, you can define the application you want and model it using YAML."



42. **회사는 AWS Fargate 컨테이너에서 수백 개의 보안 서비스를 실행하는 Amazon Elastic Container Service(Amazon ECS) 클러스터에 웹 애플리케이션을 가지고 있습니다. 서비스는 ALB(Application Load Balancer)가 라우팅하는 대상 그룹에 있습니다. 애플리케이션 사용자는 웹사이트에 익명으로 로그인하지만 보안 서비스에 액세스하려면 OpenID Connect 프로토콜 호환 ID 공급자(IdP)를 사용하여 인증되어야 합니다.**

    **최소한의 노력으로 이러한 요구 사항을 충족하는 인증 방법은 무엇입니까?**

    > Amazon Cognito를 사용하도록 서비스를 구성합니다.



63. **회사에 PHP와 WordPress로 개발되고 AWS Elastic Beanstalk를 사용하여 시작된 웹 사이트가 있습니다. Elastic Beanstalk 환경에 배포해야 하는 웹 사이트의 새 버전이 있습니다. 회사는 업데이트가 실패할 경우 웹사이트를 오프라인으로 유지하는 것을 용납할 수 없습니다. 배포는 최소한의 영향을 미치고 가능한 한 빨리 롤백해야 합니다.**

    **어떤 배포 방법을 사용해야 합니까?**

    > Immutable

- Immutable environment updates are an alternative to rolling updates. Immutable environment updates ensure that configuration changes that **require replacing instances are applied efficiently and safely.** If an immutable environment update fails, **the rollback process requires only terminating an Auto Scaling group**. A failed rolling update, on the other hand, requires **performing an additional rolling update to roll back the changes.**



64. **아래 Lambda 함수는 Amazon API Gateway를 사용하여 API를 통해 호출됩니다. Lambda 함수의 평균 실행 시간은 약 1초입니다.**

    **Lambda 함수에 대한 의사 코드는 아래와 같습니다.**

    ```python
    include "3rd party encryption module"
    include "match module"
    lambda_handler (event, context)
        rds_host = "rds-instance-endpoint"
        name = db_username
        password = db_password
        db_name = db_name
    # Connect to the RDS Database
    Conn = RDSConnection(rds_host, user=name, passwd=password, db=db_name, connect_timeout=5)
    # Perform some Processing reading data from the RDS database
    # Code Block
    # Code Block
    # Code Block
    ```

    **솔루션 비용을 증가시키지 않고 이 Lambda 함수의 성능을 개선하기 위해 취할 수 있는 두 가지 조치는 무엇입니까? (2개를 선택하세요.)**

> Lambda 함수에 필요한 모듈만 패키징합니다.
>
> 변수 Amazon RDS 연결의 초기화를 핸들러 함수 외부로 이동