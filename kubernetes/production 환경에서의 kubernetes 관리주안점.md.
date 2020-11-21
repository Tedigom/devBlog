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


