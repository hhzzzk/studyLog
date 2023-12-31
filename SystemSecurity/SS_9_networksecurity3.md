# SS_9_networksecurity3

[TOC]



## Firewall

- 기본적으로 패킷을 하나하나 다 열어본 뒤 관리자의 기준에 맞는 페킷을 통과/방어하는 역할
- Inbound session : 외부에서 방화벽 내부로 들어가는 패킷(제약을 걸어주는 역할)
- Outbound session : 방화벽 내부에서 외부로 나가는 페킷(자유로워야 함)
- 외부에서 DB로 바로 못가게 하면서 내부의 PC들은 외부 인터넷을 자유롭게 사용할 수 있게 해줌



Firewall rule-set으로 패킷의 전송을 결정한다.

5가지 조합에 어떤 액션을 취하는지

마지막 줄은 디폴트 값으로 거절한다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/fdfe5a73-dd9f-4b97-834d-1490e294421f)

규칙 찾을 때 1번부터 순서대로 매칭을 확인한다.

시험문제!!!!!패킷이 주어지면 몇 번 방화벽을 적용하는지!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!



## stateless firewall

옛날에는 stateless인 방화벽이었다.

stateless의 문제는 1. 속도가 느리고(5단계의 방화벽규칙) 2. 보안문제가 있다.

4번 규칙을 보면 출발지의 ip와 포트는 상관없고 도착지가 포트번호는 1024부터 6만넘게까지이다.

외부에서 출발한 악성 ip일 경우 감염가능하다. 위험하다.

그러나 원래 4번 규칙의 의도는 3번 규칙을 만족한 SYN, 싱크 패킷을 받고 나면 반대방향으로 나가는 ACK, 어크패킷을 허락한다는 의미였다.

즉 stateless라서 발생한 문제이다.



## stateful firewall

그래서 등장한 stateful 방화벽은 반대방향도 알아서 인식한다.

보안을 해결하고 속도가 올라갔다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/2084e28f-3c00-4478-bd2e-281f57ed444c)



## firewall : DMZ

- 일반적으로 외부에서 웹 서버로 들어오는 페킷은 열어둠(서비스를 위해)
- 웹 서버 자체는 치명적이지 않지만 웹 서버를 통해 DB로 들어갈 수 있음

![img](https://velog.velcdn.com/images/3eung_h10n/post/3cedd80a-6f15-4628-8ed2-b3eaa93534a1/image.png)

- 웹 서버에서 DB로 가는 포트 1개만 열어주는 방식으로 방화벽 규칙을 추가
  - 해커가 여전히 웹 서버를 점령한다해도 웹서버에서 DB로 가는 길은 포트번호 1개 밖에 없기 때문에 공격자가 DB를 공격하기 매우 어려워짐
- 실제로는 방화벽을 더 사용해서 외부 내부로 나누어둠

## High Availability

![image](https://github.com/hhzzzk/studyLog/assets/67236054/0a91a0d1-b064-4080-b132-63eaece136af)

방화벽 이중화 L4/L7

방화벽 stateful의 문제가 발생한다.

- 방화벽 0,1번이 있을 때 싱크가 0으로 지나갔는데 어크가 1로 가면 block된다.
- 어떤 방화벽을 썼는지 기억해야 연결이 유지된다.
  - 위의 2개의 방화벽이 전송 상태를 기억하기 때문에 페킷은 처음 지나간 방화벽을 계속 사용해야함



## L4/L7 스위치

L4는 transport 레이어로 MAC 주소만 보지 않고 포트번호도 본다.

> »H(s_ip XOR d_ip) mod (# of firewall)

XOR 연산을 통해 출발지와 도착지의 순서가 달라도 값이 나온다. 이를 해시함수 처리한다.

이걸 모듈러 연산은 방화벽 개수만큼 한다. 여기서는 방화벽이 2개라 0,1이 나올 것이다.



## Firewall HA

방화벽 간의 선을 직접 연결해 방화벽 메모리를 동기화한다.

![img](https://velog.velcdn.com/images/3eung_h10n/post/0e7195a9-b6d1-49cd-a244-644271c13c09/image.png)

## 스위치의 종류

여러가지 종류

–L2 switch

–L3 switch

–L4/L7 switch



다음시간



# High Availability : VRRP

VRRP (Virtual Router Redundancy Protocol)은 네트워크 환경에서 고가용성을 제공하기 위한 기술

라우터를 여러 개 사용한다.



여러 개의 라우터 중 하나를 마스터로 하나는 슬레이브=백업으로 쓴다. 마스터 죽으면 슬레이브를 쓴다.

- 마스터는 주기적으로 다른 라우터들에게 나는 살아있다는 메시지를 보낸다.
- 슬레이브는 대기상태로 있는다.
- 슬레이브들은 주기적으로 마스터에게 메시지 안오면 마스터 죽었다고 감지. 슬레이브 중 하나가 새로운 마스터로 승격된다.

election process : 새로운 마스터 뽑을 때 선거로 뽑는다. 어떻게 새로운 마스터 선정할지 결정법 

![img](https://velog.velcdn.com/images/3eung_h10n/post/602654c0-ee98-43ac-8942-8f1b345faab4/image.png)

## VRRP : virtual ip !!!!!!!!!!!!!!!!!!개중요

라우터는 각각의 ip 주소를 가지고 추가로 vip, 가상의 ip를 둘 다 가진다.

- 마스터가 처음에 vip 사용 이후 마스터가 고장
- 슬레이브가 vip를 이어받아 마스터가 되어 vip를 사용한다.



vip는 가상의 ip주소로 실제로는 어느 라우터에도 할당되지 않고 라우터끼리 공유된다.

1. 라우터 2개 사이에 vrrp 구성한다. 이 구성에 대한 VRID, 버추얼 라우터 ID를 할당하고 VIP를 연결한다. 42.1
2. 마스터 라우터를 결정한다. 
3. VRRP 그룹을 활성화. 각 라우터에 VIP를 할당한다. 활성 마스터 라우터는 VIP를 사용한다.
4. 활성 마스터는 정기적으로 VRRP 메시지를 브로드캐스트해 살아있음을 알린다.
5. 다른 라우터는 마스터 살아있으면 VIP를 마스터 라우터의 IP주소 42.2로 라우팅한다.
6. 마스터가 고장날 경우, 슬레이브 중 하나가 마스터가 된다. 이때 VIP는 새로운 마스터에게 라우팅된다. 



## 공격자가 가짜 VRRP 메시지를 보낼 경우

이를 대비해 라우터에도 보안을 추가할 수 있다.



## VRRP : Active / passive=standby

위의 방법이 스탠드바이 방법, 1개가 액티브하고 하나가 스탠드바이로 대기한다.

그러나 두 개의 라우터를 전부 사용해 상시가동하고 싶다면 active/ active 모드로 설정해야 한다.

설정방법

1. 가상 ip 주소를 1개 더 사용한다. vip1, vip2
2. 각 vip를 다른 vrrp 그룹에 할당한다.
3. 라우터 우선순위를 결정한다. 어떤 라우터가 활성마스터가 될지 결정한다.



## 서버도 이중화하기

![image](https://github.com/hhzzzk/studyLog/assets/67236054/4f8dcd59-c954-47f5-957c-b679312d5ad0)

서버도 2개를 사용해 고가용성을 한다.

Heartbeat : 서버끼리 하트비트 선을 통해 연결한다. 서로의 상태를 알 수 있다. 단순 핑보다 더 많은 정보가 포함된다.



## 서버가 몇 대 필요한가?

p는 가용성의 확률, 즉 시간인데 장애가 몇 시간 발생하는지를 나타낸다.

0.999999, 9가 6개면 1년에 31.5초 장애가 발생한다.

n은 서버의 개수로 Qn은 서버가 정상제공될 확률을 나타낸다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/bb351c2f-aa44-4f9e-be77-cb1c11cb01a3)

2개의 서버일 경우 qn은 둘다 정상 작동, 1개만 정상작동해서

oo + ox + xo 는 pp + p(1-p) + (1-p)p이다.

서버가 3개면 복잡해진다.



쉽게 계산하려면 여사건을 계산해서

전체에서 xx를 빼면 쉽다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/9c52b69d-6f30-45ff-b712-4f02693f42b7)

- p가 0.9999인 서버가 2대만 있어도
  - ![img](https://velog.velcdn.com/images/3eung_h10n/post/97114a19-1f25-4573-9cb2-2ef268e39627/image.png)
  - 9가 8개가 생김 -> 매우 높은 수치라 보통 서버를 2대를 많이 사용함



## 고가용성

![image](https://github.com/hhzzzk/studyLog/assets/67236054/d620d5a6-5c29-45bd-a42d-762518575235)

라우터, 방화벽, 스위치를 다 2개씩 구성해서 가용성 높이기

그러나 모든 구성이 한 건물에 있다는 단점 911 테러같은 위험 존재

![image](https://github.com/hhzzzk/studyLog/assets/67236054/9d582c88-a344-44ba-af95-213fc6913150)



서버를 각각 다른 지역에 두는 방법으로 더 높일 수 있음(Disaster Recovery Center)

DR센터를 따로 둬서 백업이 가능하도록 한다. 



## 로드 밸런싱, GSLB

로드 밸런싱은 여러 서버나 리소스의 트래픽을 균형 있게 분산하는 기술이다. DR센터를 통해 로드밸런싱을 유지한다.

Global Server Load Balancing(GSLB)은 로드밸런싱 중 하나로 전세계 여러 센터로 트래픽을 분산한다.

- 스마트 DNS : 각 서버의 상태 확인하고 DNS 요청에 가장 적합한 서버 IP주소를 반환한다.
  - 가장 응답 시간 빠른 서버 선택
- 주 데이터 센터의 장애시 DR센터로의 빠른 전환 필요
  - 이를 위해 **DNS TTL을 최소화하기**. TTL이 1시간이면 1시간 동안은 로컬 캐시에서 처리하라는 의미
    - TTL을 0으로 하면 매번 물어보라는 뜻. 이를 통해 장애시간을 최소화화할 수 있다.



다음시간



##IDS - Intrusion Detection System

IDS는 침입 탐지 시스템으로 악성 활동의 침입을 감지하는 보안 도구이다.

4가지로 분류 가능하다.

1. 네트워크 기반 IDS
2. 호스트 기반 IDS
3. 시그니처-based
   - 시그니처는 탐지 규칙으로 IDS가 악성 패킷을 식별하는데 사용하는 패턴이나 조건을 정의한다.
   - 일반적으로 문자열 매칭을 사용해 패킷을 검사한다.
   - 보안 장비에 공격 패킷에 해당하는 string을 저장해둠. 만약 5000개를 저장해뒀으면(탐지 규칙이 5000개) 하나의 패킷에 대해 5000개의 스트링 매칭을 다 해봐야함
     - 팻킷에 5000개중 하나라도 감지가 되면 악성으로 판단
4. anomaly-based



- 용어 정리

  - Alert/Alarm : 공격이라고 판단했을때 알람을 보내주는 것

  ​

  - True Positive : 실제 악성, 예측 악성
  - False Positive : 실제 정상, 예측 악성
  - False Negative : 실제 악성, 예측 정상
  - True Negative : 실제 정상, 예측 정상

positive면 예측이 악성이다. 

- True는 잘 맞춘거고 Positive는 알람을 울린 여부라고 생각
  - Alarm filtering : 오탐(false positive)를 거르는 것



## 알람 피로 (Alarm Fatigue)

알람 alert가 너무 많이 떠서 피로해지는 문제. 

실제로 모든 알람을 확인할 수 없는 문제. 그 중 유의미한 공격를 찾아내야 하는 문제.

최근 효과적인 자동 탐지기술 ai를 활용한다.



## DDos

tcp syn 패킷을 많이 보내서 서버를 죽이기.

dos 공격에서 syn flooding 공격이다.

ip 스푸핑을 함께 사용해 공격을 수행한다.



dos 공격 중 ddos 공격이 있다. 여러 대의 컴퓨터를 사용해 공격해 서비스를 중지시킨다.



## ddos : botnet

![image](https://github.com/hhzzzk/studyLog/assets/67236054/4d1fe6ef-ec91-48e8-94bd-af7660f1abb6)



ddos는 여러 대의 pc 확보가 관건인데

좀비pc를 bot이라고 한다.

봇넷은 3가지로 구성된다.

1. 봇 마스터 : 봇넷 지휘자, 감연된 pc인 봇을 제어하고 명령 내린다
2. 봇 : 감염된 pc
3. c&c서버 : 봇마스터가 봇들에게 명령을 내리고 제어하는 중앙 서버다.



**해커 : c&c서버의 추적**

c&c서버는 공격자들의 거점, 아지트므로 추적되면 안된다.

특정 도메인 네임으로 접속하는데 시간마다 동기화돼서 바뀌도록 하면

랜덤으로 생성하는데 시간으로 랜덤 넘버를 생성한다. 이를 통해 도메인 이름을 생성한다.

이게 DGA, 도메인 생성 알고리즘이다.



## IPS - Intrusion Prevention System

IPS는 사전에 방지한다는 것으로

IDS + Firewall이다. 사전에 막겠다는 뜻

ids로 탐지해서 alert 발생하면 실시간으로 해당 패킷의 ip를 방화벽에 등록해 차단하는 것



## IPS : IP 스푸핑을 방지

DDOS를 방어한다.

- IP 스푸핑을 방지하는 기능이 있다.
- 트래픽을 관리해 처리한다.



![image](https://github.com/hhzzzk/studyLog/assets/67236054/5b1340c0-e7bf-48e7-92c7-5569fd9446da)

싱크 패킷을 사용해 공격당했을 때 봇은 IP 스푸핑을 한 상태다.

(a) 공격당했을 때 : 봇이 싱크 패킷을 보내기만 해도 희생자는 자원을 소모하게 된다.

(b) IPS의 안티 디도스를 사용하면!

- 싱크 패킷이 시스템에 와서 시스템이 싱크어크패킷을 답장한다. == IPS는 메모리를 잡고 있지 않으므로 리소스를 소모하지 않는다!!!!!!!!!
- 싱크어크 답장할 때 ISN을 함께 보낸다.
  - ISN = h(s_ip, s_port, d_ip, d_port, key, time)
  - 해시함수 처리한다. 여기서 키는 IPS 장비만 알고 있는 비밀 키값이다.
- ISN도 IPS에서 기억하고 있지 않는다. 만약 어크 패킷 답장이 오면 그 때 다시 ISN을 계산해 검증한다.


