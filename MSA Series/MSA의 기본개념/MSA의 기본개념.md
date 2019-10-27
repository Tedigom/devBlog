


![lego-708086_1920.jpg](https://images.velog.io/post-images/tedigom/c2875230-f8b8-11e9-a757-dd517f114496/lego-7080861920.jpg)
마이크로 서비스 아키텍쳐를 한마디로 다음과 같이 표현할 수 있습니다.

_**"하나의 큰 어플리케이션을 여러개의 작은 어플리케이션으로 쪼개어 변경과 조합이 가능하도록 만든 아키텍쳐"**_

이것은 마치 레고놀이와 비슷하다고 볼 수 있는데요, 작은 레고블록(Microservice) 하나하나를 붙여 어떠한 큰 결과물을 만드는 형태를 MSA라고 말씀드릴 수 있겠습니다.





# MSA의 등장배경

MSA의 등장을 살펴보기 위해서는, 기존에 우리가 어떠한 방식으로 개발을 진행해 왔는지에 대해 살펴 볼 필요가 있습니다.

**Monolithic Architecture**

![monolithic_vs_microservices.jpg](https://images.velog.io/post-images/tedigom/8586da80-f8b4-11e9-856d-cbf01881f02b/monolithicvsmicroservices.jpg)

Monolithic Architecture란, 소프트웨어의 모든 구성요소가 한 프로젝트에 통합되어있는 형태입니다. 

아직까지는 많은 소프트웨어가 Monolithic 형태로 구현되어 있고, 소규모 프로젝트에는 Monolithic Architecture가 훨씬 합리적입니다. 간단한 Architecture이고, 유지보수가 용이하기 때문이죠.

하지만 일정 규모 이상의 서비스, 혹은 수백명의 개발자가 투입되는 프로젝트에서 Monolithic Architecture은 뚜렷한 한계를 보입니다.
#  
 * 서비스/프로젝트가 커지면 커질수록, 영향도 파악 및 전체 시스템 구조의 파악에 어려움이 있습니다. 
 
 * 빌드 시간 및 테스트시간, 그리고 배포시간이 기하급수적으로 늘어나게 됩니다.  
 
 * 서비스를 부분적으로 scale-out하기가 힘듭니다.   
 
 * 부분의 장애가 전체 서비스의 장애로 이어지는 경우가 발생하게됩니다.

#  
MSA는 비즈니스 민첩성(Business agility)과 관련이 크고, ~(경영자는 좋아하지만 개발자는 싫어한다는 MSA..)~  서비스나 프로젝트가 크고, 복잡하고, 장기적으로 운영될 수록, MSA의 장점이 더욱 드러나게됩니다.



