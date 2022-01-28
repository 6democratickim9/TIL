125. 개발자는 인프라를 변경하거나 상태 확인을 구성하지 않고 AWS를 사용하여 신속하게 배포해야 하는 Docker 애플리케이션으로 작업하고 있습니다. 다운타임 없이 변경 및 업데이트가 자동으로 수행될 수 있도록 애플리케이션을 구성해야 합니다. 이러한 요구 사항을 충족하는 솔루션은 무엇입니까?

> A developer Is working with a Docker application that needs to be quickly deployed using AWS without changing the infrastructure or configuring health checks. The application should be configured so that changes and updates can be made automatically without any downtime Which solution will meet these requirements?

- **배포 방식(Deployment policy)** - 다음 배포 옵션 중에서 선택합니다.
  - **한 번에 모두(All at once)** - 새 버전을 모든 인스턴스에 동시에 배포합니다. 배포가 수행되는 동안 환경에 있는 모든 인스턴스가 잠시 서비스 중지됩니다.
  - **롤링(Rolling)** - 새 버전을 배치로 배포합니다. 각 배치는 배포 단계 동안 서비스에서 제외되므로 배치에 있는 인스턴스의 수만큼 환경의 용량이 감소합니다.
  - **추가 배치를 사용한 롤링(Rolling with additional batch)** - 새 버전을 배치로 배포하지만, 먼저 새로운 배치의 인스턴스를 시작하여 배포 프로세스 중에 모든 용량이 유지되도록 합니다.
  - **변경 불가능(Immutable)** - [변경 불가능 업데이트](https://docs.aws.amazon.com/ko_kr/elasticbeanstalk/latest/dg/environmentmgmt-updates-immutable.html)를 수행하여 새 버전을 새로운 인스턴스 그룹에 배포합니다.
  - **트래픽 분할(Traffic splitting)** - 새 버전을 새 인스턴스 그룹에 배포하고 수신되는 클라이언트 트래픽을 일시적으로 기존 애플리케이션 버전과 새 애플리케이션 버전 간에 분할합니다.

- 정답은 Rolling deployment아닐까..

159. An ecommerce startup is preparing for an annual sales event As the traffic to the company's application increases, the development team wants to be notified when the Amazon EC2 instance's CPU utilization exceeds 80%.
     Which solution will meet this requirement?

- **A. Create a custom Amazon CloudWatch alarm that sends a notification to an Amazon SNS topic when the CPU utilization exceeds 80%.**

172. 회사에서 AWS CodeBuild를 사용하여 AWS CodeCommit에 저장된 소스 코드에서 웹 사이트를 컴파일하고 있습니다. 소스 코드에 대한 최근 변경으로 인해 CodeBuild 프로젝트가 웹 사이트를 성공적으로 컴파일할 수 없었습니다.
     개발자는 실패의 원인을 어떻게 식별해야 합니까?

> A company is using AWS CodeBuild to compile a website from source code stored in AWS CodeCommit. A recent change to the source code has resulted in the CodeBuild project being unable to successfully compile the website.
> How should the Developer identify the cause of the failures?

- **C.** AWS CodeBuild 프로젝트 빌드 이력에서 마지막 빌드 시도에서 **실패한 단계의 빌드 로그를 확인**합니다.
-  Check the build logs of the failed phase in the last build attempt in the AWS CodeBuild project build history. In case of need of deep troubleshooting beyond log only then we need to run build process on local machine. Also this is not possible if the code remains on CodeCommit. Failed Build details can be accessed from project "Build history". Also for enabling cloudwatch (this can be done at the time of creating build project or even after creating the project through the console) we do not need to modify buildspec.yml at all(buildspec.yml is for mentioning build instructions) For enabling cloudwatch logs(if its not enabled already) just go to your build project==> edit==>logs and you will find below option: CloudWatch

174. 프런트 엔드 웹 애플리케이션은 Amazon Cognito 사용자 풀을 사용하여 사용자 인증 흐름을 처리합니다. 개발자가 JavaScript용 AWS SDK를 사용하여 Amazon DynamoDB를 애플리케이션에 통합하고 있습니다. 개발자가 액세스 또는 비밀 키를 노출하지 않고 API를 어떻게 안전하게 호출할 수 있습니까?

> A front-end web application is using Amazon Cognito user pools to handle the user authentication flow. A developer is integrating Amazon DynamoDB into the application using the AWS SDK for JavaScript How would the developer securely call the API without exposing the access or secret keys?

- **A.** Configure Amazon Cognito identity pools and exchange the JSON Web Token (JWT) for temporary credentials

176. 회사는 Amazon API Gateway를 사용하여 공개 API를 관리하고 있습니다. CISO는 API를 테스트 계정 사용자만 사용할 것을 요구합니다. 이 특정 AWS 계정의 사용자에 대한 API 액세스를 제한하는 가장 안전한 방법은 무엇입니까?

> A company is using Amazon API Gateway to manage its public-facing API. The CISO requires that the APIs be used by test account users only. What is the MOST secure way to restrict API access to users of this particular AWS account?

- **B.** API Gateway resource policies
- Amazon API Gateway resource policies are JSON policy documents that you attach to an API to control whether a specified principal (typically an IAM user or role) can invoke the API. You can use API Gateway resource policies to allow your API to be securely invoked by: Users from a specified AWS account. Specified source IP address ranges or CIDR blocks. Specified virtual private clouds (VPCs) or VPC endpoints (in any account). You can use resource policies for all API endpoint types in API Gateway: private, edge-optimized, and Regional.

177. Lambda 함수는 데이터를 다운스트림 서비스로 보내기 전에 데이터를 처리합니다. 각 데이터 조각의 크기는 약 1MB입니다. 보안 감사 후, 이제 함수 t]는 데이터를 다운스트림으로 보내기 전에 암호화해야 합니다. 수행하는 데 필요한 API 호출 암호화?

> A Lambda function processes data before sending it to a downstream service Each piece of data is approximately 1 MB in size After a security audit, the function t]is now required to encrypt the data before sending it downstream Which API call is required to perform the encryption?

- **B.** Use the KMS GenerateDataKey API to get an encryption key

178. An application running on multiple Amazon EC2 instances pulls messages ...SQS queue. A requirement for the application is that all messages must be encrypted at rest.
     Developers are instructed to use methods that allow for centralized .. possible support requirements whenever possible.
     Which of the following solution supports these requirements?

- **C.** **Create an SQS queue, and encrypt the queue by using server-side encryption with AWS KMS**

185. A company is launching an ecommerce website and will host the static data in Amazon S3. The company expects approximately 1 000 transactions per second (TPS) for GET and PUT requests in total. Logging must be enabled to track all requests and must be retained for auditing purposes.
     What is the MOST cost-effective solution?

- **D.** Enable S3 server access logging and create a lifecycle policy to move the data to Amazon S3 Glacier in
  90 days.

189. A company wants to migrate an imaging service to Amazon EC2 while following security best practices. The images are sourced and read from a non-public Amazon S3 bucket.
     What should a developer do to meet these requirements?

- **C.Create an EC2 service role with read-only permissions for the S3 bucket Attach the role to the EC2 instance**

- As an AWS security best practice, you should not create an IAM user and pass the user's credentials to the application or embed the credentials in the application. Instead, create an IAM role that you attach to the EC2 instance to give temporary security credentials to applications running on the instance. When an application uses these credentials in AWS, it can perform all of the operations that are allowed by the policies attached to the role.So for the given use-case, you should create an IAM role with read-only permissions for the S3 bucket and apply it to the EC2 instance profile.