지난 포스팅에서 MSA를 구성하는 아키텍처 요소에 대해 살펴보았습니다. Inner Architecture와 Outer Architecture로 나누어 설명을 드렸었죠. 

[MSA 제대로 이해하기 - (2)아키텍처 개요](https://velog.io/@tedigom/MSA-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-2-MSA-Outer-Architecure)

오늘은 그 중 Outer Architecture에서도 API Gateway에 대해 설명하려 합니다.

## API Gateway의 필요성



![concept1.PNG](https://images.velog.io/post-images/tedigom/5ae7a9e0-ff02-11e9-929b-8bdd0f9b8460/concept1.PNG)

MSA는 큰 서비스를 잘게 쪼개어 개발/운영 하는 아키텍처입니다. 
하나의 마이크로 서비스에는 한개 이상의 서버가 존재하게 되는데