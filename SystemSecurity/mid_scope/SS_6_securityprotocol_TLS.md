# SS_6_securityprotocol_TLS

```
Secure Socket Layer/Transport Layer Security
Transport Layer Security
TLS Handshake protocol
TLS version 1.3
Case Study of JAVA SSL
```



## Secure Socket Layer (SSL)

보안 소켓 레이어는 데이터 통신을 암호화하고 보호하기 위한 프로토콜과 기술의 집합이다.

주로 웹 서버와 클라이언트 간의 통신에서 사용되며 인터넷 상에서 데이터의 안전한 전송을 위한 핵심 보안 메커니즘 중 하나이다.

- 전송 계층 보안 서비스
- 원래는 넷스케이프에서 개발됨, 버전3은 공개의견을 반영해 설계됨
- 신뢰할 수 있는 end-to-end 서비스를 제공하기 위해 TCP를 사용한다.
- SSL은 두 개의 프로토콜 레이어를 가지고 있다.
- 이후에는 TLS(전송 계층 보안)으로 알려진 인터넷 표준이 되었다.




## Transport Layer Security(TLS)⛄

전송 계층 보안은 SSL 버전 3.1로부터 발전한 것이다. SSLv3과 유사한 구조를 가지지만 일부 차이가 있다.

- 레코드 형식의 버전 번호에서의 차이 : TLS에서는 레코드 형식의 버전 번호가 다르다.
- MAC로 HMAC 사용 (데이터 무결성 검증에 사용)
- 암호화 키를 확장하는데 의사 랜덤 함수를 사용
- 추가 경고 코드 도입, 통신 도중 발생한 문제에 대한 정보 더 상세히 제공
- 암호화 및 인증 방식 변경, 더 강력한 보안 제공



## TLS 아키텍처⛄

![image](https://github.com/hhzzzk/studyLog/assets/67236054/719677fc-a90e-4ae7-8097-354cab647d6d)

**Handshake Protocol**

- TLS 연결은 핸드셰이트 프로토콜을 통해 시작한다. 여기서 클라이언트와 서버 간의 초기 통신 이뤄진다.
- 클라이언트는 서버에게 안전한 연결을 설정하고 요청한다. 일반적으로 HTTPS에서 발생한다.
- 서버는 클라이언트의 요청을 수락하고 서버의 디지털 인증서(서버의 공개키와 인증정보)를 클라이언트에 제공한다.
- 핸드셰이크 프로토콜을 통해 클라이언트와 서버는 상호 인증을 수행하며 서로의 신원을 확인한다. == 중간자 공격 방지
- 핸드셰이크 과정에서 클라이언트와 서버가 세션 키를 교환하여 이후 데이터 통신을 암호화한다.

**TLS Record Protocol**

- 핸드셰이크 후 실제 데이터 전송은 레코드 프로토콜을 통해 이뤄진다.
- 레코드 프로토콜은 데이터의 암호화, 무결성 검사, 복호화 및 데이터 압축을 처리한다.
- 데이터는 레코드로 분할되어 전송되며 이러한 레코드는 암호화 및 복호화되며 무결성을 확인하는데 사용된다.



## TLS 프로토콜의 특징⛄

- TCP(전송 제어 프로토콜)위에서 작동한다.

  - TCP는 안정적이고 신뢰성 있는 데이터 전송을 담당하여 TLS는 이를 통해 데이터의 보안성을 추가한다.

- TLS는 자체 단위인 **레코드**를 사용한다.

  - 레코드는 헤더와 페이로드로 구성된다. 헤더에는 레코드유형과 길이 정보가 포함되며 페이로드에는 실제 데이터 또는 메시지가 포함된다.

  - ### 레코드의 4가지 유형

    1. 사용자 데이터 : 실제 앱 데이터를 나타내며 사용자와 서버간의 실제 정보 교환에 사용된다.
    2. 핸드셰이크 메시지 : 핸드셰이크 프로토콜에서 사용되는 메시지가 포함된 레코드
    3. 경고 : TLS에서는 서로에게 경고 메시지를 보내고 받을 수 있다. 연결 끊김, 데이터 무결성 위반 등
    4. 암호 명세 변경 Change cipher spec : 데이터 전송에 사용되는 암호 명세 변경을 나타낸다.이는 실제 데이터 암호화를 활성화하거나 비활성화하는 데 사용된다.



## TLS session⛄

TLS 세션은 TLS 프로토콜을 사용하여 통신하는 클라이언트와 서버 간의 연결을 나타낸다. 

네트워크 상에서 일련의 TLS연결을 관리, 다양한 보안 매개변수와 정보를 저장한다.

- 핸드셰이크 프로토콜에 의해 생성된다.
- 암호화 알고리즘, 인증 방법, 세션 키, 디지터 인증서 및 기타 보안 매개변수를 저장한다.
  - 이러한 매개변수는 세션 동안 데이터의 암호화와 무결성을 보호한다.
- 여러 개의 TLS 연결에서 공유될 수 있다.
  - TLS 세션은 재사용될 수 있다. 



## TLS Handshake Protocol⭐⭐⭐⭐⭐ 

TLS 연결 설정을 위해 사용된다. 서버와 클라이언트가 다음과 같은 작업을 수행하게 한다.

- 서로 인증
- 암호화 및 HMAC 알고리즘 협상
- 사용될 암호화 키 협상

단계

1. 보안 기능 설정
2. 서버 인증 및 키 교환
3. 클라이언트 인증 및 키 교환

> 아래 그림은 TCP 3way 핸드쉐이크 끝난 이후이다.

![](https://velog.velcdn.com/images/vpdrnls/post/9cb2f7a0-b521-46d1-92ff-ecd725e64b77/image.png)

### 🌕client_hello🌕

TLS 핸드셰이크 프로토콜의 첫 번째 메시지로, TLS 연결 설정 과정에서 클라이언트가 서버에게 보내는 메세지이다.

**ciphers I support** : ciphers I support에 "ECDHE_AES_SHA-256"은 순서대로 공개키, 대칭키, 해쉬함수 암호화 알고리즘으로 앨리스는 이 3가지 암호화가 가능하다. 내가 사용 가능한 암호화들 리스트를 보내는 것이다. 밥이 해당 ciphers 중에 한 쌍을 선택한다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/b401ac7f-1ecf-4a9c-823c-df0224fd2f6a)

**R(alice)** : 랜덤 숫자.

---

- **암호 스위트(Cipher Suite) : 데이터의 보안 및 무결성을 위한 암호 매개변수를 협의**
  - 클라이언트가 지원 가능한 암호화 알고리즘 목록을 포함!



### 🌕server_hello🌕

서버 헬로는 TLS 핸드셰이크 프로토콜의 두번째 메시지로 클라이언트가 서버에게 보낸 클라이언트 헬로 메시지에 대한 응답이다. 

**certificate** : 서버의 디지털 인증이다. 디지털 인증서는 서버의 공개키와 서버의 신원 정보를 포함한다. 인증서는 일반적으로 인증 기관 CA에 의해 서명된다.

**cipher I choose** : 서버는 클라이언트가 제시한 암호화 알고리즘 목록 중에 사용한 암호화 스위트를 선택한다. 서버는 이후 통신에서 선택한 암호화 스위트를 사용해 데이터의 기밀성과 무결성을 보장한다.

밥도 랜덤 넘버 Rbob을 보냄!



![다운로드](https://github.com/hhzzzk/studyLog/assets/67236054/6701d9c3-bbbd-427d-bc5c-d087ae786bee)




### 🌕client_key_exchanged🌕

![image](https://github.com/hhzzzk/studyLog/assets/67236054/32a05c9a-a9d0-4288-a5f1-1a03a32ae68a)



**{S}** : 클라이언트가 비밀키 S를 생성!!! S 절대 중요 앨리스와 밥, 세상에 두 명만 알아야 한다. 절대지켜야됨

​	 *밥의 공개키로 암호화*한다.

**keyed hash of handshake msgs** : 위에서 나눈 메시지들을 다 모아서 키드 해쉬 함수처리, 무결성 체크!

​	키드 해쉬 함수 = 무결성 체크!!! HMAC!!

**K=f(S,Ra,Rb)** : S와 Ra,Rb를 함수 f를 사용해 K라는 세션키를 생성한다.

이러면 6개의 키가 생긴다.

---

K1, K2 : 대칭키로 사용된다. 암호화 및 해독에 사용. 방향에 따라 다르게 사용해 보안 강화 가능하다.

​	**기밀성 보장!!! 대칭키**💗

K3, K4 : 각 대칭키에 대한 이니셜라이즈 벡터다. 암호화 알고리즘의 초기 상태 설정에 사용된다.

K5, K6 : 각 대칭키에 해시 함수 생성할 때 이어붙이기 위한 키 값(HMAC)이다. **데이터 무결성 보장**💗하기 위해 사용된다.



💗tls 프로토콜은 지금 서버 인증서만 쓰는 상황이라고 한다면 기밀성과 무결성이 만족이 되는 프로토콜💗

시험에 나오겠죠..당근..

"여기까지 질문 일단 되게 중요하고요. 시험에 나겠죠 예

앞에서 우리가 대칭키, 공개키 해시 함수 써서 효과적으로 키 교환해서 어쩌고저쩌고 해라라는 거 시험에 난다 그랬어. "

![🌲](C:/Users/dkxl1/Downloads/가로사진/🌲.jpg)

## TLS Non-repudation

위에까지의 내용은 인증만 가지고 데이터 기밀성, 무결성은 지켰는데 여기에 부인 봉쇄를 추가하고 싶다 하면

앨리스도 자신의 개인키를 사용해 서명해야 한다.

클라이언트도 인증서해서 하면 되는데 그럼 복잡해져서 대부분 여기까지는 안한다.



@

## TLS Change Cipher Spec Protocol

TLS 변경 암호 명세 프로토콜

- TLS 핸드셰이크 과정 중의 특정 메시지이다. 이 메시지가 보내지면 암호화 스위트 키가 변경되어 통신이 암호화된다. 이는 핸드셰이크 과정에서 협의된 암호 설정을 활성화시키는 역할을 한다. 

## TLS Alert protocol

TLS 경고 프로토콜

- TLS 관련 경고를 상대에게 전달한다. 경고는 2가지가 있다.
- 치명적 경고 : 예상치 못한 메세지, 잘못된 레코드 MAC, 압축 해제 실패, 핸드셰이크 실패 등
- 경고 : 연결 종료 알림, 인증서 없음, 잘못된 인증서, 인증서 폐지, 인증서 만료 등



⛄

## TLS 보안 ⭐⭐

![image](https://github.com/hhzzzk/studyLog/assets/67236054/8c3e442a-d005-4e3c-88c1-3b826ab15f4c)

1. 무결성
   - TLS에서는 메시지 무결성을 달성하기 위해 HMAC를 사용한다.
2. 기밀성
   - TLS에서는 핸드셰이크 프로토콜에 의해 정의된 공유 비밀키를 사용해 대칭 암호화를 수행한다.
     - 대칭 암호화는 메시지의 송수신자가 같은 비밀키를 공유하여 이로 암호화 복호화한다.
   - 암호화 알고리즘으로는 AES나 IDEA를 사용할 수 있다.
   - 암호화 전에 메시지를 압축한다.

⛄

## SSL(TLS) Record Protocol Operation

![image](https://github.com/hhzzzk/studyLog/assets/67236054/c9d40e36-dfe5-491b-b659-fa654fe6d71d)

**Data** : TLS 프로토콜은 먼저 상위 수준 데이터를 받는다. 일반적인 웹 브라우저와 웹 서버 사이에서 전송되는 웹 페이지 내용 등

**Fragment** : 데이터는 작은 블럭인 프래그먼트 단위로 분할된다. 

**Compress** : 프래그먼트가 압축된다.

**Add MAC** : 데이터 블럭, 프래그먼트에 대한 MAC가 생성된다. MAC는 데이터의 무결성 검증에 사용된다.

**Encrypt** : 암호화, 생성된 MAC와 프래그먼트는 공유된 비밀 키를 사용해 대칭 암호화 알고리즘을 통해 암호화된다. 데이터 기밀성!

**SSL 레코드 헤더 추가** : 암호화 및 MAC가 적용된 데이터 블럭에 SSL 레코드 헤더가 추가된다. 이 헤더는 데이터의 길이와 유형을 식별하고 전송된 데이터 블럭이 TLS 프로토콜로 올바르게 처리되도록 돕는다.

