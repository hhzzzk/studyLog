# SS_Encryption and Decryption(ch1_intro-3)

🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳🔳

## Encryption and Decryption

메세지 M은 plaintext라고 한다. 암호화한 메세지는 cipgertext라고 한다.

Encryption : M을 암호화 알고리즘 E를 사용해 cipertext, 암호문으로 변환하는 과정.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/140580d5-029e-4246-be58-2a0e9fe34385)



- 암호화 및 복호화 알고리즘(encrypition and descryption)은 앨리스와 밥 이외의 다른 사람이 암호화된 C에서 원본 m을 복구하기 어렵도록 설계된다. 
- 따라서 암호문 C는 이미 암호화되어 해독하기 어려운 형태이므로 공격자에 의해 도청될 수 있는 위험한 채널을 통해서도 전송될 수 있다.

## Cryptosystem - 암호체계

암호체계의 기본 구성 요소 7가지

1. 가능한 평문(plaintext)의 집합
2. 가능한 암호문(ciphertext)의 집합
3. 가능한 암호화 키(encryption keys)의 집합
4. 가능한 복호화 키(decryption keys)의 집합
5. 암호화 키와 복호화 키 사이의 대응 관계
6. 사용할 암호화 알고리즘
7. 사용할 복호화 알고리즘

### Caesar Cipher - 시저 암호

시저 암호는 간단한 치환 암호의 일종으로 각 글자를 알파벳 상에서 일정한 거리만큼 잎이나 뒤로 이동해 암호화한다. (HELLO > EBIIL)



### a. Symmetric Cryptosystems

앨리스와 밥은 공유 비밀키를 가지고 있다. 공유 비밀키는 암호화, 복호화에 모두 사용된다.

Symmetric Key Distribution : 통신하는 모든 당사자 쌍마다 !별도의! 비밀 키를 공유해야 한다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/cf4673d3-0db0-475a-b221-9a000668d90a)

대칭키는 4명이 서로에게 다 통신하려면 총 6개의 키가 필요하다. (3*2)

(5명 - 20개, 6명 - 30개)

### b. Public-Key Cryptography

밥은 개인키와 공개키를 가진다.

앨리스가 밥에게 메시지 보내는 단계

1. 밥의 공개키로 메세지 암호화. 그 C를 밥에게 전송
2. 밥은 자신의 개인키로 복호화. 메시지 획득

Public Key Distribution : 암호화 복호화에 서로 다른 키가 사용된다.

- 각 수신자마다 하나의 키만 필요하다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/da37ebb4-ed15-47db-9a0d-f1fb5745c706)

비대칭키, 공개키는 4명이 서로에게 통신하려면 한 사람마다 공개키와 개인키, 8(2n)개의 키가 필요하다.

(5명 - 10개, 6명 - 12개)

### c. Digital Signatures

서명은 자신의 개인키로 암호화하는 것이다. 이 경우 누구나 해당 공개키를 알고 있다면 복호화가 가능하다. 복호화한 결과와 원본 메세지 m을 비교해 일치하면 이것에 해당 사람의 개인키로 서명되었음을 알 수 있다. 

이로써 메시지의 무결성 intergrity와 보낸 사람의 신원을 확인할 수 있다.

### d. Cryptographic Hash Functions 💙

암호 해시 함수. 메시지나 데이터를 입력받아 그에 대한 고유한 체크섬 값을 생성하는 함수이다. 데이터의 무결성을 확인하고 보호하는데 사용된다.

- 일방향성 :  H(m)=Y처럼 메세지에 해시 함수를 적용하면 체크섬 Y를 생성할 수 있어야 한다. 그러나 반대로 체크섬 Y를 가지고 원본 메세지를 찾는 것은 매우 어려워야 한다. 즉 역방향 원본 추척을 어렵게 한다.
- 충돌 저항성 : 서로 다른 두 메세지를 입력으로 하는 경우 해쉬 함수를 적용한 두 개의 결과가 서로 다른 체크섬을 생성해야 한다.

### Message Authentication Codes - MAC

메세지 인증 코드, 데이터 무결성을 확인하고 보호하기 위한 암호학적 도구이다.

- 앨리스와 밥이 공유하는 비밀키를 통해 작동한다.
- 메시지 인증 코드를 사용해 앨리스가 밥에게 보내는 메세지가 송신 중간에 변경/손상되지 않았는지 확인 가능

![image](https://github.com/hhzzzk/studyLog/assets/67236054/1ddda7ea-67ed-4783-a37e-db160f7a3a7d)

단계

1. 앨리스와 밥은 비밀 키 K를 공유한다.
2. 앨리스가 메세지를 보냈 때 H(K||M)(==해시함수에 K와M 문자열을 연결)을 계산한다.
3. 앨리스는 원본 메세지와 계산된 MAC를 밥에게 보낸다.
4. 밥은 H(K||M)을 다시 계산한다. 그 결과를 비교한다. 두 값이 일치하면 메시지의 무결성을 확인 가능하다.

### Digital Certificates

디지털 인증서 : CA, 인증기관이 신원과 그 신원에 대한 공개 키 간의 바인딩을 디지털로 서명한다.

