# SS_한시간에 끝내는 보안프로토콜(사전동영상)

[PPT](https://gaia.cs.umass.edu/kurose_ross/ppt.php)

# 한시간에 끝내는 보안프로토콜

## 목차

Chapter 8 roadmap

__8.0 Crypto Protocol: Bird's-eye view (new) __

8.1 What is network security?
8.2 Principles of cryptography 

8.3 Message integrity, authentication 

8.4 Securing e-mail

8.5 Securing TCP connections: SSL

8.6 Network layer security: IPsec 

8.7 Securing wireless LANs

8.8 Operational security: firewalls and IDS



# 0.0 Crypto Protocol : Bird's-eye view

교수님이 추가하신 부분. 전체적인 조감도? 느낌으로 보자

보안에서는 기본적으로 앨리스가 보내는 사람 밥이 받는 사람이다.

1. 앨리스는 "m"을 밥에게 보낸다.
2. 이때 지켜져야 하는 것들. (confidentiality 기밀성, integrity, non repudation, effciency)

- 🍁 대칭키 (symmetric-key 알고리즘)

  - Encryption(암호화) : Ks(m)
  - Decryption(해독) : Ks(Ks(m))
  - s라는 키로 암호화된 m을 해독하려면 마찬가지로 Ks로 해독해야함

- 🍁 비대칭키 (asymmetric-key 알고리즘)

  - '-'는 private 키, '+'는 public 키이다.

    > Encryption(암호화) : +Kb(m)
    >
    > Decryption(해독) : -Kb(+Kb(m)))

  - 밥의 공개키로 암호화된 경우 대응하는 밥의 개인키로 해독해야 함

  - 반대로 개인키로 암호화된 경우 sign, 서명이라고 함

    - 공인인증서, 인터넷 뱅킹에서 많이 이용

    > Sign : -Ka(m)
    >
    > Verification(인증) : +Ka(-Ka(m)))

- 🍁 암호학적 해쉬 cryptographic hash

  > Hash : H(m)




# 0.1 Crypto Protocol : Bird's-eye view


<img src="https://github.com/hhzzzk/studyLog/assets/67236054/652b3415-4489-4fb8-b7ba-c29af1e2cfcc" alt="이미지" width="500">

Problem > 인터넷 세상에서 앨리스가 메세지를 밥에게 전달하려고 한다. 앨리스와 밥은 각각 비대칭키 개인, 공개키를 가짐

1. 밥이 공개키를 전송

2. 앨리스는 Ks 세션키(대칭키)를 생성

   밥의 공개키로 세션키를 암호화 +Kb(Ks)

   자신의 세션키로 메시지를 암호화 (다른 과정에 비해 메세지 크기와 시간 비례하는 부분, 시간이 비교적 더 걸린다.)

   해쉬함수를 통해 메세지 크기 작게 한다.

   자신의 개인키로 해쉬처리된 메세지를 암호화, 전자서명처리(sign=개인키로암호화)함

3. 앨리스는 3가지를 밥에게 전송

4. 밥은 자신의 개인키로 앨리스가 생성한 세션키를 해독.

   얻어낸 세션키로 메세지 해독. 해쉬함수 처리함 > H1(m)

   공개된 앨리스의 공개키로 해독, > H2(m)

   	> 그렇게 얻어낸 해쉬처리된 메세지 두 개를 비교해 같은지 여부로 판단한다.

     1. 앨리스는 repudation 할 수 없음. non-rep 충족
     2. intergrity : 중간에 메세지가 변했다면 2개의 H(m) 이 일치하지 않았을 것임. 충족
     3. efficiency : 서명은 느린 작업, 메세지가 굉장히 클 수 있음. 그래서 해쉬함수로 메세지를 작게 만들어놓고 서명작업을 함.


# 0.2 Crypto Protocol : Bird's-eye view

## Q. 밥의 공개키가 정말 밥의 것일까? (+Kb)

<img src="https://github.com/hhzzzk/studyLog/assets/67236054/07225267-08ca-45d6-b744-c6057fb78c7e" alt="이미지" width="500">

>  CA : 인증기관의 도입. 공신력 있는 기관의 인증

인증기관에도 공개키, 개인키 존재

밥은 자신의 공개키를 인증기관에 제출한다. 💎__인증기관은 개인키로 서명해준다. __

- 💎 이게 인증서, 공인인증서/사설인증서 

앨리스는 이게 밥의 공개키를 신용

#### 그러나 인증기관의 공개키는 신뢰할 만한가?

브라우저, 크롬같은 곳에 존재함. 

#### 신뢰할 수 없는 인증서 문제 > 신뢰하면 해당 기관의 암호를 다 믿음



