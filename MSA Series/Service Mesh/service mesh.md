이번에는 Outer Architecture 중 Service Mesh에 대한 이야기입니다.

# Service Mesh
Service Mesh는 쉽게말해 서비스 간의 통신(네트워크)을 담당하는 요소입니다.

마이크로 서비스 구성 요소간 상호 통신을 위해서는 Service Discovery, 서비스 라우팅, Failure recovery, load balancing(트래픽 관리), 보안 등의 문제를 처리할 수 있는 메커니즘이 필요합니다. 

Service Mesh는 통신 및 네트워크 기능을 비즈니스 로직과 분리한 네트워크 통신 인프라입니다.모든 서비스의 인프라 레이어로서 서비스들 간의 통신을 처리하며, 위의 언급된 많은 기능들을 포함하고 있습니다.


### API Gateway도 비슷한 기능이 있지 않았나요?

이전 포스팅에서 API Gateway에서도 Service Discovery, 라우팅, 트래픽 관리와 같은 비슷한 기능을 담당한다고 말씀드렸습니다.

[MSA 제대로 이해하기 -(3)API Gateway](https://velog.io/@tedigom/MSA-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-3API-Gateway-nvk2kf0zbj)

그럼 API Gateway와 Service Mesh는 무엇이 다른걸까요? 

* 적용되는 위치
API Gateway는 마이크로서비스 그룹의 외부 경계에 위치하여 역할을 수행하지만, ServiceMesh는 경계 내부에서 그 역할을 수행합니다.

* 아키텍쳐 형태
API Gateway가 중앙집중형 아키텍쳐여서 SPOF(Single Point of Failure)을 생성한다면, Service Mesh는 분산형 아키텍쳐를 취하기 때문에 SPOF를 생성하지 않고 확장이 용이합니다.

#  
이외에 기능적인 측면에서의 차이점은 아래의 표에서와 같습니다.
##  

최근 MSA에서 API Gateway는 노출되는 부분(External)에 위치하여 내부서비스를 보호 및 제어하는 역할을 하고, Service Mesh는 내부 서비스(Internal)에 위치하여 서비스를 관리하는 구조로 많이 사용되고 있습니다.

![servicemesh apigateway.png](https://images.velog.io/post-images/tedigom/87e37700-083d-11ea-bf9d-db5436d09a81/servicemesh-apigateway.png)
그림 출처 : [Service Mesh vs API Gateway](https://medium.com/microservices-in-practice/service-mesh-vs-api-gateway-a6d814b9bf56)
