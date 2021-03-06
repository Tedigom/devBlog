이번에는 Outer Architecture 중 Service Mesh에 대한 이야기입니다.

# Service Mesh
Service Mesh는 쉽게말해 마이크로 서비스 간의 통신(네트워크)을 담당하는 요소입니다.

마이크로 서비스 구성 요소간 상호 통신을 위해서는 Service Discovery, 서비스 라우팅, Failure recovery, load balancing(트래픽 관리), 보안 등의 문제를 처리할 수 있는 메커니즘이 필요합니다. 

Service Mesh는 통신 및 네트워크 기능을 비즈니스 로직과 분리한 네트워크 통신 인프라입니다.모든 서비스의 인프라 레이어로서 서비스들 간의 통신을 처리하며, 위의 언급된 많은 기능들을 포함하고 있습니다.


![service-mesh-generic-topology.png](https://images.velog.io/post-images/tedigom/3fbe7db0-0925-11ea-aa94-f3699ad0167a/service-mesh-generic-topology.png)


### API Gateway도 비슷한 기능이 있지 않았나요?

이전 포스팅에서 API Gateway에서도 Service Discovery, 라우팅, 트래픽 관리와 같은 비슷한 기능을 담당한다고 말씀드렸습니다.

[MSA 제대로 이해하기 -(3)API Gateway](https://velog.io/@tedigom/MSA-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-3API-Gateway-nvk2kf0zbj)

그럼 API Gateway와 Service Mesh는 무엇이 다른걸까요? 

* 적용되는 위치
API Gateway는 마이크로서비스 그룹의 외부 경계에 위치하여 역할을 수행하지만, ServiceMesh는 경계 내부에서 그 역할을 수행합니다.

* 아키텍쳐 형태
API Gateway가 중앙집중형 아키텍쳐여서 SPOF(Single Point of Failure)을 생성한다면, Service Mesh는 분산형 아키텍쳐를 취하기 때문에 SPOF를 생성하지 않고 확장이 용이합니다.

* 패턴
API Gateway는 일반적으로 Gateway proxy pattern을 사용해서 수행됩니다. Consumer(호출자)은 구현 내용을 알 필요 없이 Gateway를 호출하는 방법만 알면 Gateway가 알아서 수행해주는 방식입니다.  
반면, Service Mesh는 일반적으로 Sidecar proxy pattern을 사용합니다. Consumer(호출자)의 코드에는 Provider(공급자)의 주소를 찾는방법, failover와 관련된 코드 등의 내용이 들어가게 됩니다. 다만, 호출자의 코드는 어플리케이션 코드(비즈니스 로직)에 내장되는 것이 아니라 sidecar 형태로 별개로 관리됩니다.  

#  
이외의 차이점에 대해서는 아래의 표에 정리해 보았습니다.

|             |  API Management |  Service Mesh |
|:--------:|:--:|:--:|
|라우팅 주체 | 서버 |요청하는 서비스|
|라우팅 구성요소 | 별도의 네트워크를 도입하는 독립적인 API gateway 구성요소 |서비스 내 sidecar로 Local network 스택의 일부가 됨|
|로드 밸런싱 | 단일 엔드포인트를 제공하고, API Gateway 내 로드밸런싱을 담당하는 구성요소에 요청을 redirection하여 해당 구성요소가 처리함 |Service Registry에서 서비스 목록을 수신함. sidecar에서 로드밸런싱 알고리즘을 통해 수행함|
|네트워크 | 외부 인터넷과 내부 서비스 네트워크 사이에 위치함 |내부 서비스 네트워크 사이에 위치하며, 응용프로그램의 네트워크 경계 내에서만 통신을 가능하게 함|
|분석 | API에 대한 사용자 및 공급자에 대한 모든 호출에 대해 수집되고 분석됨|Mesh 내 모든 마이크로서비스 구성요소에 대해 분석가능 |


##  

최근 MSA에서 API Gateway는 노출되는 부분(External)에 위치하여 내부서비스를 보호 및 제어하는 역할을 하고, Service Mesh는 내부 서비스(Internal)에 위치하여 서비스를 관리하는 구조로 많이 사용되고 있습니다.

![servicemesh apigateway.png](https://images.velog.io/post-images/tedigom/87e37700-083d-11ea-bf9d-db5436d09a81/servicemesh-apigateway.png)
그림 출처 : [Service Mesh vs API Gateway](https://medium.com/microservices-in-practice/service-mesh-vs-api-gateway-a6d814b9bf56)

## Service Mesh의 종류

![99C7FC335C70279E01.png](https://images.velog.io/post-images/tedigom/f8a13e00-0928-11ea-b582-93c0e6ad9fde/99C7FC335C70279E01.png)

Service mesh는 현재 크게 세가지 유형으로 구분할 수 있습니다.

**1) PaaS (Platform as a Service)의 일부로 서비스 코드에 포함되는 유형**  
Microsoft Azure Service fabric, lagom, SENECA 등이 이 유형에 해당되며, 프레임워크 기반의 프로그래밍 모델이기 때문에, 서비스메쉬를 구현하는데에 특화된 코드가 필요합니다. ( Mesh-native Code )

**2) 라이브러리로 구현되어 API 호출을 통해 Service mesh에 결합되는 유형**  
Spring Cloud, Netflix OSS(Ribbon/Hystrix/Eureka/Archaius), finagle 등이 이 유형에 해당되며, 프레임워크 라이브러리를 사용하는 형태입니다. 이중 Netfilix의 Prana는 sidecar 형태로 동작합니다. 서비스 메시를 이해하고 코드를 작성해야합니다. (Mesh Aware Code) 

**3) Side car proxy를 이용하여 Service mesh를 마이크로서비스에 주입하는 유형**  
Istio/Envoy, Consul, Linkerd 등이 이 유형에 해당되며, sidecar proxy 형태로 동작됩니다. 따라서 서비스메시와 무관하게 코드를 작성할 수 있습니다.


### Sidecar pattern?

![sidecar.png](https://images.velog.io/post-images/tedigom/ac3a3bd0-092c-11ea-8263-c5a6e835ad0d/sidecar.png)
Sidecar pattern은 (컨테이너 배포방식의 경우) 모든 응용 프로그램 컨테이너에 추가로 sidecar 컨테이너가 배포됩니다. Sidecar는 서비스에 들어오거나 나가는 모든 네트워크 트래픽을 처리하게 됩니다. 가장 큰 특징은, 비즈니스 로직이 포함된 실제 서비스와 sidecar이 병렬로 구성되어있기 때문에, 서비스 호출에서 서비스가 직접 서비스를 호출하는 것이 아니라 proxy 를 통해서 호출하게됩니다. 

따라서, 대규모의 마이크로서비스 환경이라고 하여도 개발자가 별도의 작업 없이 서비스의 연결 뿐만 아니라, 로깅, 모니터링, 보안, 트래픽 제어와 같은 다양한 이점을 누릴 수 있습니다.

최근의 Service Mesh는 Sidecar pattern 유형이 recommended 되고 있는 추세입니다.


## Service Mesh의 주요 기능
일반적으로, Istio나 consul, Linkerd와 같은 Service Mesh 프레임워크들은 다음과 같은 기능들을 지원하고 있습니다.

* Service Discovery
* Load balancing (지연시간 기반 / 대기열 기반 )
* Dynamic Request Routing
* Circuit Breaking
* 암호화 (TLS)
* 보안
* Health check, Retry and Timeout
* Metric 수집 
 
