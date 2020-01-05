
![스크린샷 2020-01-04 오후 6.32.52.png](https://images.velog.io/post-images/tedigom/52d42fc0-2f78-11ea-ba4b-25bc0ea03be8/-2020-01-04-6.32.52.png)


작년의 마지막날 Google Cloud의 Professional Architect 시험을 쳤고, 얼마전 자격증을 취득하였습니다. 오늘은 구글클라우드 아키텍트 시험에 대한 간단한 소개와, 제가 공부한 방법들에 대해 공유해 보도록 하겠습니다.  

# Google Cloud 자격증 
Google cloud 자격증의 종류와 그에 대한 설명은 아래의 링크에서 확인하실 수 있습니다.   https://cloud.google.com/certification/  

Associate level로는 Cloud Engineer 시험이 있고, Architect를 포함한 나머지 다른 시험들은 모두 Professional level입니다.  

그중 Google Cloud Architect 시험은 200불(약 24만원)의 비용이 발생하며, 120분 동안 50문제 ( 모두 객관식, multiple choice 포함 )를 풀어야 합니다.  

### 시험의 신청
시험은 아래의 링크에 들어가셔서 신청하실 수 있습니다.  
https://cloud.google.com/certification/register/  


![스크린샷 2020-01-05 오후 2.15.50.png](https://images.velog.io/post-images/tedigom/ab0a3570-2f7a-11ea-afc4-c74dc8f1b892/-2020-01-05-2.15.50.png)

시험은 아직 한국어를 지원하지 않습니다.그림과 같은 화면에서 English 탭을 클릭하시면, Google cloud Certificate 로그인 화면이 나옵니다. 회원가입을 하시고, 로그인을 합니다. 


![스크린샷 2020-01-05 오후 2.16.28.png](https://images.velog.io/post-images/tedigom/13fad530-2f7b-11ea-bef6-c14e9d91617f/-2020-01-05-2.16.28.png)

Register For An Exam에서 Architect 시험(혹은 본인이 원하는 시험)을 클릭하여 결제를 진행합니다. 

### 시험 장소

시험 장소는 서울 기준으로 3군데 - 선릉, 종로, 문정에서 진행되며, 문정이 가장 큰 시험장입니다. 
저는 문정에서 시험을 봤는데 소지품 검사가 매우 철저했으며( 주머니, 바짓단, 안경 까지 검사를... ) 제가 시험 칠 때만 그랬는지 모르겠지만 시험장 내에 무슨 기계가 돌아가는 소리가 좀 커서 예민하신 분들에게는 영향을 끼칠 수 있겠다고 생각이 들었습니다.(저는 소음을 막기 위해 비치된 헤드폰을 쓰고 시험을 봤습니다.)  

선릉과 종로는 시험을 볼 수 있는 컴퓨터가 2대 밖에 없는 환경이라고 합니다.

# 시험 준비
저는 회사에서 진행한 과제에서 1~2 개월 정도 Google Cloud Platform을 이용한 경험이 있으며, 당시 IAM, GAE, GCE, GKE, Cloud Function, Storage, Cloud SQL, Cloud build, Container Registry, Pub/Sub, BigQuery, Stackdriver을 사용하였습니다. 

물론, GCP를 사용해 보는 것과, 자격증 시험을 준비하는 것은 아주 다른 개념이지만, 최소한 기본적인 내용들은 학습을 한 상태에서 진행하였습니다. 

GCP를 처음 접해보시는 분들이라면, 아래의 강의들이 도움이 될 것 같습니다.  

## GCP 사용의 기본
### Coursera GCP Architect 인터넷 강의

![스크린샷 2020-01-05 오후 3.24.27.png](https://images.velog.io/post-images/tedigom/147d3580-2f84-11ea-a332-97e99ff37270/-2020-01-05-3.24.27.png)
https://www.coursera.org/learn/preparing-cloud-professional-cloud-architect-exam
기본적인 GCP 서비스들에 대해 잘 정리가 되어있는 강의입니다. 처음 7일 동안은 무료이니, 집중해서 본다면 무료기간 동안 다 볼 수 있습니다.  
###  


### QwikLab 실습
![스크린샷 2020-01-05 오후 3.26.12.png](https://images.velog.io/post-images/tedigom/518b3e90-2f84-11ea-9b63-75035484ca1c/-2020-01-05-3.26.12.png)
https://www.qwiklabs.com/

Qwiklab은 기본적으로 유료 사이트이지만, Google Cloud와 관련된 행사에 참여하거나 구글링을 잘해보시면 크레딧을 획득할 수 있는 방법이 몇가지 있습니다. 개인적으로는 Qwiklab 실습이 GCP의 기본을 익히는데에 도움이 많이 됐던 것 같습니다.  
Qwiklab course 중에 Cloud Architecture, Google Cloud의 Kubernetes 등을 추천드립니다.

#  


## 본격적인 자격증의 준비

시험의 준비는 12월 23일부터 약 1주일 동안 진행하였습니다. 개인적으로 자격증 시험은 짧은 기간내에 집중해서 하는 것이 가장 효과적이라고 생각하고 있지만, 그래도 조금 더 여유를 갖고 하는 것이 바람직한 것 같습니다. 시험 전날 스트레스가 매우 심했거든요 (20만원이 저에게는 꽤 큰돈인지라..)
그래도 결과적으로는 합격을 했으니, 다행인 것 같습니다.

본격적인 자격증을 준비하는 기간에 제가 진행했던 내용들에 대해 설명드리겠습니다.

### 자격증 준비를 위한 개념 공부 - Google Cloud Reference

자격증을 준비하기 위해서는 일반적인 GCP 사용 공부 보다 세세한 것들에 대해 많이 알아야 합니다. 다른 자료들 보다도, 저는 Google Cloud Reference 자료들을 많이 읽었습니다. 이후 문제풀이를 진행하며, 틀린 문제들을 오답 정리 할 때에도 레퍼런스 자료들을 계속 찾아 보았습니다.  
https://cloud.google.com/docs/?hl=ko

![스크린샷 2020-01-05 오후 3.49.30.png](https://images.velog.io/post-images/tedigom/a686bd40-2f87-11ea-8def-0de1b21b24ff/-2020-01-05-3.49.30.png)

AWS에 익숙하신 분들은 아래의 링크를 통해 개념 공부를 하는 것도 괜찮습니다.  
https://cloud.google.com/docs/compare/aws/?hl=ko


### 문제 풀이 - udemy, Whizlab, 공식 practice Test
#### 1. udemy - GCP Professional Cloud Architect - Practice Exams

![스크린샷 2020-01-05 오후 4.00.00.png](https://images.velog.io/post-images/tedigom/24239c40-2f89-11ea-a332-97e99ff37270/-2020-01-05-4.00.00.png)

우선 Free라고 적혀있지만, 무료는 아닙니다. 시리즈 중에 하나를 구입하면, 나머지 시리즈( 난이도 별 문제, 카테고리 별 문제)들을 공짜로 풀어볼 수 있습니다. 저는 짧은 시간 내에 GCP 리소스 개념을 익히기 위해 해당 문제 풀이와, 앞서 소개드렸던 Google Cloud Reference 읽기를 병행하며 진행하였습니다.

**실제 Certificate 문제와는 전혀 다른 형태로 문제가 이루어져있기 때문에** Practice Exam을 위한 자료는 아닙니다. 다만, GCP Resource의 개념을 이해하는 데에는 많은 도움이 되었던 것 같습니다.

https://www.udemy.com/course/gcp-professional-cloud-architect-practice-exams-by-difficultly/

#### 2. Whizlab - Google Cloud Certified Professional Cloud Architect

![스크린샷 2020-01-05 오후 4.10.00.png](https://images.velog.io/post-images/tedigom/99354960-2f8a-11ea-ad7e-19642f2e961d/-2020-01-05-4.10.00.png)

200문제에 30달러 정도로 꽤 비싸긴 하지만, 시기를 잘 맞춘다면 50% 할인된 가격으로 살 수 있습니다. 저도 크리스마스 세일로 50% 가격으로 구입하였습니다.

다른 후기들에서는 Whizlab이 CaseStudy가 업데이트 되지 않아 만족도가 낮았다고 한 것을 봤었는데, 제가 시험을 준비할 때는 모두 업데이트 되어있었습니다. 

저는 시험 직전 이틀 정도 Practice Exam 용으로 사용하였고, 문제가 실제 자격증 시험 문제보다 좀 더 어려웠던 것 같습니다. 문제에 대한 감각이나, 실제 자격증 시험 문제와 비슷한 문제들을 풀어보고 싶으신 분들에게 추천드립니다. ( dump는 아닙니다. Whizlab의 문제가 실제 Exam에 똑같이 나오지 않습니다. )


https://www.whizlabs.com/google-cloud-certified-professional-cloud-architect/

#### 3. 공식 practice Test
Google Cloud Certificate 공식 홈페이지에서 Practice test가 20문제 정도 제공됩니다. 다른 후기 글에서는 Practice Test와 똑같은 문제가 2~3문제 나왔다고 하셨는데, 저의 경우에는 똑같은 문제가 나오진 않았습니다.


  
 > 문제 풀이를 진행한 후에는 오답노트를 만들어 놓는 것이 공부하는데에 효과적입니다.


### 기타 도움이 됐던 방법 / 참고자료들
#### 1. Asana를 이용한 할 일 목록 정리
![스크린샷 2020-01-05 오후 1.54.35.png](https://images.velog.io/post-images/tedigom/d7317540-2f85-11ea-8def-0de1b21b24ff/-2020-01-05-1.54.35.png)

GCP Architect 자격증을 준비하는 것과 직접적인 연관이 있는 것은 아니지만, 개인적으로 공부를 진행하거나 할일 목록을 정리할 때 저는 Asana를 많이 이용하고 있습니다. (Trello와 같은 다른 Kanban board 서비스를 사용해도 괜찮습니다.) 

#### 2. AWS/GCP/Azure 시험준비 카톡방
개인적으로 모르는 것을 질문하거나, 자료들을 얻을 때 많은 도움이 되었던 카톡방입니다.  
https://open.kakao.com/o/gMCqYX

#### 3. Google Cloud Platform 페이스북 그룹

Google Cloud 유저 그룹  
https://www.facebook.com/groups/googlecloudkorea/  
시험준비와 관련된 그룹  
https://www.facebook.com/groups/1129292383932010/   

#### 4. 도움이 됐던 다른 후기글들
개인적으로, 동민님과 태호님의 GCP 후기 글들을 보며 시험 준비를 하였고, 많은 도움이 되었습니다.  

https://reoim.tistory.com/entry/Google-Cloud-Certified-Professional-Cloud-Architect-%ED%9B%84%EA%B8%B0  
https://brunch.co.kr/@topasvga/728  






