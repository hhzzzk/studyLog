# SS_2_symmetrickey_2_(stream_cipher)

```
Symmetric encryption
Classical substitution ciphers
Crypto analysis
One time pad
DES
Modes of operation
Triple DES
AES
Stream Cipher(RC4)
```



## 개요

3가지 중요한 보안의 알고리즘

대칭키 / 비대칭키(공개키) / 암호학적 해쉬 함수



## 대칭키 암호 알고리즘의 두 분류

대칭키 암호 알고리즘 크게 2가지다.

1. 블록 싸이퍼
   - 긴 메시지가 주어졌을 때 메시지 길이를 모르므로 동일한 블록 크기로 잘라 각 블록별로 암호화 시킨다.
2. 스트리밍 싸이퍼
   - 메시지가 주어졌을 대 앞에서부터 1바이트 가져오고 암호화하고 1바이트 가져오고 암호화하고 반복한다. 음악 재생하는 것처럼 앞에서부터 쭉 암호화한다.

지난 시간에 블록 사이퍼에 해당하는 DES와 AS의 구조에 대해 배웠다.

여기서 스트리밍 사이퍼에 대해 배운다.



원타임 패드 : 메시지가 주어지면 앨리스와 밥이 메시지와 동일한 크기의 랜덤 넘버를 생성해놓고 이것을 원타임 패드 키이다. 그걸 원본 메시지랑 exclusive or하면 된다.

- 문제는 메시지의 길이를 모르는 상황에서 매번 앨리스와 밥이 만나 해당 길이만큼의 랜덤 넘버 만드는 것이 힘들다. 현실적으로 불가능.
- 그래서 블록 사이퍼에서는 현재 기준으로 256비트 정도의 대칭키를 만들어두고 블록 단위로 암호화한다. - 현실적으로 가능



## 스트림 싸이퍼의 기본 아이디어

원본 메시지의 길이는 모르지만 앨리스와 밥이 256비트 정도의 대칭키를 만들어 공유하고 

대칭키를 입력으로 받아 랜덤한 비트를 무한히 생성해내는 랜덤 넘버 제너레이터를 만들 수 있다면 ?

40페이지

![image](https://github.com/hhzzzk/studyLog/assets/67236054/5629d66f-fb46-48c6-8775-208c02daeb8b)

M이 원본 메시지고 암호화된 Ci를 어떻게 생성하냐면

랜덤 넘버 생성기에 들어가는 키값을 앨리스와 밥이 공유하고 있다.

> 앨리스와 밥은 공유된 키값을 사용하여 랜덤 넘버 생성기를 구현?
>
> 랜덤 넘버 생성기로 스트림 키의 각 바이트를 생성한다?

해당 스트림 키의 i번째 바이트 == StreamKeyi와 메시지를 XOR하면 된다. 끝

앨리스와 밥은 랜덤 넘버 제너에이터를 만드는 같은 알고리즘을 가진다. 

이런 알고리즘이 여러 개 잇는데 RC4 등이 있다.



## XOR 연산, exclusive or

저번시간...

![image](https://github.com/hhzzzk/studyLog/assets/67236054/1b6c05ca-518f-4404-a3f8-7ab969756ee3)

두 비트가 다를 때 1을 리턴, 같으면 0을 반환한다.



## RC4

원본 메시지에서 i번째 바이트를 가지고 오고

키 제너레이터에서 생성한 i번째 키를 가져와

둘을 XOR해서 보내면 끝



## Attacks

암호화된 메시지를 공격하는 방법?

![image](https://github.com/hhzzzk/studyLog/assets/67236054/11e29270-db5f-41fb-9c98-97bd2061a9c7)



​	💙**4가지 공격**💙

1. ciphertext only attack : **공격자는 암호화된 메시지만** 가진다. 가장 어려운 케이스.
2. known plaintext attack : 공격자는 **일부 원본 메세지와 해당 메시지의 암호화된 버전**을 가진다. 공격자는 두 정보의 상응 관계를 활용할 수 있다.
3. chosen plaintext attack : 공격자는 **일부 원본 메시지를 !선택!하고 그에 상응하는 암호문**을 얻을 수 있다. 더 효과적으로 공격 가능하다.
4. chosen ciphertext attack : 공격자는 **일부 암호문을 선택하고 그에 상응하는 원본 메시지**를 얻을 수 있다. 


---

아래 참고용~

## SS_Stream Cipher(RC4)_(ch2-대칭키-N)



![૮₍ ˃ ⤙ ˂ ₎ა](C:/Users/dkxl1/Downloads/가로사진/૮₍ ˃ ⤙ ˂ ₎ა.jpg)

## Stream cipher 💙

스트림 암호는 메시지를 암호화하기 위한 기술 중 하나로, 원타임 패드를 생성하는데 사용된다.

- 스트림 암호에 의해 생성된 One time pad는 랜덤 숫자 생성기이다.
- 메세지를 비트 단위로(스트림으로) 처리한다.
- have a pseudo random keystream, 랜덤 숫자 키스트림을 생성한다.
- 랜덤 키스트림과 plaintext를  비트 단위로 XOR 연산해 결합한다.
- 스트림 암호의 키스트림은 랜덤이므로 메시지의 통계적 특성을 완성히 파괴한다. 이로 인해 암호화된 메시지가 보호된다. 이러한 속성 때문에 원타임 패드라고 불린다. 원타임 패드를 사용하면 한 번 사용한 키를 다시 사용하지 않는 한 매우 강력한 암호화를 제공한다.

>  Ci = Mi XOR StreamKeyi



​	💙**스트림 암호 설계 고려사항**💙

- 반복없는 긴 주기
- 통계적으로 무작위
- 충분히 키가 커야 한다.
- large linear complexity
  - 적절히 설계된 경우, 동일한 크기 키를 가진 블록 암호와 동일한 수준의 보안을 제공한다. 그러나 보통 블록 암호보다 간단하고 빠르다.



​	💙**RC4의 특징**💙

- RSA DSI 소유의 특허 암호
- 변수 키 크기를 지원하는 바이트 기반의 스트림 암호
- 키는 8비트 모든 값의 무작위 순열을 형성한다. 이 순열을 사용해 입력 정보를 바이트 단위로 처리하고 스크램블링(혼란)한다. 이 과정을 통해 원본 데이터를 암호화된 스트림으로 변환한다.



​	💙**RC4 구현**💙

+

​	💙**4가지 공격**💙

1. ciphertext only attack : 공격자는 암호화된 메시지만 가진다. 가장 어려운 케이스.
2. known plaintext attack : 공격자는 일부 원본 메세지와 해당 메시지의 암호화된 버전을 가진다. 공격자는 두 정보의 상응 관계를 활용할 수 있다.
3. chosen plaintext attack : 공격자는 일부 원본 메시지를 선택하고 그에 상응하는 암호문을 얻을 수 있다. 더 효과적으로 공격 가능하다.
4. chosen ciphertext attack : 공격자는 일부 암호문을 선택하고 그에 상응하는 원본 메시지를 얻을 수 있다. 