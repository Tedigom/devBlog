# Production 환경에서 고려해야할 kubernetes 이슈 및 해결방법

Production에서 발생하는 kubernetes 이슈 ( Most common customer issues)
* 메모리 과부하 이슈 ( Memory overload )
* IO 과부하 이슈 ( IO overload )
* SNAT 포트 부족 (SNAT port exaustion )
* Master(Control plane) 과부하 (Control plane overload)
* 리소스 할당량 부족 ( Insufficient quota )
* 네트워크 설정오류 ( Network misconfiguration ) 


## 1. 메모리 과부하 이슈 ( Memory overload )
메모리 과부하 이슈의 경우에는 위에 언급된 다른 이슈들 보다는 조금 더 수월하게 해결이 가능합니다. 
우선, 메모리 과부하 이슈가 생길때의 증상을 살펴보도록 하겠습니다.

### 메모리 과부하 이슈로 인한 증상
1. 사용자의 pod가 강제종료(evicted) 됨  
2. 사용자의 pod가 Out of Memory로 인해 제거됨 (OOMKilled)  
3. Kube-system의 파드가 evicted 됨  
4. 노드가 일시적으로 tainted되어 파드가 스케쥴링이 되지 않음  


#### 1. 사용자의 pod가 강제종료(evicted) 되는 경우
Pod가 요구하는 리소스의 limit의 양이 실제 시스템이 가용할 수 있는 리소스의 양보다 많은 상황이 발생할 수 있습니다.(이를 overCommited 된 상태라 합니다.)
Overcommited 상태가 계속될 경우, CPU의 경우에는 request 수준까지 할당 상태를 낮출수 있습니다.(성능 저하를 일어나지만, Pod가 제거되지 않음)  
하지만, Memory의 경우 할당된 메모리의 크기를 바로 줄일 수 없기 때문에 우선순위에 따라 운영중인 Pod를 강제종료 시킵니다.

> Pod 제거 우선순위
> 1. request와 limit이 둘다 설정되어있지 않은 pod
> 2. limit 설정이 되어있지만, request가 설정이 되어있지 않은 경우 / request는 설정이 되어있지만 limit 설정이 되어있지 않은 경우
> 3. 시스템 pod


#### 2. 사용자의 pod가 Out of Memory로 인해 제거되는 경우 (OOMKilled)
pod의 limit이 설정되어 있지만, limit값이 너무 작을 때 Out of Memory Killed(OOMKilled) 가 발생합니다.  
request와 limit값을 pod 내 어플리케이션 resource 요구량에 맞게 설정하는 것이 이러한 증상을 줄일 수 있는 방법입니다.


#### 3. Kube-system의 파드가 강제종료(evicted) 되는 경우
이 경우는 쿠버네티스 클러스터 자체가 불안정적이거나, 사용할 수 없는 상태가 되어버립니다.


### 메모리 과부하 이슈가 생길때 취할 수 있는 방법 ( Best Practices )
1. 모든 Pod에 request와 resource를 설정합니다.
2. namespace 마다의 Resource Quota와 Limit Range를 설정하여 클러스터의 자원을 관리합니다.
3. Critical한 Pod의 경우에는 dedicated node pool로 분리 시키거나, 해당 Pod가 Critical하다는 것을 라벨링하여 표시합니다.  



## 2. IO 과부하 이슈 ( IO overload )
IO 과부하 이슈(Disk 이슈)는 Memory 과부하 이슈보다는 조금 더 발견하기 어려우며, 복합적인 증상이 나타납니다. 
IO와 관련한 이슈는 다른 것 보다도 모니터링 툴을 통해 조금 더 쉽게 확인 가능하며, 모니터링 툴을 활용하는 방법이 가장 이상적입니다.

### IO 과부하 이슈로 인한 증상
1. 클러스터 내 노드가 NotReady 상태가 됨
2. API 서버에 접근할 때 "TLS handshake timeout" 메세지가 나타남
3. 중요한 데몬셋이나 pod(kube-proxy, coreDNS 등) 이 fail 상태가 됨
4. istio 사용이나, 복잡한 오퍼레이터 설정시에 성능/안정성 이슈가 생김
5. 타 클라우드 서비스/On-premises 연결시에 latency가 길어지거나 networking 에러가 발생
6. 느린 DNS쿼리
7. Persistent Volume을 연결/연결해제 시킬 때 느리거나, 이슈가 생김  

### IO를 증가시키는 원인
* Pod의 수가 너무 많거나, 컨테이너의 이미지가 너무 큰 경우 
* 써드파티 로깅 시스템이나,모니터링, audit tools을 적극적으로 사용하는 경우
* OS디스크를 데이터디스크 처럼 사용하는 경우 

> Public Cloud에서 Kubernetes Production 환경을 사용하는 경우에는 IOPS에 대한 확인 및 고려가 굉장히 중요합니다.   
> Azure의 경우에는 VM에 해당하는 부분과 OS Disk에 해당하는 부분의 IOPS가 각각 존재하며, 선택한 VM의 IOPS와 OS Disk의 IOPS 중 더 작은 값이 Max IOPS입니다. 따라서 VM의 IOPS 뿐만 아니라 OS Disk의 IOPS에 대한 고려도 굉장히 중요합니다.  

> ex ) VM의 IOPS가 12800 / OS 디스크의 IOPS가 120인 경우, MAX_IOPS의 값은 120이 됨. 


### IO 과부하 이슈가 생길때 취할 수 있는 방법 ( Best Practices )
1.OS 디스크를 데이터디스크처럼 사용하면 안됩니다. 데이터 디스크는 PV를 붙여서 사용해야합니다.
2.OS 디스크의 사이즈를 충분히 늘려 어플리케이션이 구동할 수 있을 만큼의 max IOPS를 확보해야합니다.
3. ephemeral OS 디스크를 사용함으로써 성능을 높일 수 있습니다.
4. knode를 이용하여 성능을 높일 수 있습니다.( 도커에 대한 mountPath를 data-drive나 ephemeral disk로 변경)
5. 써드파티 로깅시스템이나 모니터링에 대하여 I/O를 많이 사용하는지에 대하여 체크를 해야합니다.
6. OS Disk에 alert를 세팅해주어 이슈가 있을 때 운영자에 알람이 갈 수 있도록 합니다.



## 3. SNAT 포트 부족 이슈 (SNAT port exaustion )
SNAT 포트 부족 이슈는 Public cloud를 사용하는 경우 좀 더 발생하기 쉬운 이슈로, 어플리케이션 구동에 직접적인 영향을 끼치지만 바로 원인을 
발견하기 어렵기 때문에 클라우드사 모니터링 툴을 활용하여 SNAT의 여유가 충분한지 체크를 계속 해주어야 합니다.

### SNAT 포트 부족 이슈로 인한 증상
1. 간헐적으로 DNS resoulution이 실패됨
2. 노드가 NotReady 상태가 되어 API 서버에 연결을 할 수 없게됨.
3. Pod에서 API server나 다른 네트워크 주소로 연결 시 "i/o timeout"과 같은 에러코드가 발생함


### SNAT 포트부족 이슈가 생길 때 취할 수 있는 방법 ( Best Practices, Azure의 경우 )
1. frontend IP를 늘려줌으로써 아웃바운드에 대한 커넥션 숫자를 늘려줍니다.
2. VM 마다의 아웃바운드 포트 갯수를 조절합니다.
3. SNAT을 얼마나 사용하는지, 얼마나 Fail이 되는지를 모니터링을 항상 해주어야 합니다. 



## 4. Master(Control plane) 과부하 이슈 (Control plane overload )
일반적으로 Public cloud에서 Kubernetes를 운영할 때에는 managed 서비스(EKS, AKS, GKE 등)을 사용하는 경우가 많은데, 이런 경우에도 Control plane에 간헐적으로 문제가 발생할 수 있습니다.  

Master(Control plane)에 과부하가 생길 경우의 증상으로는 보통 API 서버와 연결 시 "TLS handshake timeout" 현상이 발생하게 됩니다.(API 서버에 문제가 발생하게 됨)  

API서버에 너무 높은 QPS hitting이 발생하거나, ETCD에 너무 많은 객체가 들어가서 API 서버에서 응답을 할때의 payload가 너무 커지는 경우, 혹은 컨테이너가 너무 많거나, request나 update가 많을 때에는 Control plane의 API 서버가 OOMkilled가 될 수 있습니다.  


### Master(Control plane) 과무하 이슈가 생길 때 취할 수 있는 방법 ( Best Practices)
1. 클러스터의 API 서버에는 DDOSing을 하지 않습니다.
2. 새로운 컴포넌트를 올릴 경우에는 미리 load test를 해야합니다.
3. API 서버의 limit QPS 와 throughput을 항상 모니터 해줍니다.
4. cronjob의 경우 끝난 job들에 대하여 자동으로 cleanup할 수 있도록 해주어야 합니다.


## 5.리소스 할당량 부족 이슈 ( Insufficient quota )
Quota에 대한 계획은 kubernetes를 운영환경에서 활용할 때 굉장히 중요합니다. 또한, 요구사항이나 문제 상황에 따라 quota를 바로바로 늘릴 수 있는 환경을 구성해 놓는 것도 역시 중요합니다. 여기서의 리소스란, CPU/Memory 뿐만 아니라 VNET에 해당하는 서브넷 등도 포함합니다.

Quota 부족이 생길 경우의 증상으로는 auto-scaling이나 수동으로 scaling을 할 때 해당 동작이 실패 할 수 있고, pod/node의 업그레이드가 실패 할 수 있습니다. ( rolling upgrade(default)를 하는 경우에는 여유분의 자원이 필요합니다.)  

Quota문제의 경우에는 에러메세지에 Quota가 부족하다고 나오기 때문에 좀 더 빠르게 문제를 해결할 수 있습니다.  

### 리소스 할당량 부족 이슈가 생길 때 취할 수 있는 방법 ( Best Practices)
1. Planning을 사전에 미리 해봐야합니다. (production 환경에 옮기기 전 로드 테스트(CPU,메모리 뿐만 아니라 네트워크 관점에서도..)를 거쳐 플래닝이 이루어 져야 합니다.)
2. Public cloud의 경우에는 특정 region에 대해 Quota가 부족할 수 있기 때문에 multiple-region에서 사용할 수 있는 아키텍처가 필요합니다. 


## 6. 네트워크 설정 오류  이슈 ( Network misconfiguration )
### 네트워크 설정 오류로 인한 증상
1. 노드가 NotReady 상태가 됨
2. API 서버에 연결 할 때 "TLS handshake timeout"에러가 발생함
3. Pod를 만들 때 Image pull fail 에러가 발생함
4. scaling이나 업그레이드를 할 때 실패함
5. pod 간 통신이나 다른 노드와의 통신이 실패함

네트워크 오류가 발생할 경우에는, 네트워크의 문제/변경이 있었는지를 가장 먼저 확인해 주어야하며,  
NSG(Network Security Groups)룰이나 Policy가 잘못 설정했거나 변경이 생긴 경우를 확인해 주어야 합니다.  
또한, Custom DNS 서버나 vnet의 firewall을 사용할 경우 잘못 설정되어 있는 부분에 대해 확인하고, pod를 생성하거나 operation을 할때 실패현상을 야기시키는 부분이 없는지 체크해 주어야합니다.  
