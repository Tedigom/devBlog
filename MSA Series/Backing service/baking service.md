이번 시간에는 MSA의 Outer Architecture 중 Backing Service에 대해 알아보도록 하겠습니다.


# Backing service
우선 Backing Service란, 어플리케이션이 실행되는 가운데 네트워크를 통해서 사용할 수 있는 모든 서비스를 말하며 My SQL과 같은 데이터베이스, 캐쉬 시스템, SMTP 서비스 등 어플리케이션과 통신하는 attached Resource들을 지칭하는 포괄적인 개념입니다.

### 마이크로서비스 Backing service의 특징

마이크로 서비스에서의 Backing service는 메세지큐를 활용한 비동기 통신 패턴을 많이 사용합니다. 현대 MSA의 특징 중 하나는 하나의 Micro Service에 이벤트(장애 발생, 트래픽 증가, 소스 반영 등)가 발생할 경우, Micro Service 오케스트레이션이 진행되며, 마이크로서비스의 신규 생성, 재생성, 서비스 인스턴스의 삭제 등의 작업이 빈번하게 이루어진다는 것입니다. 

![msa pattern.jpg](https://images.velog.io/post-images/tedigom/09405d40-0dbb-11ea-af24-7bccb2a7b17c/msa-pattern.jpg)

그림과 같이 하나의 비즈니스 프로세스를 수행하기 위해 여러 마이크로 서비스간 통신이 필요한 경우를 생각해보겠습니다.

하나의 트랜잭션에서 여러 마이크로 서비스들이 강하게 결합되어 처리되는 방식의 경우, Orchestration이 진행되면서 진행 중인 트랜잭션이 끊어지게 되고, 해당 서비스 요청을 보존할 수 없게 됩니다.

MSA에서는 Message queue를 활용하여 트랜잭션을 분리하는 전략을 많이 취합니다. 특히 Message queue를 사용할 경우 서비스의 영속성( 서비스에 장애가 발생하더라도 event message가 consumer에 전달되는 것이 보장됨 )을 유지할 수 있다는 장점이 있습니다. 
#  
# Message queue
일반적인 웹서비스에서 서버-클라이언트 사이의 통신은 결합도가 높은 구조이며, 동기방식으로 작동합니다. 이와 같은 방식은 시스템 내 요소들 간에 의존성이 높아 시스템에 많은 영향을 끼치며, 유연성이 낮습니다.

서비스 간 결합도가 낮아야 하는 MSA에서 데이터의 송수신 방법으로는 **비동기**방식으로 메시지를 사용하는 것이 효율적입니다. Message Queue(MQ)는 메세지를 발행하는 생산자(producer, publisher) 와 메세지를 받는 소비자(consumer, subscriber) 사이에 위치하는 매개체역할을 수행하는 미들웨어입니다.


![messagequeue.png](https://images.velog.io/post-images/tedigom/d1465930-1698-11ea-873a-2119d5583619/messagequeue.png)

분산된 마이크로서비스 간에 Message queue를 이용하여 비동기 방식으로 통신하는 것은 다음과 같은 특징을 가집니다.
* **비동기 / 약결합**
* **Redundancy** : 서비스가 실패하더라도 재처리를 할 수 있습니다.
* **Resilence** : 전체 시스템에 대한 영향이 적고, 회복 탄력성이 높습니다.
* **보장성** : Message Queue에 들어간 Message는 최소 한번은 처리됩니다.
* **확장성** : 다수의 Message queue를 두어 많은 요청에 대해 유연하게 확장할 수 있습니다.


#   

## Apache Kafka
Kafka는 Pub/Sub 구조에 특화된 메세지 큐이고, 분산 환경에 특화되어 설계되어있습니다. RabbitMQ나, ActiveMQ에 비해 높은 처리량, 및 성능을 가지고 있습니다. 


![kafkaCluster.png](https://images.velog.io/post-images/tedigom/fe046520-18f0-11ea-b856-7f9c87a20e1c/kafkaCluster.png)

### Apache Kafka의 특징
* 대용량 및 실시간 처리에 특화되어있습니다.
* 단순한 TCP 기반의 프로토콜을 사용함으로 오버헤드가 적습니다.
* 메모리가 아닌 파일시스템에 메세지를 저장합니다.
* OS에서 처리하는 페이지 캐시를 이용함으로써 속도가 빠릅니다.
* consumer가 pull 방식으로 메세지를 받으며, batch 처리가 가능합니다.
