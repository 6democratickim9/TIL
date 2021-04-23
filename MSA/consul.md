## 공식문서 보고 정리하는 Consul

#### 1. 시작하기

- 컨설 다운로드
- 컨설.exe 설치된 곳으로 간다
- conda activate msa(내가 가진 가상환경 구동)
- ![image-20210423064011945](C:\Users\MIN\AppData\Roaming\Typora\typora-user-images\image-20210423064011945.png)

해당 명령어로 실행



#### 2. 서비스 정의하기

``` mkdir ./consul.dconfigurationㄴ게```

- .d는 해당 디렉토리가 일련의 config 파일들을 가지고 있다는 뜻
- 서비스를 정의하는 구성 파일 작성하기
- 포트 80번에 "web" 이라는 이름의 서비스가 돌아간다고 가정한다
- consul.d 에 들어가 web.json 이라는 이름의 파일을 만든다

--> 해당 파일에는 이름, 포트, 옵션으로 들어갈 태그가 나중에 서비스를 찾을 때 사용하기 위해 해당 서비스를 정의하는 파일에 들어가게 될 것

```json
echo '{
  "service": {
    "name": "web",
    "tags": [
      "rails"
    ],
    "port": 80
  }
}' > ./consul.d/web.json
```

다 만들고 나면 에이전트 재실행하기

- configuration 디렉토리를 지정하고 스크립트 체크를 사용 가능하게 하기 위해 에이전트에서 커맨드 라인 플래그를 사용하도록 한다.

- 스크립트 체크는 멜웨어와 같은 보안상의 문제를 일으킬 수 있으므로  ```-enable-local-script-checks```를  강하게 권장하는 바이다

- .... 머리가 안돌아가서 자꾸 이상한짓을 하네ㅠ

  

```
$ consul agent -dev -enable-script-checks -config-dir=./consul.d
==> Starting Consul agent...
           Version: 'v1.5.2'
           Node ID: '82f64bfa-22c2-5727-0f5d-0bae376f6584'
         Node name: 'Judiths-MBP.lan'
        Datacenter: 'dc1' (Segment: '<all>')
            Server: true (Bootstrap: false)
       Client Addr: [127.0.0.1] (HTTP: 8500, HTTPS: -1, gRPC: 8502, DNS: 8600)
      Cluster Addr: 127.0.0.1 (LAN: 8301, WAN: 8302)
           Encrypt: Gossip: false, TLS-Outgoing: false, TLS-Incoming: false, Auto-Encrypt-TLS: false

==> Log data will now stream in as it occurs:

...

2019/07/16 14:09:25 [INFO] agent: Synced service "web"
2019/07/16 14:09:25 [DEBUG] agent: Node info in sync
2019/07/16 14:09:25 [DEBUG] agent: Service "web" in sync
2019/07/16 14:09:25 [DEBUG] agent: Node info in sync
```

이제 ``` agent: Synced service "web" ``` 를 보자.

consul이 웹 서비스를 싱크한 것을 알 수 있다.

- 이 것은 에이전트가 configuration 파일들을 통해 서비스 정의를 로드한 것을 뜻하고, 서비스 카탈로그 또한 성공적으로 등록한 것을 알 수 있음
- 알아둘 것
  - 우리는 해당 예시에서 웹서비스를 시작한 적이 없다. 컨설은 아직 기동되지 않은 서비스를 등록할 수 있다. 이것은 해당 서비스의 포트에 기반하여 등록과 함께 기동되는 서비스를 상관짓는다.
- 다수의 컨설 데이터센터에서는 각 서비스는 로컬 컨설 클라이언트를 등록하고, 클라이언트들은 서비스 카탈로그를 포함하는 등록(registration)을 컨설 서버에 전달한다.



- #### 쿼리 서비스

  - 에이전트가 서비스를 영사의 서비스 카탈로그에 추가하면 DNS 인터페이스 또는 HTTP API를 사용하여 서비스를 쿼리할 수 있습니다.



- 먼저 Consul의 DNS 인터페이스를 사용하여 웹 서비스를 쿼리합니다. Consul에 등록된 서비스의 DNS 이름은 ```NAME.service.consul```입니다. 여기서 ```NAME```는 서비스를 등록하는 데 사용한 이름입니다(이 경우 ```web```). 기본적으로 모든 DNS 이름은 ```consul```네임스페이스에 있지만 config될 수 있음
- 웹 서비스의 정규화된 도메인 이름은 ```web.service.consul```입니다. 등록된 서비스의 DNS 인터페이스(포트 ```8600```에서 기본적으로 실행되는 컨설)를 쿼리합니다.

```
dig @127.0.0.1 -p 8600 web.service.consul
```

- 윈도우에서는 @와 -p를 뺍니당
- ![image-20210423070849269](C:\Users\MIN\AppData\Roaming\Typora\typora-user-images\image-20210423070849269.png)

이러케 실행됨

(이제 귀찮아서 거의 다 파파고 돌릴 예정)

- 출력에서 확인할 수 있듯이 서비스가 등록된 IP 주소가 포함된 A 레코드가 반환되었습니다. 
- 레코드는 IP 주소만 저장할 수 있습니다.

### 팁

- 최소한의 구성으로 consul을을 시작했으므로 A 레코드는 로컬 호스트(127.0.0.1)를 반환합니다. 
- 데이터 센터의 다른 노드에 의미 있는 IP 주소를 알리려면 서비스 정의에서 Commer 에이전트 ```- advertise``` 인수 또는```address``` 필드를 설정하십시오.

- 또한 사용자는 DNS 인터페이스를 사용하여 SRV 레코드로 전체 주소/포트 쌍을 검색한다. 

```MacOS
dig @127.0.0.1 -p 8600 web.service.consul SRV
```

```windows
dig 127.0.0.1 8600 web.service.consul SRV
```

![image-20210423071410894](C:\Users\MIN\AppData\Roaming\Typora\typora-user-images\image-20210423071410894.png)

SRV 레코드는 80번 포트에서 ```Judiths-MBP.lan.node.dc1.consul``` 라는 노드 위에 존재하고 있음을 보여준다.

- 추가적인 섹션은 해당 노드를 위해 A레코드와 함꼐 DNS에 의해 반환됨



마지막으로, DNS 인터페이스를 사용하여 사용자는 태그를 통해 서비스를 필터링 할 수 있다.

태그 베이스의 서비스 쿼리를 위한 포맷은 ```TAG.NAME.service.consul```  이다.

- 하단의 예시를 보면, 사용자는 모든 웹 서비스에 대한 "rails" 태그에 대해 찾을 것

- 사용자는 해당 태그와 함께 웹 서비스를 등록해뒀다면 성공적인 response를 받을 수 있음

- ###  SRV 레코드

  - SRV 레코드는 SRV(서비스 로케이터) 리소스 레코드
  - 유사한 TCP/IP 기반 서비스를 제공하는 여러 서버를 단일 DNS 쿼리 동작을 사용하여 찾음
  - 레코드를 사용하여 잘 알려진 서버 포트 및 전송 프로토콜 종류에 대한 서버 목록을 DNS 도메인 이름의 우선 순위로 정렬하여 관리 가능

![image-20210423072059953](C:\Users\MIN\AppData\Roaming\Typora\typora-user-images\image-20210423072059953.png)

DNS 인터페이스뿐만 아니라 HTTP API를 사용하여 서비스를 쿼리할 수도 있습니다.





## Register the service and proxy with Consul

