지난 포스팅에서 MSA를 구성하는 아키텍처 요소에 대해 살펴보았습니다. Inner Architecture와 Outer Architecture로 나누어 설명을 드렸었죠. 

[MSA 제대로 이해하기 - (2)아키텍처 개요](https://velog.io/@tedigom/MSA-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-2-MSA-Outer-Architecure)

오늘은 그 중 Outer Architecture에서도 API Gateway에 대해 설명하려 합니다.

## API Gateway의 필요성



![concept1.PNG](https://images.velog.io/post-images/tedigom/5ae7a9e0-ff02-11e9-929b-8bdd0f9b8460/concept1.PNG)

MSA는 큰 서비스를 잘게 쪼개어 개발/운영 하는 아키텍처입니다. 하나의 큰 서비스는 수십~수백개의 작은 서비스로 나뉘어지며, 만약 이를 클라이언트에서 서비스를 직접 호출하는 형태라면 다음과 같은 문제점이 생길 수 있습니다.

* 각각의 서비스마다 인증/인가 등 공통된 로직을 구현해야하는 번거로움이 있습니다.
* 수많은 API 호출을 기록하고 관리하기가 어렵습니다.
* 클라이언트에서 여러 마이크로 서비스에 대한 번거로운 호출을 해야합니다.
* 내부의 비즈니스 로직이 드러나게 되어 보안에 취약해집니다.

특히 이러한 문제점들은 마이크로 서비스의 갯수가 많아질 수록 기하급수적으로 늘어나게 될 것입니다. 

###  

어느 규모 이상의 마이크로 서비스 기반 어플리케이션에는 API Gateway를 도입하는 것이 효율적입니다.


![concept2.PNG](https://images.velog.io/post-images/tedigom/4e85f7b0-ffca-11e9-86a4-6bfda3e4890b/concept2.PNG)

API Gateway는 API 서버 앞단에서 모든 API 서버들의 엔드포인트를 단일화 해주는 또다른 서버입니다. API에 대한 인증과 인가 기능을 가지고 있으며, 메세지의 내용에 따라 어플리케이션 내부에 있는 마이크로 서비스로 라우팅하는 역할을 담당합니다.

> _API Gateway의 시작은 SOA의 핵심 인프라라고 할 수 있는 ESB(Enterprise Service Bus)에서 시작되었습니다. 따라서 API Gateway의 많은 부분들이 ESB로 부터 승계되었습니다._
_ESB가 SOAP/XML 기반의 무거운 기능을 가졌다면, API Gateway는 REST/JSON 기반으로 보다 가볍게 설계된 것이 특징입니다._
