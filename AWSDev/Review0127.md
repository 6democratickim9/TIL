1. ### **Amazon SQS**

> 개발자는 Amazon SQS 대기열에서 메시지 처리를 담당하는 애플리케이션이 일상적으로 뒤처지고 있음을 발견했습니다. 애플리케이션이 한 번의 실행으로 여러 메시지를 처리할 수 있지만 한 번에 하나의 메시지만 수신합니다. 애플리케이션이 **수신하는 메시지 수를 늘리려면** 개발자는 어떻게 해야 합니까?

> A developer has discovered that an application responsible for processing messages in an Amazon SQS queue is routinely falling behind. The application is capable of processing multiple messages in one execution, but is only receiving one message at a time What should the developer do to **increase the number of messages the application receives?**

- ReceiveMessage API를 호출하여 MaxNumberOfMessages를 기본값인 1보다 큰 값으로 설정
- Call the ReceiveMessage API to set MaxNumberOfMessages to a value greater than the default of 1
- **MaxNumberOfMessages**
  - The maximum number of messages to return. Amazon SQS never returns more messages than this value (however, fewer messages might be returned). Valid values: 1 to 10. Default: 1.
  - Type: Integer
  - Required: No

2. ### AWS Cloud Formation

> 개발자가 AWS Cloud Formation을 사용하여 배포 패키지를 준비하고 있습니다. 패키지는 두 개의 개별 템플릿으로 구성됩니다. 하나는 인프라용이고 다른 하나는 애플리케이션용입니다. 애플리케이션은 인프라 템플릿에서 생성된 VPC 내부에 있어야 합니다. 애플리케이션 스택이 **인프라 템플릿에서 생성된 VPC를 어떻게 참조**할 수 있습니까?

> A developer is using AWS CloudFormation to create a deployment package. Two distinct templates are included in the package: one for the infrastructure and another for the application. The application **must be contained inside the VPC** built using the infrastructure template's infrastructure template.
>
> How can the application stack **make reference to the VPC established using the infrastructure template's infrastructure template?**

- 인프라 템플릿에서 내보내기 플래그를 사용한 다음 응용 프로그램 템플릿에서 `Fn::lmportValue` 함수를 사용합니다.
-  Use the export flag in the infrastructure template, and then use the `Fn::ImportValue` function in the application template.
- To reference a resource in another AWS CloudFormation stack, you must **create cross-stack references.** To create a cross-stack reference, **use the *export field to flag the value of a resource output for export*. Then, use the `Fn::ImportValue` intrinsic function to import the value in any stack within the same Region and account**. Exported values are identified by the names specified in the template. These names must be unique to your Region and account. 

3. ### Amazon S3

> 개발자는 Amazon S3 버킷으로 전달되는 데이터를 처리할 애플리케이션을 작성하고 있습니다. 데이터는 하루에 약 10번 전달되며 개발자는 데이터가 평균적으로 1분 이내에 처리될 것으로 예상합니다.
> 개발자는 **비용과 대기 시간이 가장 낮은 애플리케이션을 어떻게 배포하고 호출**할 수 있습니까?

> A programmer is developing an application that will process data that has been uploaded to an Amazon S3 bucket. The developer anticipates that the data will be processed in less than one minute on average.
>
> How can the developer **deploy and activate the program efficiently and with the least amount of latency?**

- (내가 맞음;;)
-  Deploy the application as an AWS Lambda function and invoke it with an S3 event notification.

4. ### ECR

> AWS CodeBuild는 애플리케이션용 코드를 빌드하고, 도커 이미지를 생성하고, 이미지를 Amazon Elastic Container Registry(Amazon ECR)로 푸시하고, 고유 식별자로 이미지에 태그를 지정합니다.
> 개발자가 워크스테이션에 이미 **AWS CLI를 구성한 경우 Docker 이미지를 워크스테이션으로 가져오려면** 어떻게 해야 합니까?

> AWS CodeBuild generates the source code for an application, develops the Docker image, uploads it to Amazon Elastic Container Registry (Amazon ECR), and tags it with a unique identifier.
>
> If developers already have the **AWS CLI setup on their workstations, how are the Docker images downloaded** to the workstations?

- **`aws ecr get-login` 및 `run:docker pull REPOSITORY URI: TAG`의 출력을 실행합니다.**
- Run the **output of the following**: `aws ecr get-login` and then `run: docker pull REPOSITORY URI : TAG`
-  you should **run the output of the command** then pull the image

5. ### AWS Elastic Beanstalk

> 회사에는 개발 프로젝트를 위해 코드를 점진적으로 업데이트하는 여러 개발자가 전 세계에 있습니다. 개발자가 코드를 동시에 업로드하면 인터넷 연결이 느려지고 AWS Elastic Beanstalk에 배포할 코드를 업로드하는 데 시간이 오래 걸립니다.
> 최소한의 관리 노력으로 업**로드 및 배포 시간을 최소화하는 단계**는 무엇입니까?

> A corporation has numerous developers stationed across the world who are progressively upgrading code for a development project. When developers upload code simultaneously, internet connection is poor, and uploading code for deployment in AWS Elastic Beanstalk takes a long time.
>
> Which approach will result in the **smallest amount of administrative work and the shortest upload and deployment times?**

- **AWS CodeCommit 리포지토리를 생성하고 개발자가 여기에 코드를 커밋하도록 허용한 다음 코드를 Elastic Beanstalk에 직접 배포합니다.**
- (얘도 내가맞음;;머하냐ㅡ.ㅡ)

6. ### KMS GenerateKey

> 수백 개의 비디오 파일을 저장하려면 개발 중인 애플리케이션이 필요합니다. 데이터는 저장하기 전에 각 비디오 파일에 대한 **고유 키를 사용하여 애플리케이션 내에서 암호화**되어야 합니다.
> 개발자는 애플리케이션을 어떻게 코딩해야 합니까?

> An application under development is required to store hundreds of video files. The data must be **encrypted within the application prior to storage, with a unique key for each video file.**
> How should the Developer code the application?

- **KMS GenerateDataKey API를 사용하여 데이터 키를 가져옵니다. 데이터 키로 데이터를 암호화합니다. 암호화된 데이터 키와 데이터를 저장합니다.**
- Use the KMS GenerateDataKey API to get a data key. Encrypt the data with the data key. Store the encrypted data key and data.
- GenerateDataKey generates a **unique symmetric data key for client-side encryption**. This operation returns a **plaintext copy of the data key and a copy that is encrypted under a customer master key (CMK) that you specify.** You can use the plaintext key to encrypt your data outside of AWS KMS and store the encrypted data key with the encrypted data.

7. ###  Code Pipeline

> 개발 팀은 소스 코드가 변경될 때마다 개발 팀은 소스 코드가 변경될 때마다 즉시 애플리케이션을 빌드하고 배포하기를 원합니다. 배포를 트리거하는 데 사용할 수 있는 접근 방식은 무엇입니까? (2개를 선택하십시오.)하기를 원합니다. 배포를 트리거하는 데 사용할 수 있는 접근 방식은 무엇입니까? (2개를 선택하십시오.)

> A development team wishes to build and **deploy an application instantly** after a modification to the source code is made.
>
> Which methods could be utilized to initiate the deployment? (Select two.)

-  **Amazon S3 버킷에 소스 코드 저장 버킷의 파일이 변경될 때마다 시작하도록 AWS CodePipeline 구성**

- **AWS CodeCommit 리포지토리에 소스 코드 저장 변경 사항이 리포지토리에 커밋될 때마다 시작하도록 AWS CodePipeline을 구성합니다.**

  (이것두 내가맞음;;)

8. ### AWS X-Ray

   > **AWS X-Ray로 Lambda 기반 애플리케이션을 추적**하려면 무엇이 필요합니까?

   > What is needed to use **AWS X-Ray to trace Lambda-based application**s?

   - **IAM 실행 역할을 사용하여 Lambda 함수 권한 및 활성화된 추적을 제공합니다**

   -  Use an IAM execution role to give the Lambda function permissions and enable tracing.

   - Your function **needs permission to upload trace data to X-Ray.** When you enable active tracing in the Lambda console, Lambda adds the required permissions to your function's execution role. Otherwise, a**dd the AWSXRayDaemonWriteAccess policy to the execution role.**

     (이것두 내가맞음...우짠댜)

9. ### S3

   > 개발자가 Amazon S3 PutObject API 작업을 사용하여 기본 암호화가 활성화된 S3 버킷에 객체를 업로드하려고 합니다. 개발자는 **400 잘못된 요청 오류를 수신**합니다.
   > 이 오류의 가장 가능성 있는 원인은 무엇입니까?

   > A developer is attempting to use the Amazon S3 PutObject API operation to upload an object to an S3 bucket that has default encryption enabled. The developer receives a **400 Bad Request error**.
   > What is the MOST likely cause of this error?

   - **S3 버킷이 허용되는 최대 스토리지 용량을 초과합니다.**

   - | `LimitExceededException` | 요청 결과가 볼트 제한, 태그 제한 또는 프로비저닝된 용량 제한 중 한 가지를 초과한 경우에 반환됩니다. |
     | ------------------------ | ------------------------------------------------------------ |

     Returned if a retrieval job will exceed the **current data policy's retrieval rate limit.** For more information about data retrieval policies, see [Amazon S3 Glacier Data Retrieval Policies](https://docs.aws.amazon.com/amazonglacier/latest/dev/data-retrieval-policy.html).

10. ### Customer's Responsibility

> AWS에서 고객의 책임은 어떤 보안 측면입니까? 4개의 답변을 선택하세요

> In AWS, which security aspects are the customer's responsibility? Choose 4 answers

- A. **Life-cycle management of IAM credentials** 
- C. **Security Group and ACL (Access Control List) settings** 
- D. **Encryption of EBS (Elastic Block Storage) volumes** 
- F. **Patch management on the EC2 instance’s operating system**
- 물리적이지 않은 부분은 모두 고객의 몫

11. ### Amazon Congnito

> 개발자는 새 사용자가 새 사용자 계정을 등록하고 만들 수 있도록 하는 응용 프로그램을 빌드하려고 합니다.
> 또한 애플리케이션은 소셜 미디어 계정이 있는 사용자가 소셜 미디어 자격 증명을 사용하여 로그인할 수 있도록 허용해야 합니다.
> 이러한 요구 사항을 충족하기 위해 어떤 AWS 서비스 또는 기능을 사용할 수 있습니까?

> A developer wants to build an application that will allow new users to register and create new user accounts.
> The application must also allow users with social media accounts to log in using their social media credentials.
> Which AWS service or feature can be used to meet these requirements?

- **Amazon Cognito 사용자 풀**

------

43번부터

12. ###  Amazon CloudWatch

> 개발자는 시스템 관리자가 EC2 인스턴스에서 실행 중인 애플리케이션의 **로그 데이터를 사용**할 수 있도록 액세스를 원합니다.
> 다음 중 **Amazon CloudWatch에서 이 지표를 모니터링**할 수 있는 것은 무엇입니까?

> A Developer wants access to make the log data of an application running on an EC2 instance available to systems administrators.
> Which of the **following enables monitoring of this metric in Amazon CloudWatch?**

- **애플리케이션이 실행 중인 EC2 인스턴스에 Amazon CloudWatch Logs 에이전트를 설치합니다.**
-  **Install the Amazon CloudWatch Logs agent on the EC2 instance that the application is running on.**
- 굳이 새 인스턴스를 설치할 필요 없이 CloudWatch Logs Agent를 해당 EC2에 설치하면 된다

13. ### *DynamoDB Security*

> 회사는 직원이 개인 Amazon S3 버킷에 프로필 사진을 업로드할 수 있는 웹 애플리케이션을 개발 중입니다. 프로필 사진에는 크기 제한이 없으며 직원이 로그인할 때마다 표시되어야 합니다. **보안상의 이유로 사진은 업로드할 수 없습니다**. **공개적으로 액세스할 수 있습니다.**
> 이 시나리오에 대한 실행 가능한 장기 솔루션은 무엇입니까'?

> A company is developing a web application that allows its employees to upload a profile picture to a private Amazon S3 bucket There is no size limit for the profile pictures, which should be displayed every time an employee logs in. For security reasons, **the pictures cannot be publicly accessible.**
> What is a viable long-term solution for this scenario?

- (이것도 내가맞음;;)
- **사진의 S3 키를 Amazon DynamoDB 테이블에 저장합니다. 함수를 사용하여 직원이 로그인할 때마다 미리 서명된 URL을 생성합니다. URL을 브라우저에 반환합니다.**
- the object owner can **optionally share objects with others by creating a presigned URL,** using their own security credentials, to grant time-limited permission to download the objects
- VPC endpoint is for private subnets, if the user logged in and want to access the **S3 url it will not work since it's client side and outside the VPC**. The only way to work with VPC endpoint would be an application inside VPC downloading the image and sending to the client (as a proxy). 

14. ### Swagger - SAM

    > 개발자는 AWS에 서버리스 RESTful API를 반복적이고 일관되게 배포해야 합니다.
    > 어떤 기술이 작동할까요? (2개를 선택하세요.)

    > A Developer must repeatedly and consistently deploy a serverless RESTful API on AWS.
    > Which techniques will work? (Choose two.)

    - ** **인라인 Swagger 정의를 사용하여 SAM 템플릿을 배포합니다.**
      - **Deploy a SAM template with an inline Swagger definition.**
    - **Swagger 파일을 정의합니다. Swagger 파일을 참조하는 SAM 템플릿을 배포합니다.**
      - **Define a Swagger file. Deploy a SAM template that references the Swagger file.**

15. ### Lambda

    > 개발자가 콘솔에서 기존 프로그램을 AWS Lambda 함수로 변환했습니다. 프로그램이 로컬 랩톱에서 제대로 실행되지만 Lambda 콘솔에서 테스트할 때 **"모듈을 가져올 수 없음"** 오류가 표시됩니다. 다음 중 오류를 수정할 수 있는 것은 무엇입니까?

> A developer converted an existing program to an AWS Lambda function in the console. The program runs properly on a local laptop, but shows an "Unable to import module" error when tested in the Lambda console Which of the following can fix the error?

- **Lambda 코드에서 Linux 명령을 호출하여 /usr/lib 디렉토리 아래에 누락된 모듈을 설치합니다.**
-  **In the Lambda code invoke a Linux command to install the missing modules under the /usr/lib directory**

- Same for me. I am working with Python 3.6 on Mac, so `sudo chmod 777 /usr/local/lib/python3.6/site-packages` did the trick 

  

16. ### *ELB*

    > 스타트업의 사진 공유 사이트는 VPC에 배포됩니다. ELB는 두 개의 서브넷에 웹 트래픽을 분산합니다. ELB 세션 고정은 세션 TTL이 5분인 AWS 생성 세션 쿠키를 사용하도록 구성됩니다.
    > 웹서버 Auto Scaling Group은 min-size=4, max-size=4로 구성됩니다.
    > us-west-2a에서 실행되는 단일 EC2 인스턴스에 설치된 부하 테스트 소프트웨어를 실행하여 공개 출시를 준비하는 스타트업. 60분의 부하 테스트 후 웹 서버 로그에 다음이 표시됩니다.
    > 부하 테스트 HTTP 요청이 **4개의 웹 서버에 고르게 분산되도록 하는 데 도움이 되는 권장 사항**은 무엇입니까? 2개의 답변을 선택하세요

    > A startup s photo-sharing site is deployed in a VPC. An ELB distributes web traffic across two subnets. ELB session stickiness is configured to use the AWS-generated session cookie, with a session TTL of 5 minutes.
    > The webserver Auto Scaling Group is configured as: min-size=4, max-size=4.
    > The startups preparing for a public launch, by running load-testing software installed on a single EC2 instance running in us-west-2a. After 60 minutes of load-testing, the webserver logs show:
    > Which recommendations can help **ensure load-testing HTTP requests are evenly distributed across the four webservers**? Choose 2 answers

- (이것두 내가맞음;;)

-  **로드 테스트 소프트웨어를 재구성하여 각 웹 요청에 대해 DNS를 다시 확인합니다.**
- **전 세계적으로 분산된 테스트 클라이언트를 제공하는 타사 부하 테스트 서비스를 사용합니다.**

- (B)If clients do not re-resolve the DNS at least once per minute, then the new resources Elastic Load Balancing adds to DNS will not be used by clients. This can mean that clients continue to overwhelm a small portion of the allocated Elastic Load Balancing resources, while overall Elastic Load Balancing is not being heavily utilized. This is not a problem that can occur in real-world scenarios, but it is a likely problem for load testing tools that do not offer **the control needed to ensure that clients are re-resolving DNS frequently**. 
- (C) Private beta users prove that **ELB is distributing the load correctly**

17. ### Dynamo DB

> C사는 최근 AWS에서 자전거를 위한 온라인 상거래 사이트를 시작했습니다. 제조업체, 색상, 가격, 수량 및 크기와 같이 온라인 상점에 표시할 각 자전거에 대한 세부 정보를 저장하는 "제품" DynamoDB 테이블이 있습니다. 고객 요구로 인해 기존 세부 정보와 함께 각 자전거에 대한 이미지를 포함하려고 합니다.
> 아래에서 **"제품" 테이블의 프로비저닝된 처리량에 가장 적은 영향을 미치는 접근 방식**은 무엇입니까?

> Company C has recently launched an online commerce site for bicycles on AWS. They have a "Product" DynamoDB table that stores details for each bicycle, such as, manufacturer, color, price, quantity and size to display in the online store. Due to customer demand, they want to include an image for each bicycle along with the existing details.
> Which approach below **provides the least impact to provisioned throughput on the "Product" table?**

-  **Amazon S3에 이미지를 저장하고 각 이미지에 대한 "제품" 테이블 항목에 S3 URL 포인터를 추가합니다.**
-  Not to impact the throughput one should not increase the size of the data. Best solution is to store the images outside the DB and just **add a link to the image** on the outside storage

18. ### IAM

> 개발자는 IAM 역할을 사용하여 여러 EC2 인스턴스에 배포할 소프트웨어 패키지를 생성했습니다.
> **Amazon Kinesis Streams에서 레코드를 가져오기 위해 IAM 액세스를 확인하기 위해 수행할 수 있는 작업은** 무엇입니까? (2개를 선택하십시오.)

> A Developer has created a software package to be deployed on multiple EC2 instances using IAM roles.
> What actions could be performed to verify IAM access to get records from Amazon Kinesis Streams? (Select TWO.)

- **AWS CLI를 사용하여 IAM 그룹을 검색합니다.**
  - Then you can get detailed role info by running AWS CLI https://docs.aws.amazon.com/cli/latest/reference/iam/get-role.html
  - 예비답안1 - 근데 얘가 좀 더 맞는듯?
- --dry-run 인수를 사용하여 get 작업을 수행합니다.
  - Examtopics 유저들이 주장하는 답안. 실행했을 때 막혀있으면 accessDenied 되기 때문에 액세스 권한을 알 수 있다는 얘기.
  - 예비답안 2
-  **IAM 정책 시뮬레이터로 IAM 역할 정책을 검증합니다.**
- (이 문제에 대한 답이 갈림)

19. ### S3

    > 회사에는 사용자 유형에 따라 Amazon S3에서 객체를 읽는 애플리케이션이 있습니다. 사용자 유형은 등록된 사용자와 게스트 사용자입니다. 회사에는 25,000명의 사용자가 있고 증가하고 있습니다. 정보는 사용자 유형에 따라 S3 버킷에서 가져옵니다.
    > 두 사용자 유형 **모두에 대한 액세스를 제공하려면 어떤 접근 방식을 권장**합니까? (2개를 선택하십시오.)

> A company has an application where reading objects from Amazon S3 is based on the type of user The user types are registered user and guest user The company has 25.000 users and is growing Information is pulled from an S3 bucket depending on the user type.
> Which approaches are recommended to provide access to both user types? (Select TWO.)

- **Amazon Cognito를 사용하여 인증된 역할과 인증되지 않은 역할을 사용하여 액세스 제공**
- AWS IAM 서비스를 사용하고 애플리케이션이 사용자 유형에 따라 **AWS Security Token Service(AWS STS) AssumeRole 작업을 사용하여 다른 역할을 맡도록 하고 위임된 역할을 사용하여 Amazon S3에 대한 읽기 액세스 권한을 제공합니다.**

20. ### *DynamoDB*

> Amazon DynamoDB 테이블에 대한 쿼리는 많은 양의 읽기 용량을 소비합니다. 테이블에는 많은 수의 큰 속성이 있습니다. 응용 프로그램에는 모든 속성 데이터가 필요하지 않습니다.
> **애플리케이션 성능을 최대화하면서 DynamoDB 비용을 최소화**하려면 어떻게 해야 합니까?

> Queries to an Amazon DynamoDB table are consuming a large amount of read capacity. The table has a significant number of large attributes. The application does not need all of the attribute data.
> How can **DynamoDB costs be minimized while maximizing application performance?**

- (내가맞음)
- **최소한의 프로젝션 속성 집합으로 글로벌 보조 인덱스를 생성합니다.**
- A projection is the set of attributes that is copied from a table into a secondary index. The partition key and sort key of the table are always projected into the index; you can project other attributes to support your application's query requirements. When you query an index, Amazon DynamoDB can access any attribute in the projection as if those attributes were in a table of their own
- global secondary indexes **reduce the amount of data returned to queries**
- 지수 백오프가 아닌 이유 - The exponential back off normally only apply to Peak situation, and not reduce cost

21. ### AmazonS3 - 정답 다름

    > 애플리케이션은 키가 온프레미스 데이터 센터(사용자/클라이언트)에서 관리되고 암호화가 **S3에서 처리되는 Amazon S3에 기록되는 데이터를 암호화**해야 합니다. **어떤 유형의 암호화를 사용**해야 합니까?

    > An application must encrypt data that is written to Amazon S3, where the keys are controlled in-house and S3 handles the encryption.
    >
    > Which encryption method should be used?

    - **고객이 제공한 키로 서버 측 암호화 사용**
    - With Server-Side Encryption with Customer-Provided Keys (SSE-C), you manage the encryption keys and Amazon S3 manages the encryption, as it writes to disks, and decryption, when you access your objects
    - **고객 제공 키를 사용한 서버 측 암호화(SSE-C)**
      - 고객 제공 키를 사용한 서버 측 암호화(SSE-C)를 사용하면 사용자는 암호화 키를 관리하고 Amazon S3는 암호화(디스크에 쓸 때) 및 해독(객체에 액세스할 때)을 관리합니다. 자세한 정보는 [고객 제공 암호화 키(SSE-C)로 서버 측 암호화를 사용하여 데이터 보호](https://docs.aws.amazon.com/ko_kr/AmazonS3/latest/userguide/ServerSideEncryptionCustomerKeys.html)을 참조하세요.

22. ### Security

    > 회사는 Admin 그룹의 한 사용자만 Amazon EC2 리소스를 삭제할 수 있는 **영구적인 권한**을 갖도록 하려고 합니다. Admin 그룹의 **기존 정책에는 변경 사항이 없어야 합니다**. 개발자는 이러한 요구 사항을 충족하기 위해 무엇을 사용해야 합니까?

> A company wants to make sure that only one user from its Admin group has the permanent right to delete an Amazon EC2 resource There should be no changes in the existing policy under the Admin group What should a developer use to meet these requirements?

- **Inline policy**

23. ### *SAM*

> 개발자가 서버리스 애플리케이션의 배포 프로세스를 자동화하는 스크립트를 만들고 있습니다. 개발자가 애플리케이션에 기존 AWS 서버리스 애플리케이션 모델(AWS SAM) 템플릿을 사용하려고 합니다. 개발자는 프로젝트에 무엇을 사용해야 합니까? (2개 선택)

> A developer is creating a script to automate the deployment process for a serverless application. The developer wants to use an existing AWS Serverless Application Model (AWS SAM) template for the application What should the developer use for the project? (Select TWO)

- (이것두 내가맞는듯)
- **배포 패키지를 생성하기 위한 Call aws cloudformation 패키지 이후에 패키지를 배포하기 위해 aws cloudformation deploy를 호출합니다.**
- **sam 패키지를 호출하여 배포 패키지 생성 나중에 패키지를 배포하려면 sam deploy를 호출합니다.**
- https://docs.aws.amazon.com/codedeploy/latest/userguide/tutorial-lambda-sam-package.html

24. ### Session Data - 정답 다름

> 개발자는 분당 최소 5000개 요청을 처리할 수 있어야 하는 3계층 웹 애플리케이션을 구축하고 있습니다. 요구 사항에는 애플리케이션이 사용자에 대한 세션 상태를 유지하는 동안 웹 계층이 완전히 상태 비저장이어야 한다고 명시되어 있습니다.
> 대기 시간을 가능한 한 **가장 낮은 값으로 유지하면서 세션 데이터를 어떻게 외부화**할 수 있습니까?

> A developer is developing a three-tier web application that must support at least 5000 requests per minute. According to the requirements, the web layer should be **fully stateless, whereas the application should keep user session data.**
>
> How may session data be **externalized while minimizing latency**?

- Amazon DynamoDB 테이블을 생성한 다음 애플리케이션 수준에서 세션 처리를 구현하여 세션 데이터 저장용 테이블 활용
- Create an Amazon DynamoDB table, then implement session handling at the application level to leverage the table for session data storage
  - The answer would be **ElastiCache, but NOT memcached**. That is not **persistent and the question specifies it**. So it has to be D. This is a trick question that's just there to find out if you know the differences between redis and memcached. That's it guys

25. ### *API Gateway*

> 회사는 많은 다운스트림 소비자에게 서비스를 제공하고 있습니다. 각 소비자는 하나 이상의 서비스에 연결할 수 있습니다. 그 결과 관리하기 어렵고 확장이 잘 되지 않는 복잡한 아키텍처가 발생했습니다. 회사는 소비자에 대한 이러한 서비스를 관리하기 위해 단일 인터페이스가 필요합니다.
> 이 아키텍처를 리팩토링하려면 어떤 AWS 서비스를 사용해야 합니까?

> A company is providing services to many downstream consumers. Each consumer may connect to one or more services. This has resulted in a complex architecture that is difficult to manage and does not scale well. The company needs a single interface to manage these services to consumers.
> Which AWS service should be used to refactor this architecture?

- (내가 맞음;;)
- Amazon API Gateway

26. ### Amazon Cognito

> 회사는 Amazon API Gateway REST API를 통해 액세스할 애플리케이션을 개발 중입니다. 등록된 사용자는 이 API의 특정 리소스에 액세스할 수 있는 유일한 사용자여야 합니다. 사용 중인 토큰은 자동으로 만료되어야 하며 주기적으로 새로 고쳐야 합니다.
> 개발자는 이러한 요구 사항을 어떻게 충족할 수 있습니까?'

> A company is developing an application that will be accessed through the Amazon API Gateway REST API Registered users should be the only ones who can access certain resources of this API. The token being used should expire automatically and needs to be refreshed periodically.
> How can a developer meet these requirements'?

- **Amazon Cognito 사용자 풀 생성, API Gateway에서 Cognito Authorizer 구성, 자격 증명 또는 액세스 토큰 사용**
- User pools are for authentication (identify verification). With a user pool, your app users can sign in through the user pool or federate through a third-party identity provider (IdP).
- Cognito User pool= user & Lambda Authorizer = Generate Token

27. ### IAM

> 배포 패키지는 AWS CLI를 사용하여 환경 변수에 저장된 액세스 키를 사용하여 계정의 모든 S3 버킷에 파일을 복사합니다. 패키지는 EC2 인스턴스에서 실행되고 있으며 인스턴스는 수임된 IAM 역할과 하나의 버킷에만 액세스를 허용하는 보다 제한적인 정책으로 실행되도록 수정되었습니다.
> 변경 후 개발자는 호스트에 로그인하고 여전히 해당 계정의 모든 S3 버킷에 쓸 수 있습니다.
> 이 상황의 가장 가능성 있는 원인은 무엇입니까?

> A deployment package uses the AWS CLI to copy files into any S3 bucket in the account, using access keys stored in environment variables. The package is running on EC2 instances, and the instances have been modified to run with an assumed IAM role and a more restrictive policy that allows access to only one bucket.
> After the change, the Developer logs into the host and still has the ability to write into all of the S3 buckets in that account.
> What is the MOST likely cause of this situation?

- (내가맞음;;)

- **AWS 자격 증명 공급자가 마지막으로 인스턴스 프로필 자격 증명을 찾습니다.**
- **The AWS credential provider looks for instance profile credentials last**
- A deployment package uses the AWS CLI to copy files into any S3 bucket in the account, using access keys stored in environment variables.

28. ### API Access - 정답다름

> 회사는 API를 서비스로 제공하고 모든 사용자와 SLA(서비스 수준 계약)를 약속합니다.
> 각 SLA를 준수하기 위해 회사는 무엇을 해야 합니까?

> A business delivers APIs as a service and binds all of its users to a service level agreement (SLA).
>
> What should the organization do to ensure compliance with each SLA?

- **사용자별 사용 계획을 수립하고 API 접근을 위한 API 키를 요청합니다.**

  - **Create a usage plan for each user and request API keys to access the APIs**

  - A usage plan specifies who can access one or more deployed API stages and methods—and also how much and how fast they can access them. The plan uses API keys to identify API clients and meters access to the associated API stages for each key. It also lets you configure throttling limits and quota limits that are enforced on individual client API keys.

29. ### DynamoDB

> 개발자는 Amazon DynamoDB 테이블의 항목 수명 주기 활동을 기반으로 AWS Lambda 함수를 트리거해야 합니다.
> 개발자는 어떻게 솔루션을 만들 수 있습니까?

> A Developer must trigger an AWS Lambda function based on the item lifecycle activity in an Amazon DynamoDB table.
> How can the Developer create the solution?

-  **DynamoDB 스트림을 활성화하고 스트림에서 동기적으로 Lambda 함수를 트리거합니다**
- Enable a DynamoDB stream, and trigger the Lambda function synchronously from the stream. 
- https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Streams.Lambda.html

30. ### EBS

> 진료실 관리 애플리케이션에서는 EC2 인스턴스와 Amazon EBS 볼륨 간에 전송 중인 모든 데이터를 암호화해야 합니다. 다음 기술 중 이 요구 사항을 충족하는 기술은 무엇입니까? (2개 선택)

> All data in transit between an EC2 instance and an Amazon EBS volume must be secured for a physician's office management application.
>
> Which one of the following strategies satisfies this criterion? (Select two.)

- 이것두 내가맞음;;
- **1AM 역할을 사용하여 Amazon EBS 볼륨에 대한 액세스 제한**
  - You need to enable **EBS encryption otherwise the data is not secure**
- **EBS 암호화 활성화**
  - EC2 is being used to access EBS so IAM roles are the most secure. 

31. ### Auto Scale

> 회사 웹 사이트가 Amazon EC2 인스턴스에서 실행되고 피크 시간에 환경을 Auto Scale 사용합니다. 전 세계 웹 사이트 사용자는 피크 시간이 아닌 경우에도 EC2 인스턴스의 정적 콘텐츠로 인해 높은 지연 시간을 경험하고 있습니다.
> 어떤 단계 조합으로 대기 시간 문제를 해결할 수 있습니까? (2개 선택)

> The website of a business is hosted on an Amazon EC2 instance, which utilizes Auto Scaling to automatically scale the environment during peak periods. Worldwide, website visitors are experiencing increased latency as a result of static material on the EC2 instance, even during off-peak hours.
>
> Which sequence of actions will overcome the problem of latency? (Select two.)

- 이것두 내가맞음;;
- **정적 콘텐츠를 캐시할 Amazon CloudFront 배포 생성**
- **Amazon S3에 애플리케이션의 정적 콘텐츠 저장**

32. ### VPC - 정답다름

> Amazon VPC를 사용하는 퍼블릭 서브넷과 이 서브넷에서 실행 중인 3개의 인스턴스로 구성된 환경이 있습니다. 이 세 가지 인스턴스는 인터넷의 다른 호스트와 성공적으로 통신할 수 있습니다. 다른 인스턴스에 사용한 것과 동일한 AMI 및 보안 그룹 구성을 사용하여 동일한 서브넷에서 네 번째 인스턴스를 시작했지만 이 인스턴스는 인터넷에서 액세스할 수 없습니다.
> 인터넷 액세스를 활성화하려면 어떻게 해야 합니까?

> You have an environment that consists of a public subnet using Amazon VPC and 3 instances that are running in this subnet. These three instances can successfully communicate with other hosts on the Internet. You launch a fourth instance in the same subnet, using the same AMI and security group configuration you used for the others, but find that this instance cannot be accessed from the Internet.
> What should you do to enable internet access?

- **네 번째 인스턴스에 탄력적 IP 주소를 할당합니다.**

33. ### DynamoDB

> 회사는 거래 요청을 처리하는 데 밀리초 미만의 대기 시간이 필요한 주식 거래 애플리케이션을 구축하고 있습니다. Amazon DynamoDB는 각 **요청을 처리하는 데 사용되는 모든 거래 데이터를 저장하는 데 사용**됩니다. 애플리케이션을 로드 테스트한 후 개발 팀은 데이터 검색 시간으로 인해 **대기 시간 요구 사항이 충족되지 않음**을 발견했습니다. 요청 수가 갑자기 급증하기 때문에 조절을 피하기 위해 DynamoDB 읽기 용량을 상당히 과도하게 프로비저닝해야 합니다.
> **대기 시간 요구 사항을 충족하고 애플리케이션 실행 비용을 줄이려면 어떤 조치**를 취해야 합니까?

> A company is building a stock trading application that requires sub-millisecond latency in processing trading requests. Amazon DynamoDB is used to store all the trading data that is used to process each request. After load testing the application, the development team found that due to data retrieval times, the latency requirement is not satisfied. Because of sudden high spikes in the number of requests, DynamoDB read capacity has to be significantly over-provisioned to avoid throttling.
> What steps should be taken to meet latency requirements and reduce the cost of running the application?

- **DynamoDB Accelerator를 사용하여 거래 데이터를 캐시합니다.**

34. ### CloudWatch

> 회사에 매시간 실행되고, Amazon S3에 저장된 로그 파일을 읽고, 콘텐츠를 기반으로 Amazon Simple Notification Service(Amazon SNS) 주제에 경고를 전달하는 AWS Lambda 함수가 있습니다. 개발자는 Lambda 함수에 사용자 지정 지표를 추가하기를 원합니다. 각 실행에 대한 각 유형의 경고 수를 추적합니다. 개발자는 Lambda/AlertCounts라는 지표의 Amazon CloudWatch에 이 정보를 기록해야 합니다. 개발자는 최소 운영 오버헤드로 이 요구 사항을 충족하도록 Lambda 함수를 수정해야 합니다.''

> A company has an AWS Lambda function that runs hourly, reads log files that are stored in Amazon S3, and forwards alerts to Amazon Simple Notification Service (Amazon SNS) topics based on content A developer wants to add a custom metric to the Lambda function to track the number of alerts of each type for each run The developer needs to log this information in Amazon CloudWatch in a metric that is named Lambda/AlertCounts How should the developer modify the Lambda function to meet this requirement with the LEAST operational overhead''

- **PutMetncAlarm API 작업에 대한 호출 추가 "Lambda/AlertCounts" 네임스페이스를 사용하여 메트릭 구성원의 경고 배열 전달**