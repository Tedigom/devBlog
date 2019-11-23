이번 시간에는 MSA의 Outer Architecture 중 Backing Service에 대해 알아보도록 하겠습니다.


# Backing service
우선 Backing Service란, 어플리케이션이 실행되는 가운데 네트워크를 통해서 사용할 수 있는 모든 서비스를 말하며 My SQL과 같은 데이터베이스, 캐쉬 시스템, SMTP 서비스 등 어플리케이션과 통신하는 attached Resource들을 지칭하는 포괄적인 개념입니다.

### 마이크로서비스 Backing service의 특징

마이크로 서비스에서의 Backing service는 메세지큐를 활용한 비동기 통신 패턴을 많이 사용합니다. 현대의 MSA의 특징 중 하나는 하나의 Micro Service에 이벤트(장애 발생, 트래픽 증가, 소스 반영 등)가 발생할 경우, Micro Service 오케스트레이션이 진행되며, 마이크로서비스의 신규 생성, 재생성, 서비스 인스턴스의 삭제 등의 작업이 빈번하게 이루어진다는 것입니다. 

![msa pattern.jpg](https://images.velog.io/post-images/tedigom/09405d40-0dbb-11ea-af24-7bccb2a7b17c/msa-pattern.jpg)

그림과 같이 하나의 비즈니스 프로세스를 수행하기 위해 여러 마이크로 서비스간 통신이 필요한 경우를 생각해보겠습니다.

모놀리틱에서와 같이 하나의 트랜잭션에서 여러 마이크로 서비스들이 강하게 결합되어 처리되는 방식의 경우, Orchestration이 진행되면서 진행 중인 트랜잭션이 끊어지게 되고, 해당 서비스 요청을 보존할 수 없게 됩니다.

MSA에서는 Message queue를 활용하여 트랜잭션을 분리하는 전략을 많이 취합니다. 특히 Message queue를 사용할 경우 서비스의 영속성( 서비스에 장애가 발생하더라도 event message가 consumer에 전달되는 것이 보장됨 )을 유지할 수 있다는 장점이 있습니다. 

