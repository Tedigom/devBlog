이번 시간에는 MSA의 Outer Architecture 중 Telemetry에 대해 알아보도록 하겠습니다.  

# Telemetry
MSA에서는 상당수의 마이크로서비스가 분산환경에서 운영되기 때문에 서비스들의 상태를 일일이 모니터링하고, 이슈에 대응 하는 것은 굉장히 힘들고 오랜 시간이 걸립니다. Telemetry는 서비스들을 모니터링하고, 서비스별로 발생하는 이슈들에 대응할 수 있도록 환경을 구성하는 역할을 합니다.  

Telemetry는 Grafana, Prometheus, EFK와 같이 오픈소스로 직접구현하는 방법, Datadog와 같은 상용 솔루션을 이용하는 방법, 그리고 AWS Cloud watch, GCP Stackdriver와 같이 public cloud의 SaaS를 이용하는 방법으로 구현할 수 있습니다.  

![Telemetry](https://github.com/Tedigom/devBlog/blob/master/MSA%20Series/Telemetry/Telemetry%20.png) . 

## Telemetry의 주요기능
### 1. Monitoring
모니터링은 인프라 및 응용 프로그램의 성능이나 효율성을 확인하는 작업으로 마이크로 서비스를 운영하는데에 필요로 합니다. Monitoring을 위해서는 metric 수집, logging, Tracing 영역에서의 데이터 수집 및 분석이 필요합니다.  

AWS의 Cloud watch, Azure의 Monitor, GCP의 Stackdriver가 Public cloud에서 Monitoring을 담당하는 요소이며, OSS로는 Prometheus등이 있습니다.
Monitoring은 각 대상에서 수집한 Metric을 통해 대상의 리소스 사용률이나, 트래픽 등을 대시보드로 볼 수 있게 해줍니다.  

![prometheus](https://github.com/Tedigom/devBlog/blob/master/MSA%20Series/Telemetry/prometheus.png) . 

### 2.Logging
Log는 실행중인 프로세스에서 발생하는 이벤트를 말하며, Logging은 이러한 Log들을 수집해서 보여주는 것을 말합니다. 마이크로 서비스 아키텍쳐는 Monolithic 어플리케이션보다 실행하는 프로세스의 수가 훨씬 많기 때문에 장애가 발생시에 root cause를 파악하기 힘듭니다.  

AWS에서는 Amazon Elastic Search 등이 Logging을 담당하는 요소이며, OSS로는 EFK(Elastic Search - FluentD - Kibana) 가 대표적입니다. 각 서비스에 심어진 Agent가 해당 서비스의 Log정보들을 수집하고, Log Server(Aggregator)를 통해 취합됩니다. 최종적으로 Kibana와 같은 툴을 통해 시각화된 데이터를 관리자에게 보여줍니다.  

![efk.pngimage](https://github.com/Tedigom/devBlog/blob/master/MSA%20Series/Telemetry/efk.png)
출처: https://medium.com/@carlosedp/log-aggregation-with-elasticsearch-fluentd-and-kibana-stack-on-arm64-kubernetes-cluster-516fb64025f9 . 

#### Logging시의 고려사항
로그를 서비스 내 저장소에 저장할 경우, 관리가 어려워지므로 ( container managed service의 경우 컨테이너가 종료되거나 재시작 될 경우 사라질 수 있습니다.) 로그를 어플리케이션 서버 내부에 저장하지 않고 외부 저장소에 저장하도록 합니다.  
MSA 에서 가상머신과 컨테이너는 application과의 결합이 "약한 결합"입니다. 즉, 배포에 사용되는 컨테이너는 배포할 때마다 달라질 수 있습니다. 따라서 디스크 저장 상태에 의존하는 것이 아니라, 별도의 Logging도구를 활용하는 것이 효율적입니다.  
로그파일은 ACL을 통하여 로그 관리자만 로그를 확인 할 수 있도록 하여야 합니다.  

### 3. Tracing
Tracing은 마이크로 서비스 아키텍처에서 발생한 Event를 발생한 순서대로 나열하여 추적할 수 있게 해주는 기능입니다.  

AWS에서의 Amazon X-Ray 등이 Tracing을 담당하는 요소이며, OSS로는 Zipkin Jaeger등이 대표적입니다.  


+ Stackdriver / Spinnaker / Zipkin
