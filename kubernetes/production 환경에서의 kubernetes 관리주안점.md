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
