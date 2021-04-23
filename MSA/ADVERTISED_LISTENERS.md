https://www.confluent.io/blog/kafka-listeners-explained/

## KAFKA_ADVERTISED_LISTENERS

- 도커 이미지 쓸거면 이거 쓰기

- 이거 있어야 외부 주소로 노출해서 클라이언트가 연결시킴 -> 안그러면 내부 호스트 주소로 연결돼는데 만약에 도달 못하면 그게 문제가 되는것

- 일단 LISTENER이 카프카가 묶는 인터페이스고, ADVIERTSED_LISTENERS는 클라이언트가 연결 가능하게 만드는거라고 합니다.

  ​			-------------------------------------------------------- 생략 ----------------------------------------------------------------

- 중요한 것은 클라이언트를 실행할 때 해당 클라이언트를 전달하는 브로커가 어디로 이동하는지와 클러스터의 브로커에 대한 메타데이터를 얻는다는 것입니다.

- 데이터 읽기/쓰기를 위해 연결하는 실제 호스트와 IP는 브로커가 초기 연결에서 다시 전달하는 데이터를 기반으로 합니다. 단 하나의 노드이고 브로커가 반환하는 데이터도 연결된 호스트와 동일합니다.

- 이 것을 올바르게 구성하기 위해서는 당신은 카프카 브로커가 다수의 리스너들을 가질 수 있다는 것을 이해해야 합니다. 리스너는 

  1. Host/IP
  2. Port
  3. Protocol

- 세 가지로 구성되어 있습니다.

- config를 살펴봅시다. 프로토콜이 listner name으로도 사용되곤 하지만, 이름을 추상적이게 사용함으로써 리스너를 위해 조금 더 명확하고 깔끔하게 만들어봅시다.

  ```
  KAFKA_LISTENERS: LISTENER_BOB://kafka0:29092,LISTENER_FRED://localhost:9092
  KAFKA_ADVERTISED_LISTENERS: LISTENER_BOB://kafka0:29092,LISTENER_FRED://localhost:9092
  KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: LISTENER_BOB:PLAINTEXT,LISTENER_FRED:PLAINTEXT
  KAFKA_INTER_BROKER_LISTENER_NAME: LISTENER_BOB
  
  ```

  

- server.properties 를 바로 사용한다면(AWS에서 처럼) Docker config name를 아래와 같이 사용하시오:

  - ```KAFKA_LISTENERS```는 수신기와 수신을 위해 Kafka가 바인딩하는 호스트/IP 및 포트의 쉼표로 구분된 목록입니다. 보다 복잡한 네트워킹의 경우 시스템의 지정된 네트워크 인터페이스와 연결된 IP 주소일 수 있습니다. 기본값은 0.0.0.0으로, 모든 인터페이스에서 수신을 의미합니다.
  - listeners
  - ```KAFKA_ADPERTIZED_LISTERS```는 호스트/IP와 포트를 사용하여 수신기를 쉼표로 구분한 목록입니다. 이 메타데이터는 클라이언트에 다시 전달됩니다.
  - `advertised.listeners`
  - ```KAFKA_LISTENER_SECURE_PROTOCOL_MAP``는 수신기 이름당 사용할 보안 프로토콜에 대한 키/값 쌍을 정의합니다.
  - `listener.security.protocol.map`

- kafka broker은 이들 사이에서 통신하며 주로 내부 네트워크 내에서 작동됩니다. 어떤 리스너를 사용할지 정의한다면, ```KAFKA_INTER_BROKER_LISTENER_NAME(inter.broker.listener.name)``` 를 명시하세요

- 사용된 호스트/IP는 브로커 컴퓨터에서 다른 컴퓨터로 액세스할 수 있어야 합니다.

  ​			-------------------------------------------------------- 생략 ----------------------------------------------------------------

  

## HOW TO: Connecting to Kafka on Docker

- `advertised.listeners` 를 세팅하는 것이 우리의 네트워크에 훨씬 도움됩니다!

- 카프카를 돌리려면 두 개의 리스너를 구성해야 합니다

  1. 도커 네트워크 내의 통신: 이는 브로커 간 통신(즉, 브로커 간)일 수 있으며, 카프카 커넥트나 제3자 클라이언트 또는 생산자와 같은 도커에서 실행되는 다른 구성요소 간의 통신일 수 있다.이러한 통신의 경우 도커 컨테이너의 호스트 이름을 사용해야 합니다. 동일한 도커 네트워크의 각 도커 컨테이너는 카프카 브로커 컨테이너의 호스트 이름을 사용하여 도달합니다.

  2. 도커를 사용하지 않는 네트워크 트래픽: 이 것은 클라이언트가 로컬에서 도커 호스트 머신을 돌리는 것일 수 있음. 예를 들어, 사용자들이 도커 컨테이너에서 외부로 노출된 포트를 ```localhost```에서 연결한다고 가정해보자

     ```dockerfile
     kafka0:
         image: "confluentinc/cp-enterprise-kafka:5.2.1"
         ports:
           - '9092:9092'
           - '29094:29094'
         depends_on:
           - zookeeper
         environment:
           […]
           # For more details see See https://rmoff.net/2018/08/02/kafka-listeners-explained/
           KAFKA_LISTENERS: LISTENER_BOB://kafka0:29092,LISTENER_FRED://kafka0:9092,LISTENER_ALICE://kafka0:29094
           KAFKA_ADVERTISED_LISTENERS: LISTENER_BOB://kafka0:29092,LISTENER_FRED://localhost:9092,LISTENER_ALICE://never-gonna-give-you-up:29094
           KAFKA_LISTENER_SECURITY_PROTOCOL_MAP: LISTENER_BOB:PLAINTEXT,LISTENER_FRED:PLAINTEXT,LISTENER_ALICE:PLAINTEXT
           KAFKA_INTER_BROKER_LISTENER_NAME: LISTENER_BOB
     ```

     - 도커에 있는 클라이언트들은 ```BOB```라는 리스너를 사용하여 연결하고, 포트 29092와 ```kafka0``` 라는 이름의 호스트를 사용한다. 이렇게 함으로써 그들은 호스트이름을 kafka0 로 연결할 때 반환받는다. 각 Docker 컨테이너는 Docker의 내부 네트워크를 사용하여 kafka0을 해결하고 브로커와 연결할 수 있습니다.
     - 도커 네트워크 외부의 클라이언트들은 ```FRED```라는 리스너를 사용하여 연결하는데, 포트 9092번과 ```localhost```라는 이름의 호스트명을 사용한다. 포트 9092는 도커 컨테이너에 의해 외부로 노출되고 그렇게 함으로써 연결이 가능해진다. 클라이언트가 연결되면 브로커의 메타데이터에 대한 호스트 이름 localhost가 제공되므로 데이터를 읽거나 쓸 때 이 호스트에 연결합니다.
     - 위의 구성에서는 Docker 외부 클라이언트와 호스트 시스템의 외부 클라이언트가 연결하려는 시나리오를 처리하지 않습니다. 그 이유는 kafka0(내부 Docker 호스트 이름)이나 localhost(Docker 호스트 시스템의 루프백 주소) 모두 확인할 수 없기 때문입니다.

## HOW TO: Connecting to Kafka on AWS/IaaS

- AWS 에서도 도커와 같은 방식으로 진행됩니다. 가장 큰 차이점은 Docker의 경우 외부 연결은 로컬 호스트(상기처럼)에 있을 수 있지만, 클라우드 호스트 Kafka(예: AWS)의 경우 외부 연결은 브로커의 로컬이 아닌 시스템에서 이루어지며 브로커에 연결할 수 있어야 한다는 것입니다.
- 더 큰 문제는 Docker 네트워크가 호스트와 상당히 분리되어 있지만 IaaS에서는 종종 외부 호스트 이름을 내부적으로 확인할 수 있어 실제로 이러한 문제가 발생할 수 있는 시기를 놓치게 된다는 것입니다.
- 두 가지 접근 방법이 있다: 브로커에 연결할 외부 주소도 네트워크의 모든 브로커(예: VPC)에서 로컬로 확인할 수 있는지 여부에 따라 달라집니다.

![image-20210423213234622](C:\Users\MIN\AppData\Roaming\Typora\typora-user-images\image-20210423213234622.png)

여기서 PLAINTEXT 라고 불리는 존재하는 리스너를 사용/ 외부에 노출된(advertised) 호스트 이름(즉, 인바운드 클라이언트에 전달되는 호스트 이름)을 설정하기 위해 재정의하기만 하면 됩니다.

```
advertised.listeners=PLAINTEXT://ec2-54-191-84-122.us-west-2.compute.amazonaws.com:9092

```

내부적, 외부적으로 사용될 새로운 연결은 ```ec2-54-191-84-122.us-west-2.compute.amazonaws.com``` 를 사용할것입니다. 왜냐면 ec2-54-191-84-122.us-west-2.compute.amazonaws.com 는 로컬로나 외부적으로나 잘 확인되니까영

### **Option 2: External address is NOT resolvable locally**

1. VPC 내부에서 통신: 이는 브로커 간 통신(즉, 브로커 간)과 카프카 커넥트 또는 타사 클라이언트 또는 생산자와 같은 VPC에서 실행되는 다른 구성요소 간의 통신일 수 있다.이러한 통신의 경우, 우리는 EC2 시스템의 내부 IP(또는 DNS가 구성된 경우 호스트 이름)를 사용해야 합니다.

2. AWS 트래픽 외부: 이것은 노트북 또는 단순히 아마존에서 호스팅되지 않은 기계로부터 연결을 테스트하는 것일 수 있다. 두 경우 모두 인스턴스의 외부 IP를 사용해야 합니다(또는 DNS가 구성된 경우 호스트 이름 사용).

![image-20210423214107088](C:\Users\MIN\AppData\Roaming\Typora\typora-user-images\image-20210423214107088.png)

```
listeners=INTERNAL://0.0.0.0:19092,EXTERNAL://0.0.0.0:9092
listener.security.protocol.map=INTERNAL:PLAINTEXT,EXTERNAL:PLAINTEXT
advertised.listeners=INTERNAL://ip-172-31-18-160.us-west-2.compute.internal:19092,EXTERNAL://ec2-54-191-84-122.us-west-2.compute.amazonaws.com:9092
inter.broker.listener.name=INTERNAL
```

## Exploring listeners with Docker

https://github.com/rmoff/kafka-listeners

- 여기 참고해보길. 여기에 여러 개의 리스너들로 구성된 카프카 브로커와 함께 도커 컴포즈가 주키퍼 인스턴스를 가져오는 것을 포함하고 있음

  - 도커 네트워크의 내부 트래픽을 위한 listener```BOB```(port29092)

  - ```
    $ docker-compose exec kafkacat \
            kafkacat -b kafka0:29092 \
            -L
    Metadata for all topics (from broker 0: kafka0:29092/0):
    1 brokers:
      broker 0 at kafka0:29092
    ```

  - 도커 호스트 머신의 트래픽을 위한 Listener```FRED```(port9092) 

  - ```
    $ docker-compose exec kafkacat \
            kafkacat -b kafka0:9092 \
                    -L
    Metadata for all topics (from broker -1: kafka0:9092/bootstrap):
    1 brokers:
      broker 0 at localhost:9092
    ```

  - 외부의 트래픽을 위한Listener `ALICE` (port 29094) DNS name `never-gonna-give-you-up`

  - ```
    $ docker run -t --network kafka-listeners_default \
                confluentinc/cp-kafkacat \
                kafkacat -b kafka0:29094 \
                        -L
    Metadata for all topics (from broker -1: kafka0:29094/bootstrap):
    1 brokers:
      broker 0 at never-gonna-give-you-up:29094
    ```

    

