# AI_3_Artificial Neural Networks

```
인공신경망
퍼셉트론
다층 퍼셉트론
오류 역전파
```

## 인공 신경망 종류

- 전방 forward 신경망과 순환 recurrent 신경망
- 얕은 shallow 신명망과 깊은 deep 신경망
- 결정론적 신경망과 확률론적 신경망


# 퍼셉트론

- 인간 뉴런을 모방한 최초의 인공 신경망
- 노드, 가중치, 층과 같은 개념을 도입하고 학습 알고리즘을 제시



## 퍼셉트론 구조

![image](https://github.com/hhzzzk/studyLog/assets/67236054/a83f96fa-430e-4332-968f-1b017ecdb619)



- 입력층과 출력층을 가진다.

  - 편향 bias 노드 : 입력층이나 은닉층의 각 노드마다 추가적으로 존재하는 상수이다. 항상 1이 입력된다.

    ​				각 노드가 얼마나 쉽게 활성화되는지 조절하는 역할

- 각 입력은 해당하는 가중치와 함께 연결된다.

- 입력과 가중치의 곱(내적)이 계산되어 더해진다. 선형결합

- 합산된 결과는 활성 함수를 통과해 출력을 생성한다.

  - 일반적으로 계단함수나 시그모이드 함수를 사용한다.
  - 활성 함수는 입력에 대한 비선형적인 변환을 제공해 퍼셉트론이 비선형적인 관계를 학습하도록 한다.

- 활성화 함수의 출력은 이후 퍼셉트론의 예측 또는 활성화 값으로 사용된다. 출력층은 한 개의 노드이다.



7w1

10/16

## 퍼셉트론 동작

퍼셉트론은 입력값과 가중치를 곱하고 더하는 선형 연산을 수행한다. 이렇게 계산된 값에 활성함수(계단함수)를 적용해 최종 출력을 얻는다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/6003c925-1048-4493-b030-3614e73bb7ca)

- y=τ(s)가 계단함수이다.  계단함수는 입력값이 임계값 threshold를 넘으면 1을 출력하고 그렇지 않으면 -1을 출력한다.
- s : 계단함수의 입력으로 들어가는 s는 선형연산이 수행된 결과이다. 즉 각 입력값인 x와 가중치 w를 내적한 값이다. 

![image](https://github.com/hhzzzk/studyLog/assets/67236054/1e5a469c-ad55-449f-9f31-39c96304da6c)



- w0'는 편향이다. 편향을 입력 벡터 x에 1을 추가하고 가중치 벡터 w에 추가해 식을 s에서 w0'를 생략할 수 있다. 
  - 편향을 쓰는 이유는 x는 편향을 추가한 차원을 맞추기 위해 1을 추가하고(편향을 추가하려고) w0을 통해 기준값, 임계값을 맞출 수 있다. 일종의 영점, 초점을 맞추는 작업이다.
  - 편향은 주어진 입력 데이터에 대해 모델이 얼마나 쉽게 활성화되는지 조절하는 역할을 한다.
- 이렇게 편향을 추가한 s를 비선형 연산인 계단함수, 활성함수에 적용해 식을 정리한다. 
  - 표현이 용이해졌다.



## 퍼셉트론 동작 예시

AND나 OR 게이트 x 입력과 가중치 예제를 들 수 있다.

가중치에 편향 차원을 추가하고 x에도 1을 추가한다. 반영해 내적, s를 계산하면 0을 기준으로 한 계단함수에서

AND, OR 게이트가 제대로 동작하는 것을 확인할 수 있다.



## 퍼셉트론 동작 예시의 기하학적 의미

![image](https://github.com/hhzzzk/studyLog/assets/67236054/6cc5e694-4fef-4552-9f89-d60fccd47c89)



2차원 특징 공간에서 가중치(편향 포함)를 반영하고 x의 식을 정리하면 직선의 방정식이 정리된다.

이러한 직선은 주어진 특징 공간은 1과 -1의 두 부분 공간으로 분할하는 분류기 역할을 한다. == 선형 분류기

![image](https://github.com/hhzzzk/studyLog/assets/67236054/a26c2fbb-b42e-4be4-ba8a-373add546fae)



3차원에서는 결정 평면, 4차원 이상에서는 결정 초평면

다차원 공간에서 퍼셉트론은 초평면을 사용해 공간을 분할한다. 

- 이는 각 차원에 대한 가중치와 입력값의 곱의 합에 대한 결정 경계를 나타낸다.



그림에서 보면 편향이 없다. 왜지?

T는 활성함수의 임계값 threshold로 활성화 함수의 출력을 결정하는 역할을 한다. 기본적인 계단함수는 0을 기준으로 1,-1중 하나로 출력하는데 임계값을 설정하면 임계값을 기준으로 크면 1, 작다면 0이나 -1을 출력할 것이다.

## +편향과 임계값의 차이?

편향은 모델의 결정경계를 원점이 아닌 다른 곳으로 이동시킬 수 있다. 편향이 없다면 결정경계는 원점을 지날 것이다. 편향을 통해 이 경계를 움직일 수 있다. 데이터가 원점을 중심으로 대칭적이지 않을 때 유용하다. 선형 연산을 할 때 처리된다.

임계값은 활성화 함수에서 모델의 출력을 결정할 때 사용된다. 활성화 함수의 입력값을 임계값T를 기준으로 2분할해 크면 1 작으면 -1로 분할한다. 



## 퍼셉트론 학습

퍼셉트론의 동작은 학습을 마친 후, 주어진 입력에서 출력을 생성하는 과정이다. 

100프로로 정확하게 분류하도록 퍼셉트론을 동작시킬려면 *올바른 가중치와 편향을 설정해야 한다.*

데이터가 **선형적으로 분리가 가능하다면** 가능하다.

그러나 데이터가 선형적으로 분리되지 않거나 분류가 불가능한 경우라면 어떻게 할 것인가

- MNIST는  784차원에  6만개  데이터  집합  예처럼  현실  세계는  d차원  특징  공간에  수백~수만  개의  데이터가  존재함

---

![image](https://github.com/hhzzzk/studyLog/assets/67236054/74a9a40c-c00b-42a0-a12e-a1e01874e7ea)



## 일반적인 분류기의 학습 수행 과정

1. 분류기의 가설(모델) 설정 == 퍼셉트론으로 설정
2. 분류기의 목적함수𝐽(Θ)를 정의 > 목적함수가 분류기를 평가하는 정량적 지표이다.
3. 𝐽(Θ)를 최소화하는 Θ를 찾는 최적화 수행



## 퍼셉트론 모델의 학습 수행 과정

퍼셉트론의 목적함수의 조건은 모든 샘플은 선형 분리가 가능함을 가정한다.

## 퍼셉트론 목적함수 조건 3가지

- 𝐽(w) >= 0
- w가 최적이면, 즉 모든 샘플을 맞히면 𝐽(w)=0이다.
- 틀리는 샘플이 많은 w일수록  𝐽(w)는 큰 값을 가진다. 

---

![image](https://github.com/hhzzzk/studyLog/assets/67236054/11dd6553-c00b-44fe-938b-f273f668d988)

결국 목적함수는 오차라고 볼 수 있다. 예측값 y^과 실제값 y와의 차이 (대표적으로 MSE)

이를 최소화로 줄여야 하는데(최적화) 이를 위해 3단계에서 경사 하강법을 사용한다. 

경사하강법은 목적함수 𝐽(Θ)의 미분 정보를 활용해 가중치 w를 다시 갱신하는 것을 반복한다.



## 가중치 갱신 규칙

- 기본적으로 𝐽(Θ)를 미분한 경사도, 그래디언트의 음의 방향으로 가중치를 갱신한다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/f7d845b5-9611-4c7d-a0a8-13163417a293)



Θ는 가중치 벡터

ρ는 학습률(learning rate)

g는 손실 함수(비용 함수) J(Θ)에 대한 가중치 Θ의 편미분

- 𝐽(w)를 wi에 대해 편미분하면 w가 아닌 다른 값은 사라지고 w의 계수?만 남는다. 우항 하나만 남는다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/f5080a59-226d-49a9-b7ff-d4072c2b9e24)



- Y는 예측 오답 데이터 집합이다. 

  ![image](https://github.com/hhzzzk/studyLog/assets/67236054/84d68fec-428c-46f4-8e22-4327392b74d1)

- x는 d개의 입력을 가진다. x11,x12...x1d

  ![image](https://github.com/hhzzzk/studyLog/assets/67236054/d4ac0aba-213c-424b-a8d8-4023417ddebf)

  - xk의 i번째 요소 xki는 해당 가중치에 대한 영향을 나타낸다.
  - 이를 yk와 곱해 실제 값과 예측값 사이의 차이를 계산해 가중치 조정에 반영한다.

- 실제 값 yk와 입력 데이터 xk의 i번째 요소인 xki를 곱한 값들을 모두 더한 것이다. (w는 미분)

![image](https://github.com/hhzzzk/studyLog/assets/67236054/1eb8aece-b9ec-4d96-851f-724f18b3a0a0)

계산한 값을 학습률과 곱해 가중치 갱신에 더한다. 



## re 퍼셉트론의 목적함수 조건

```
- 𝐽(w) >= 0
- w가 최적이면, 즉 모든 샘플을 맞히면 𝐽(w)=0이다.
- 틀리는 샘플이 많은 w일수록  𝐽(w)는 큰 값을 가진다. 
```

조건을 만족하는지 보자

![image](https://github.com/hhzzzk/studyLog/assets/67236054/4a488f89-3081-4477-82b5-6a2db1623fb9)

첫번째 조건은 목적함수가 0보다 크거나 같아야 한다.

​	그림에 점선 기준으로 공간이 2분할된 선형 분류기...

![image](https://github.com/hhzzzk/studyLog/assets/67236054/aa2a1944-5c1c-4d58-94a3-7e859752d3f4)

- 임의의 데이터 xk가 Y, 오답에 속한다면 퍼셉트론의 예측값인 w^Txk와 실제값 yk는 부호가 다르다.
  - 그럼 음수 x 음수 x 얌수, 또는 음수 x 양수 x 음수 조합 둘 중 하나만 가능하므로 목적함수는 항상 양수이다.

두번째 조건은 w가 최적이면 목적함수는 0이다.

- Y가 공집합이라는 뜻이다. 그럴 경우 0이다.

세번째 조건은 틀리는 샘플이 많을수록 목적함수는 커진다.

- Y가 커질수록 목적함수는 큰 값을 가진다. 목적함수는 항상 양수이므로

![image](https://github.com/hhzzzk/studyLog/assets/67236054/a5852826-7d50-4a46-a728-324fa2adeab9)



## 학습률 중요성

학습률은 경험적으로 판단해야... 너무 커도 너무 작아도 안좋다.

## 퍼셉트론 학습 알고리즘 정리

![image](https://github.com/hhzzzk/studyLog/assets/67236054/db11393a-93c2-4ba2-bb5f-fbae7a722f75)

미분값으로 갱신한다. 갱신하는 시점에 따라 풀배치와 스토캐스틱으로 나뉜다.



## 행렬 표기해 간결하게 표기

행렬표기로 배치버전 알고리즘을 수정하면

벡터에서 벡터로 업데이트

```
물론입니다. 다음은 퍼셉트론 학습 알고리즘에 관한 문제입니다.

주어진 퍼셉트론의 초기 가중치 벡터 \(w(0)\)은 \((-0.5, 0.75)\)이며, 초기 편향 \(b(0)\)는 \(0.375\)입니다. 두 개의 입력 특성을 가진 데이터셋을 고려합니다.

1. 데이터 포인트 \(x_1 = (1.5, 2.0)\)이 클래스 'a'에 속한다고 가정합니다. 이 데이터 포인트에 대한 목표값 \(t\)는 -1입니다. 이 때, 주어진 초기 가중치 벡터를 사용하여 이 데이터 포인트의 예측값 \(y\)를 계산하세요.
2. 주어진 학습률이 0.3일 때, 위의 데이터 포인트에 대한 예측 오차를 이용하여 가중치와 편향을 업데이트한 후의 새로운 가중치 벡터 \(w(1)\)와 편향 \(b(1)\)을 계산하세요.

이를 통해 퍼셉트론 학습 알고리즘에 대한 이해를 확인할 수 있습니다.
---
먼저, 주어진 데이터 포인트 \(x_1 = (1.5, 2.0)\)에 대해 예측값 \(y\)를 계산해보겠습니다. 

주어진 초기 가중치 벡터 \(w(0) = (-0.5, 0.75)\)와 편향 \(b(0) = 0.375\)을 사용하여 예측값을 계산합니다. 주어진 데이터 포인트의 첫 번째 및 두 번째 특성을 각각 \(x_1\)과 \(x_2\)라고 합시다. 따라서 예측값 \(y\)는 다음과 같이 계산됩니다.

\[y = w_1(0) \times x_1 + w_2(0) \times x_2 + b(0)\]
\[= -0.5 \times 1.5 + 0.75 \times 2.0 + 0.375\]
\[= -0.75 + 1.5 + 0.375\]
\[= 1.125\]

따라서 주어진 데이터 포인트 \(x_1 = (1.5, 2.0)\)에 대한 예측값 \(y\)는 1.125입니다.

여기서 \(w_1(0)\)은 초기 가중치 벡터 \(w(0)\)의 첫 번째 요소를 나타내며, \(w_2(0)\)는 두 번째 요소를 나타냅니다. \(b(0)\)은 초기 편향을 나타냅니다.
---
두 번째로, 주어진 학습률이 0.3일 때, 위의 데이터 포인트에 대한 예측 오차를 이용하여 가중치와 편향을 업데이트하겠습니다.

주어진 학습률 \(\eta = 0.3\)를 사용하여 가중치와 편향을 업데이트하는 과정은 다음과 같습니다.

먼저, 주어진 데이터 포인트의 목표값은 -1이므로, 오차 \(t - y\)는 다음과 같이 계산됩니다.

\[t - y = -1 - 1.125 = -2.125\]

이 오차를 사용하여 가중치와 편향을 업데이트합니다. 각 가중치 \(w_i\)와 편향 \(b\)의 업데이트는 다음과 같이 수행됩니다.

\[w_i(1) = w_i(0) + \eta \times (t - y) \times x_i\]

\[b(1) = b(0) + \eta \times (t - y)\]

여기서 \(x_i\)는 입력 데이터 포인트의 각 특성입니다. 위의 계산 결과를 대입하여 새로운 가중치 벡터 \(w(1)\)과 편향 \(b(1)\)을 구할 수 있습니다. 이를 통해 새로운 가중치와 편향을 얻을 수 있습니다.
```



- 선형분리가 불가능한 경우에는 무한 반복된다.
  - 정지조건을 추가하는 수정이 필요하다.




## 선형 분할이 안되는 데이터의 경우

타겟과의 간격 차이가 여전히 존재한다. 이를 위해 다층 퍼셉트론을 사용한다.

![yuxi](https://github.com/hhzzzk/studyLog/assets/67236054/1bd29f92-2bbd-44e9-bee6-45e9d9aca222)



## 다층 퍼셉트론

퍼셉트론은 선형 분류기로 활성함수가 미분 불가능한 한계가 있다.

이를 극복하기 위해 다층 퍼셉트론은 은닉층과 레이어의 추가로 공간을 변환해 미분이 가능하게 한다. 

공간을 변환할 때 선형연산과 비선형 연산을 수행하는데

비선형 연산으로 대표적인 것이 시그모이드 활성함수이다. 



이전의 계단함수가 -1,1인 hard 극단적인 출력만을 수행해 미분을 하지 못했다면

시그모이드 함수는 soft, 연속적인 출력을 통해 미분을 가능하게 한다.



## 다층 퍼셉트론으로 XOR 문제 해결 

XOR문제인 논리회로는 선형 분리 불가능했다. 75프로의 정확도 한계가 있었는데

이를 복수의 퍼셉트론을 활용해서 해결해보면

---

![image](https://github.com/hhzzzk/studyLog/assets/67236054/1c8a078b-ea33-421f-b141-3281e32771b5)



퍼셉트론 2개로 공간분할해서 해결이 가능하다. 

## 퍼셉트론 2개를 병합결합한 은닉층의 기하학적 의미

![image](https://github.com/hhzzzk/studyLog/assets/67236054/7120e745-83cb-47c0-9d87-d5aab6720e64)



10/18

7w2

![image](https://github.com/hhzzzk/studyLog/assets/67236054/f3044f7d-7f93-43bd-ae82-c1d0cc1ff0f4)





##  다층 퍼셉트론과 은닉층 일반화

다층 퍼셉트론은 선형 분류기로 여러 개의 필터를 배치한 것이다.



3개의 직선 조합으로 공간을 나눈다. == 레이어, 퍼셉트론의 병렬화

레이어를 반복해 묶기의 반복이다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/261268c7-c979-4bc1-a687-ae9c784de803)



## 다층 퍼셉트론의 비선형연산, 시그모이드

퍼셉트론은 선형연산과 비선형연산을 수행한다.

다층 퍼셉트론의 비선형연산은 이전의 계단함수는 미분이 불가능했다.

계단함수보다 연속적이고 비선형성을 유지하는 연산을 위해 시그모이드 함수를 적용한다.

---

![image](https://github.com/hhzzzk/studyLog/assets/67236054/c0643fd1-5be4-44ef-8073-60acf54ca458)

---

계단함수는 이산적인 출력을 내므로 공간을 딱딱하게 계단형식으로 분할한다. 

시그모이드 연속적인 출력, 부드러운 공간분할한다. 



로지스틱 시그모이드는 0-1사이의 출력이다.

하이퍼블릭 탄센트 시그모이드는 -1~1사이의 출력이다.

> 계단함수를 쓰면 미분정보(경사하강법)을 얻기 어렵다. 그래서 시그모이드를 사용한다.

---

시그모이드를 쓰면 주어진 공간을 점이 아니라 지역, 그 근방으로 그려진다. 미분이 가능한 장점!



## 인공 신경망이 사용하는 다양한 활성함수

![image](https://github.com/hhzzzk/studyLog/assets/67236054/4eee7066-8f0f-48d9-aed6-53fb82e5777e)

시그모이드가 레이어 단위로 존재한다. 

## Gradient Vanishing 그래디언트 소실

레이어가 많을수록 시그모이드가 많다. 그러나 그럴 경우 레이어 미분값이 사라지는 문제가 생긴다.

- 결과값에 시그모이드 미분값을 곱할 건데 이 때 0을 곱하면 0이 되어 경사도가 사라질 수 있다. 그럼 갱신할 수가 없다.


- 시그모이드는 입력이 크거나 작을 경우 변화율이 매우 작아진다. 따라서 역전파 과정에서 이 작은 기울기가 여러 레이어를 통과하면서 누적되면 그래디언트가 소실되는 문제가 발생할 수 있다.

그래서 ReLU가 등장했다. ReLU를 사용하면 그래디언트 소실 문제 해결이 가능하다.



## 다층 퍼셉트론 구조

![image](https://github.com/hhzzzk/studyLog/assets/67236054/b8775acd-da2b-4ee2-9652-719b5b2b12bf)

파란색 노드 하나에서는

​	입력과 가중치의 내적과 비선형함수인 활성함수를 통과해 시그마로 합하는 과정까지가 들어있다.

이런 연산을 수행하는 것은 행렬곱셈과 같다.

> 신경망 레이어의 첫번째 선형 연산은 행렬곱셈이다.



출력이 다시 입력으로 들어가는 과정을 반복한다. 즉 공간을 변화시키는 과정을 반복한다.

---

즉 입력 차원이 아무리 복잡하고 어려워도 레이어를 거쳐가면서

출력 차원에서의 추상화가 반복된다. 이를 통해 특징이 두드러지게 된다.

​	레이어의 특징 추출은 공간의 변화이다.



신경망은 선형과 비선형 연산으로 레이어의 특징 추출하는 것이 목표이다. 이는 공간을 변화시키는 것이다.



## 다층 퍼셉트론 동작

![image](https://github.com/hhzzzk/studyLog/assets/67236054/5776008c-5f80-4cfd-86df-a20cf2dc7cce)

다층 퍼셉트론이 동작하는 과정은 합성함수와 유사하다. 여러 층, 레이어를 반복해서 결과를 도출한다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/82c9f556-6979-4724-829a-1c8276797ba6)

깊은 신경망은 이런 레이어가 4개 이상인 L>=4일 때다.

은닉층 한 층에서는 선형(행렬곱셈)과 비선형연산(시그모이드,ReLU)를 수행한다.



## 다층 퍼셉트론의 노드 연산

은닉층 동작 행렬 표기 (W = U)

![image](https://github.com/hhzzzk/studyLog/assets/67236054/3b69ed03-819c-40f9-8b26-9b287cdeed5c)

x는 입력 벡터, U는 각 레이어의 가중치 행렬이다. τ는 비선형 활성함수이다. 

- 입력벡터에 첫번재 가중치를 곱해서 활성화 함수를 적용한다. = 첫번째 레이어의 출력
- 위의 출력이 다시 입력벡터로 들어가 두번째 가중치 행렬을 곱해 활성화 함수를 적용한다. = 두번째 레이어의 출력

즉 가중치인 W,U의 값을 위의 학습을 통해 최적화된 값을 찾아낸다.



## 은닉층 == 특징 추출기

내적은 벡터 사이의 유사도를 측정했다.

은닉층을 통해 벡터 사이의 유사도가 강하다면 강하게 바꾸고 그렇지 않다면 버리는 과정을 반복해 특징을 추출한다. 일종의 필터효과

- 은닉층은 특징 벡터를 분류에 더 유리한 새로운 특징 공간을 변환한다.(추상화, 특징 추출)

![image](https://github.com/hhzzzk/studyLog/assets/67236054/97158f0c-c8f9-42fe-8c96-49d6d30e29d3)

💛**범용적 근사 이론**💛

은닉층을 통과하며 공간을 변환해간다. 즉 은닉층을 함수의 근사로 활용한다.

퍼셉트론의 병렬화를 통해 여러 개의 직선들의 조합으로 공간을 근사화하는 것이 가능하다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/84d49d2a-41c2-4db1-8a97-dc87a854fcd9)

💛은닉층의 구조는 폭width보다 깊이depth가 성능에 큰 영향을 준다.💛



## 은닉층의 기하학적 의미

은닉층을  통한 특징공간의  변환 

- 행렬  곱: 회전 
- 편향: 이동
- 비선형 함수: 왜곡

## 은닉층 정리

1. 선형대수 측면 : 주요 특징은 강조, 부각시키고 아닌 특징은 줄인다.
2. 분류기의 기하학적 의미 : 분류기인 직선 여러 개로 공간을 분할한다. 구역화한다.
3. 특징 공간 변환 : 레이어 단위로 공간을 변환한다.



## 은닉층 깊이에 따른 장점

![image](https://github.com/hhzzzk/studyLog/assets/67236054/75f91852-2ab3-4fe1-8700-d8bf10268804)

은닉층이 깊어질수록 데이터가 점점 모이는 형태로 공간이 변환되고 구역화된다.

![HD background PC_Laptop](https://github.com/hhzzzk/studyLog/assets/67236054/fd161c0a-06c3-4a48-8ef6-8d330ac24e5b)

ㅠㅠ

# 오류 역전파

기계학습을 통한 목표는 목적함수를 줄이는 것이다. 모델의 성능 판단 지표가 목적함수이다.

대표적으로 MSE(평균 제곱 오차)가 있다. 

## 연산 그래프

![image](https://github.com/hhzzzk/studyLog/assets/67236054/71c0a7fe-7a71-49e8-b6fe-224949e1831c)

하나의 레이어에서 선형과 비선형 연산을 한다는 것을 볼 수 있다.

## 도함수의 종류

1. 스칼라 > 스칼라 : 미분으로 구할 수 있다.
2. 벡터 > 스칼라 : 그래디언트, 편미분으로 구할 수 있다.
3. 벡터 > 벡터 : 야코비안으로 구할 수 있다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/d4607ee6-8ecc-4801-8c81-71791283beeb)

## 오류 역전파는 미분의 연쇄 법칙을 활용

합성함수를 미분할 때 chain rule을 활용한다. 이런 체인룰을 활용해 오류 역전파를 할 수 있다.

- 수일 경우 : 스칼라일 경우 미분을 통해 나온 값을 가중치에 대한 그래디언트로 사용한다.
- 벡터일 경우 : 각 가중치 행렬은 행렬 미분을 통해 그래디언트 벡터를 계산한다.



목적함수는 오차이므로 스칼라 값이 출력되어야 한다. 예측값 y^은 w 가중치 값으로 결정된다.

즉 [ w > y^ > J(Θ) ]는 다음과 같은 함수 관계를 가진다.

이 때 w와 y^은 다대다의 관계, y^과 목적함수는 다대스칼라의 관계를 가진다.



## 2층 다층 퍼셉트론의 오류 역전파 알고리즘 예시

목적함수의 미분을 통해 방향을 알고 그를 통해 w를 다시 갱신한다.

이러한 구조는 [ 입력층 > 은닉층 > 출력 ] 에서 출력에서 다시 입력으로 갱신되는 역방향 전파, backward라 한다.

오차인 출력에서 시작해 다시 입력층인 w를 갱신한다. 



![image](https://github.com/hhzzzk/studyLog/assets/67236054/350835fd-cd9d-48f9-99c9-1a4988c817b7)



---

## 신경망의 오류 역전파 연쇄 법칙

![image](https://github.com/hhzzzk/studyLog/assets/67236054/abbe7561-5c42-4fe5-bb37-a6aa5006605b)



net

w와 J(Θ)는 함수관계이므로 미분 값을 구할 수 있다. 



## 단일 노드 연산 그래프의 오류 역전파

출력은 out = f(in) 이다.

>  in > f > out

은 forward이다.

backprop은

![image](https://github.com/hhzzzk/studyLog/assets/67236054/151fc02a-ea15-4f1a-8079-5bb76b3064b8)

---

![image](https://github.com/hhzzzk/studyLog/assets/67236054/98b1c04a-6f81-4872-929e-528e86e81d8e)

역전파로 계산할 때 출력이 입력으로 들어간다.

- 출력 그래디언트는 손실함수를 미분한다. 

다음 미분은 벡터대벡터이고 local gradient이다.

- 활성화 함수의 가중치를 기반으로 각 레이어의 노드에서 계산된다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/26d8d7ca-c90e-4b2a-9f34-711827feb0a5)

## 곱셈 연산의 역전파

input이 2개이다. 

![image](https://github.com/hhzzzk/studyLog/assets/67236054/c53548c7-8720-4901-8e9b-ce7e112129c5)



 순전파 단계에서 계산된 중간 값을 저장해두어야 하며, 역전파 단계에서 이러한 값들을 사용하여 그래디언트를 계산

ε는 손실 함수!!!

손실함수에 대한 편미분을 한 것이다.

## 주요 연산의 역전파 예시

매우 중요한듯..

![image](https://github.com/hhzzzk/studyLog/assets/67236054/b77cf7d1-6242-4b39-bebd-d491ddc37912)

## 곱셈 연산의 역전파 파이토치 구현

56페이지 코드...

관심 있는 input에 대해서 미분하기

## 덧셈 연산의 역전파

ㅋㅋ..이해하기..

결국 다 손실함수에 대해 미분하면 최종출력된 output에 대한 미분을 하고 

output을 입력 어떤 것에 대해 편미분한 2개의 곱으로 이뤄진다.

그게 output gradient = 최종출력을 미분

최종출력을 또 입력으로 편미분 = local gradient

연산 종류에 따라 로컬 그래디언트가 예측 가능하다.

## 시그모이드 함수 연산의 역전파

f(x)=1/(1+e−x1) 가 시그모이드 함수이다.

이를 미분하면 f' * (1-f)

## 최대화 max 함수 연산의 역전파 (ReLU)

![image](https://github.com/hhzzzk/studyLog/assets/67236054/aeb5d2cc-525b-440c-b450-6ed5e6eb170a)

max 함수의 역전파는 출력 그래디언트가 가장 큰 값을 갖는 입력 변수에 대해서만 전파되는 것으로 정의됩니다. 다른 변수에 대해서는 그래디언트가 전파되지 않습니다.





위에 61페이지 주요 연산의 역전파 예시르 이해해...꼭....



각 가중치와 입력 변수에 대한 그래디언트를 계산하여, 역전파를 통해 각 변수가 손실 함수에 대해 어떻게 변화해야 하는지를 알 수 있습니다. 이를 통해 경사하강법 등의 최적화 알고리즘을 사용하여 가중치와 편향을 업데이트할 수 있습니다.