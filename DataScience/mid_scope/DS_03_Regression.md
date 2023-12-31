# DS_03_Regression

## 지도학습

`훈련 데이터로부터 하나의 함수를 유추해내기 위한 기계학습의 한 방법`

- 기계학습의 한 유형으로 *입력과 출력 사이의 관계를 모델링, 함수화*한다. 이를 통해 새로운 입력이 들어올 때의 출력을 예측할 수 있다.
- 분류, 회귀, 강화학습, 시계열 예측, 자연어 처리, 객체 탐지 등이 있다.

## 회귀분석(Regression)

지도학습의 한 종류

> 관찰된 *연속형 변수들*에 대해 두 변수 사이의 모형을 구한 뒤 *적합도(관련있는정도?)를 측정*해내는 분석방법
>
> **선형회귀분석** : *종속 변수 y와 한 개 이상의 독립변수 x와의 선형 상관 관계를 모델링*하는 회귀분석 기법



## Linear Regression

선형 회귀는 변수 사이의 관계를 만족하는 직선 y=ax+c 함수를 찾아 새로운 입력의 출력을 예측할 수 있다.

a,c를 찾아야 한다.



## 가설과 비용 Hypothesis and Cost function

**가설함수 H(x) = wx + b**

- 가설함수는 입력을 받아 모델의 예측값을 출력한다.

**손실함수 cost(w,b)** 

- 모델의 예측과 실제 값 사이의 차이/오차를 측정
- MSE : 평균제곱오차, MSE = (1/n) * Σ(yᵢ - ŷᵢ)²
  - 실제값과 예측값의 제곱의 평균. (y-y^)



## 경사 하강법 Gradient Descent

- cost를 최소로 하자. cost를 최소로 만드는 w,b 찾기
- 함수의 기울기, 경사를 이용해 함수의 최솟값을 찾는 최적화 알고리즘
  - 함수의 기울기는 함수를 미분/편미분을 해서 기울기 벡터를 계산한다.
    - 기울기 벡터는 함수가 어느 방향으로 가장 가파르게 증가하는지 나타낸다.

```
가중치 업데이트:
W := W - learning_rate * ∂(손실 함수) / ∂(W)

편향 업데이트:
b := b - learning_rate * ∂(손실 함수) / ∂(b)

여기서,

W: 가중치(Weight) 벡터
b: 편향(Bias)
learning_rate: 학습률(learning rate), 가중치 및 편향 업데이트의 크기를 제어하는 하이퍼파라미터입니다.
∂(손실 함수) / ∂(W) 및 ∂(손실 함수) / ∂(b)는 손실 함수에 대한 가중치와 편향의 편미분입니다. 이를 통해 손실 함수의 기울기(경사)를 계산합니다.
```



