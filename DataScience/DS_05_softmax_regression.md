# DS_05_softmax_regression

## 로지스틱 회귀

###🐤로지스틱 회귀의 예측값 도출 과정🐤

![image](https://github.com/hhzzzk/studyLog/assets/67236054/1b2d6459-6b4b-4d54-a2ef-7c320ae01890)



1. 입력벡터 x와 가중치 w를 내적. 결과 z = wTx
2. 내적한 결과 z를 활성함수(로지스틱 회귀는 시그모이드 함수)에 적용한다.
   - 시그모이드 함수는 입력을 0에서 1 사이의 확률로 변환한다.
3. 시그모이드 함수를 통해 얻은 출력은 입력 벡터 x가 어떤 클래스에 속하는 확률을 나타낸다. 이를 예측값으로 사용한다.

---

```
가설 함수(hypothesis function)는 입력 벡터에서 예측값을 출력하는 함수
	입력과 가중치의 관계를 모델링 = 함수로 표현
내적하고 활성함수에 적용한 것까지를 전부 포함함
가설 함수를 통해 얻는 값은 입력 벡터 x가 어떤 클래스에 속할 확률이다.
```

````
활성함수는 인공 신경망에서 뉴런의 출력을 결정하는 함수이다. 
신경망의 _비선형성_을 도입해 복잡한 함수를 모델링할 수 있게 한다. 
대표적으로 시그모이드, softmax함수 등이 있다.
````

```
비용함수는 모델의 예측과 실제 데이터 간의 차이를 측정하는 함수이다. == 손실함수
모델의 성능을 평가하고 모델 파라미터를 조정한다.
오차를 최소화해 모델 파라미터를 찾는 것이 목표이다.
대표적으로 MSE, BCE, CE 등이 있다.
```



### 🐤정리🐤

로지스틱 회귀는 y가 0,1인 이진 분류 문제에서 시그모이드 함수를 사용해 분류하는 모델이다.

선형,직선으로 분류 문제를 수행할 경우 오류가 발생할 수 있어 가설함수에 시그모이드 함수를 사용해 비선형성을 추가했다.

최종 출력을 확률로 봐서 0,1을 결정한다. 

비용함수로 MSE를 사용할 경우 cost가 1이상으로 올라가지 않아 평평한 부분이 생겨 경사하강법이 제대로 작동하지 않는 부분이 생긴다. 

따라서 새로운 비용함수를 필요로 하는데 -log(1-x)를 이용한 BCS(바이너리 크로스 앤트로피)를 사용한다. 

BCS에 경사하강법(편미분)해서 비용을 최소로 하는 w,b 적절한 가중치를 찾는다.



## 다중 분류 문제 Multinomial Classification

`종속 변수 y가 두 가지 이상의 값을 가지는 경우의 회귀 분석`

- 입력에 대한 출력이 K개의 클래스로 나옴
- 이진 분류에서는 0, 1로 나타냈는데 그 이상이면
  - [1,0,0] 이런 식으로 나타냄
  - 클래스가 K개면 K개의 이진분류를 수행한다! 각 열마다 이진분류 확인



- 각 이진분류에서 계산된 출력을 *확률로* 해석한다.
  - 정규화를 통해 합이 1이 되도록하고 가장 큰 확률이 1이 됨 >>> [1,0,0] A클래스겠군



### 🐤softmax🐤

다중 분류 문제도 로지스틱 회귀처럼 이진분류를 사용하는데 그걸 여러 번 사용한다고도 볼 수 있음 원리 유사

입력과 가중치를 내적하고 합한 것에 시그모이드 함수를 사용하고 정규화하는 과정을 통해 예측값을 구하는데

여기서 시그모이드 함수를 사용하고 정규화하는 과정을 합친 것이 softmax 함수이다.



![image](https://github.com/hhzzzk/studyLog/assets/67236054/f0b1dafc-0407-42f0-921f-45eab875c076)

![image](https://github.com/hhzzzk/studyLog/assets/67236054/20576712-d240-4a08-b700-edc9d7b4e5ad)

### 🐤다중분류문제의 비용함수 : Cross Entropy🐤

비용함수 : 현재의 가설이 얼마나 잘못되었는가

- 값이 작을수록 가설이 정확하고 값이 클수록 가설이 잘못됐다

![image](https://github.com/hhzzzk/studyLog/assets/67236054/de6bded9-17c5-4b76-a12a-f4c0bd7591bb)





## 정리

![image](https://github.com/hhzzzk/studyLog/assets/67236054/e07403e3-a8b2-4439-9309-f818bf1b15df)





![image](https://github.com/hhzzzk/studyLog/assets/67236054/ac60be79-75d2-4de6-ba73-64c2009174f0)
