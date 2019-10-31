![lego-708086_1920.jpg](https://images.velog.io/post-images/tedigom/c2875230-f8b8-11e9-a757-dd517f114496/lego-7080861920.jpg)
����ũ�� ���� ��Ű���ĸ� �Ѹ���� ������ ���� ǥ���� �� �ֽ��ϴ�.

_**"�ϳ��� ū ���ø����̼��� �������� ���� ���ø����̼����� �ɰ��� ����� ������ �����ϵ��� ���� ��Ű����"**_

�̰��� ��ġ ������̿� ����ϴٰ� �� �� �ִµ���, ���� ������(Microservice) �ϳ��ϳ��� �ٿ� ��� ū ������� ����� ���¸� MSA��� �����帱 �� �ְڽ��ϴ�.
  
# MSA�� ������

MSA�� ������ ���캸�� ���ؼ���, ������ �츮�� ��� ������� ������ ������ �Դ����� ���� ���� �� �ʿ䰡 �ֽ��ϴ�.

### Monolithic Architecture

![monolithic_vs_microservices.jpg](https://images.velog.io/post-images/tedigom/8586da80-f8b4-11e9-856d-cbf01881f02b/monolithicvsmicroservices.jpg)

Monolithic Architecture��, ����Ʈ������ ��� ������Ұ� �� ������Ʈ�� ���յǾ��ִ� �����Դϴ�. 

���������� ���� ����Ʈ��� Monolithic ���·� �����Ǿ� �ְ�, �ұԸ� ������Ʈ���� Monolithic Architecture�� �ξ� �ո����Դϴ�. ������ Architecture�̰�, ���������� �����ϱ� ��������.

������ ���� �Ը� �̻��� ����, Ȥ�� ������� �����ڰ� ���ԵǴ� ������Ʈ���� Monolithic Architecture�� �ѷ��� �Ѱ踦 ���Դϴ�.
###  
 * ����/������Ʈ�� Ŀ���� Ŀ������, ���⵵ �ľ� �� ��ü �ý��� ������ �ľǿ� ������� �ֽ��ϴ�. 
 
 * ���� �ð� �� �׽�Ʈ�ð�, �׸��� �����ð��� ���ϱ޼������� �þ�� �˴ϴ�.  
 
 * ���񽺸� �κ������� scale-out�ϱⰡ ����ϴ�.   
 
 * �κ��� ��ְ� ��ü ������ ��ַ� �̾����� ��찡 �߻��ϰԵ˴ϴ�.

###  
MSA�� ����Ͻ� ��ø��(Business agility)�� ������ Ů�ϴ�. ~(�濵�ڴ� ���������� �����ڴ� �Ⱦ��Ѵٴ� MSA..)~  ���񽺳� ������Ʈ�� ũ��, �����ϰ�, ��������� ��� ����, MSA�� ������ ���� �巯���Ե˴ϴ�.

> _MSA �������� CBD, SOA �� Monolith�� ��/���������� ����ȭ �ϱ� ���� ��µ��� �־�Խ��ϴ�. 
MSA�� ū �ǹ̿��� SOA�� �κ��������� �������� ������, ������ ��ȸ�� �� �� SOA�� MSA�� ���� �ڼ��� �ٷﺸ���� �ϰڽ��ϴ�._ 

# Micro service�� ����
Martin Folwer�� MSA�� ���� �Ʒ��� ���� �����Ͽ����ϴ�.  

_"the microservice architectural style is an approach to developing a single application as a suite of small services, each running in its own process and communicating with lightweight mechanisms, often an HTTP resource API. These services are built around business capabilities and independently deployable by fully automated deployment machinery."_ 

���� : https://martinfowler.com/articles/microservices.html
###  
�� ���忡�� ���� _**small services, each running in its own process(������ ���� �� �� �ִ� ���� ����)**_ ��, _**independently deployable(������ ���� ����)**_ �� MicroService�� ������ �� �� �ִ� ���� �ٽ����� ������� �����մϴ�.
![lego-708086_1920.jpg](https://images.velog.io/post-images/tedigom/c2875230-f8b8-11e9-a757-dd517f114496/lego-7080861920.jpg)
����ũ�� ���� ��Ű���ĸ� �Ѹ���� ������ ���� ǥ���� �� �ֽ��ϴ�.

_**"�ϳ��� ū ���ø����̼��� �������� ���� ���ø����̼����� �ɰ��� ����� ������ �����ϵ��� ���� ��Ű����"**_

�̰��� ��ġ ������̿� ����ϴٰ� �� �� �ִµ���, ���� ������(Microservice) �ϳ��ϳ��� �ٿ� ��� ū ������� ����� ���¸� MSA��� �����帱 �� �ְڽ��ϴ�.
  
# MSA�� ������

MSA�� ������ ���캸�� ���ؼ���, ������ �츮�� ��� ������� ������ ������ �Դ����� ���� ���� �� �ʿ䰡 �ֽ��ϴ�.

### Monolithic Architecture

![monolithic_vs_microservices.jpg](https://images.velog.io/post-images/tedigom/8586da80-f8b4-11e9-856d-cbf01881f02b/monolithicvsmicroservices.jpg)

Monolithic Architecture��, ����Ʈ������ ��� ������Ұ� �� ������Ʈ�� ���յǾ��ִ� �����Դϴ�. 

���������� ���� ����Ʈ��� Monolithic ���·� �����Ǿ� �ְ�, �ұԸ� ������Ʈ���� Monolithic Architecture�� �ξ� �ո����Դϴ�. ������ Architecture�̰�, ���������� �����ϱ� ��������.

������ ���� �Ը� �̻��� ����, Ȥ�� ������� �����ڰ� ���ԵǴ� ������Ʈ���� Monolithic Architecture�� �ѷ��� �Ѱ踦 ���Դϴ�.
###  
 * ����/������Ʈ�� Ŀ���� Ŀ������, ���⵵ �ľ� �� ��ü �ý��� ������ �ľǿ� ������� �ֽ��ϴ�. 
 
 * ���� �ð� �� �׽�Ʈ�ð�, �׸��� �����ð��� ���ϱ޼������� �þ�� �˴ϴ�.  
 
 * ���񽺸� �κ������� scale-out�ϱⰡ ����ϴ�.   
 
 * �κ��� ��ְ� ��ü ������ ��ַ� �̾����� ��찡 �߻��ϰԵ˴ϴ�.

###  
MSA�� ����Ͻ� ��ø��(Business agility)�� ������ Ů�ϴ�. ~(�濵�ڴ� ���������� �����ڴ� �Ⱦ��Ѵٴ� MSA..)~  ���񽺳� ������Ʈ�� ũ��, �����ϰ�, ��������� ��� ����, MSA�� ������ ���� �巯���Ե˴ϴ�.

> _MSA �������� CBD, SOA �� Monolith�� ��/���������� ����ȭ �ϱ� ���� ��µ��� �־�Խ��ϴ�. 
MSA�� ū �ǹ̿��� SOA�� �κ��������� �������� ������, ������ ��ȸ�� �� �� SOA�� MSA�� ���� �ڼ��� �ٷﺸ���� �ϰڽ��ϴ�._ 

# Micro service�� ����
Martin Folwer�� MSA�� ���� �Ʒ��� ���� �����Ͽ����ϴ�.  

_"the microservice architectural style is an approach to developing a single application as a suite of small services, each running in its own process and communicating with lightweight mechanisms, often an HTTP resource API. These services are built around business capabilities and independently deployable by fully automated deployment machinery."_ 

���� : https://martinfowler.com/articles/microservices.html
###  
�� ���忡�� ���� _**small services, each running in its own process(������ ���� �� �� �ִ� ���� ����)**_ ��, _**independently deployable(������ ���� ����)**_ �� MicroService�� ������ �� �� �ִ� ���� �ٽ����� ������� �����մϴ�.

![pic_1.png](https://images.velog.io/post-images/tedigom/575c07d0-f980-11e9-ac2c-696993348d8a/pic1.png)


martin Fowler�� �������� �����Ͽ�, MSA������ (micro)Service�� �� ������ �������� ������ ���ҽ��ϴ�.  
###  
* ������ ���񽺴� �� ũ�Ⱑ ���� ��, ���� ��ü�� �ϳ��� ��ƽ ��Ű���Ŀ� ������ ������ ����

* ������ ���񽺴� ���������� ������ �����ؾ���.  

* ������ ���񽺴� �ٸ� ���񽺿� ���� �������� �ּ�ȭ �Ǿ����  

* �� ���񽺴� ���� ���μ����� ���� �Ǹ�, REST�� ���� ������ ������� ��ŵǾ�� ��.
###  

�Ϲ������� �ϳ��� ���񽺴� �ϳ��� ����̸�, �ϳ��� ������Ʈ��� �� �� ������, ����Ͻ��� �ý����� ������ �°� ������ ����(ũ��)�� �����ϴ� ���� �߿��մϴ�.

# MSA�� �����
### MSA�� ����
�켱 MSA�� ������ ���� �˾ƺ����� �ϰڽ��ϴ�. MSA�� ���񽺰� Ŀ���鼭 ����� Monolithic Architecture�� ���������� ������� ������ �� �� �ֽ��ϴ�.


* ����(deployment) ����
	* ���� �� ���� ���� ���� ( ���� �� ��ü ������ �ߴ��� ����)
    * �䱸������ �ż��ϰ� �ݿ��Ͽ� ������ ������ �� ����.  
    ###  

* Ȯ��(scaling) ����
	* Ư�� ���񽺿� ���� Ȯ�强�� ������.
    * Ŭ���� ��뿡 ������ ��Ű����.
    ###  
* ���(failure) ����
	* ��ְ� ��ü ���񽺷� Ȯ��� ���ɼ��� ����
    * �κ��� ��ֿ� ���� �ݸ��� ������
###  

�̿ܿ���, �ű���� ������ �����ϰ�, ���񽺸� polyglot�ϰ� ����/� �� �� �ִٴ� ������ �ֽ��ϴ�.
###  
### MSA�� ����
Monolithic Architecture�� �ܼ��� ��Ű�����ε� ���� MSA�� ���� ������ ��Ű���ķ�, ��ü ���񽺰� Ŀ���� ���� �� ���⵵�� ���ϱ޼������� �þ �� �ֽ��ϴ�.

* ���� - ���� �� ȣ�� �� API�� ����ϱ� ������, ��� ����̳�, Latency�� �׸�ŭ �þ�� �˴ϴ�.
###  
* �׽�Ʈ / Ʈ����� - ���񽺰� �и��Ǿ� �ֱ� ������ �׽�Ʈ�� Ʈ������� ���⵵�� �����ϰ�, ���� �ڿ��� �ʿ�� �մϴ�.
###  
* ������ ���� - �����Ͱ� ���� ���񽺿� ���� �л�Ǳ� ������ �ѹ��� ��ȸ�ϱ� ��ư�, �������� ���ռ� ���� �����ϱ� ��ƽ��ϴ�.