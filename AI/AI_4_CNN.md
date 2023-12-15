# AI_4_CNN

```
1. 깊은 신경망 DNN
2. 합성곱 신경망 CNN
3. 대표적인 합성곱 신경망
4. 심층 학습 특징
```

숙제열심히하기..미리미리하기..

## 오류 역전파 re

## 신경망의 오류 역전파 연쇄 법칙

![image](https://github.com/hhzzzk/studyLog/assets/67236054/eab848d9-c2c1-43cd-92c5-26ca9e31c5f6)

1번이 output gradient > oj를 변경할 때 E가 변하는 정도

2번이 local gradient > netj를 변경할 때 oj가 변하는 정도

## 단일 노드 연산 그래프의 오류 역전파

![image](https://github.com/hhzzzk/studyLog/assets/67236054/31052286-885d-470e-9239-26f79f270181)



∂ε/∂in = ∂ε/∂out * ∂out/∂in

ε는 손실함수, 오차를 나타낸다.

입력 input에 따른 오차의 변화량 = ouput에 따른 오차량에 local gradient를 곱한다.

## 전개 fanout 혹은 분배 연산의 역전파

+...

63p 신경망의 역전파 시험 나온거

결국 gradient vanishing해서 0이였나 그럼..

교수님 이런 딱떨어지는 심플한 문제 취향

---

## 1. 깊은 신경망 DNNs

- 다층 퍼셉트론에 은닉층을 여러 개 추가하면 깊은 신경망이 된다.
- 80년대에 DNN이 제안되었으나 경사 소멸 gradient vanishing 문제로 인해 학습이 안되는 문제
  - sol ) ReLU로 활성함수를 변경, 교차 엔트로피 등



> 퍼셉트론일 때 활성함수로 계단함수, 목적함수로 MSE
>
> 다층 퍼셉트론에서 활성함수로 시그모이드 함수, 목적함수 MSE
>
> 깊은 다층 퍼셉트론에서 활성함수로 ReLU나 그런 종류, 목적함수로 교차 엔트로피나 로그우도로 발전함



## 기계학습의 패러다임 변화

- 과거에는 수작업으로 특싱을 선택하거나 추출하는 과정 있었다.
- data-driven features : DNN은 데이터로부터 자동화된 특징 추출하도록 학습한다. 



## 깊은 신경망의 특징 (표현) 학습

**Fine-tuning** : 이미 훈련된 모델을 새로운 데이터셋에 맞게 미세조정하는 과정

- 미리 학습된 모델을 사용해 비용과 시간을 절약

**Transfer Learning** : 한 작업에서 학습한 지식을 다른 유사한 작업에 적용하는 머신러닝 기술

- 한 작업에서 학습된 모델을 다른 작업에서 재사용해 성능 향상

---

![image](https://github.com/hhzzzk/studyLog/assets/67236054/3db87176-7e37-4f7d-a2cc-8616c91c7d52)



초기 레이어는 저급특징(점,선,면 등)을 추출

후반 레이어는 분류작업을 수행한다.

- 후반 은닉층 레이어로 갈수록 고급특징, 복잡한 특징을 추출한다. 즉 이전의 정보를 기반으로 점점 더 발전되고 복잡한 특징들(추상적인 형태의)을 가져올 수 있게 된다.
- 점진적 계층화, 모델이 입력의 복잡한 특징을 점진적으로 이해한다.
- 레이어 단위의 역할 배분, 분할 = 각 레이어는 입력 데이터의 다른 측면을 표현한다.



## DMLP, 깊은 다층 퍼셉트론

퍼셉트론의 각 층에서는 선형과 비선형 연산이 수행된다.



![HD wallpaper_ Studio Ghibli, nature, landscape, The Wind Rises, colorful](https://github.com/hhzzzk/studyLog/assets/67236054/e71ab676-fde0-4a5b-b937-157f67164c9b)



## 2. CNN 합성곱 신경망의 구조

CNN의 가장 큰 특징은 신경망의 선형 연산을 합성곱, convolutional로 바꾸겠다는 것이다.



## CNN 등장 배경

컴퓨터 비전에서 사진 분류 등은 동일한 객체라도 카메라의 각도에 따라 모든 픽셀값이 변화되거나 배경과 구분이 어려운 경우 등 한계가 존재했다. SIFT 등의 방법으로 해결하려 했으나 복잡한 이미지나 고차원 데이터 처리에서의 한계점 등으로 CNN이 등장한다.



## 합성곱 신경망

**구조** : 은닉층은 높이, 폭, 깊이의 3차원으로 처리한다. height, width, depth

**구성 요소** : 합성곱 층(CONV + RELU)과 통합층 (POOL), 완전 연결층 (fully connected 레이어, FC)

✅ **합성곱층**

- 컨볼루션, 합성곱 연산과 활성화 함수를 조합해 입력 데이터에서 지역적인 패턴을 인식한다.
  - *컨볼루션 연산으로 이전의 선형 연산을 대체*한다!!! 활성함수인 ReLU가 비선형 연산
- 사진의 특성인 지역성 locality와 정상성 stationarity를 활용해 이미지의 지역적인 패턴을 효과적으로 인식한다.
  - 정상성은 사진의 특성상 반복되는 부분이 나오는 특성이다.

✅ **풀링층**

- 합성곱층의 출력을 간소화하고 중요 정보를 유지한다. 공간적인 크기를 줄이며 중요 정보는 유지

✅ **완전연결층**

- 이전 층의 특징을 바탕으로 최종 출력을 생성, 입력 데이터의 모든 특성을 고려해 최종 예측을 수행한다.



## 신경망 연결성 비교

DMLP의 선형 연산과 CONV의 차이!

완전 연결 VS 부분 연결

![image](https://github.com/hhzzzk/studyLog/assets/67236054/fead24b9-2823-481b-850e-612949d3d503)

- 완전연결 구조는 높은 복잡도를 가진다. 서로 다 연결되어 있다. 학습이 매우 느리고 과잉적합 우려가 있다.
- 합성곱 연결층은 컨볼루션 연산을 이용한 부분연결로 복잡도를 크게 낮춘다.
  - 전체 가중치가 아닌 부분 가중치로만 연산, 즉 부분내적을 하고 이를 shift, 한 칸씩 이동하며 반복 수행한다. (사진의 지역성, 정상성)
  - 3개씩 마스크(윈도우) 씌워서 연산해 출력 1개를 낸다.



## 합성곱의 가중치 공유 weight sharing / parameter sharing

![image](https://github.com/hhzzzk/studyLog/assets/67236054/2eeb0ea6-3cab-41bf-9d08-ce7437f9d532)

사진의 정상성으로 인해 가중치가 반복된다.

그림에서 0.4, 0.3, 0.3이 반복된다. stride

부분내적을 수행하고 stride수행 = 걸음을 이동한다.



해당예제에서 필터당 필요가중치는 3개이다. 완전 연결이었다면 64개

3개만 사용해 모델의 복잡도가 크게 낮아진다.

사진의 특성 덕분에 이런게 가능하다. 여러 개의 필터를 사용한다.



## 합성곱 연산

컨볼루션 연산에는 교차 연관성과 컨볼루션 연산 2가지가 있는데

교차 연관성은 cross - correlation으로 컴비에서 배운 상관이다. 필터를 바로 적용한다.

- 상관은 두 영상의 연관관계를 나타낼 때 주로 사용한다. 패턴 매칭, 템플릿 매칭에서 사용한다.

컨볼루션은 필터를 뒤집어서 적용한다.

수업에서는 컨볼루션으로 통칭한다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/524c2150-6cbf-4f8b-8181-d476b82e0096)



요소와 요소를 곱한 것을 합친게 합성곱 연산이다. 

![image](https://github.com/hhzzzk/studyLog/assets/67236054/34d76a9f-1d4d-41b7-9d42-24b0e8ac1460)

위의 수평 소벨 필터를 씌운 것이다. 이러한 필터 적용을 통해 특징이 두드러지게 된다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/c20d8cf8-80ee-4835-81b2-bd2526d5dea8)

✅ **feature map**

9개의 칸에 필터와 연산을 한 값들을 더하면 하나의 값이 나온다. 이를 반복해 9칸을 채운다.

---

⏩ 

신경망 레이어로 원하는 정보, 위에서의 특징점처럼 원하는 정보를 두드러지게 해서 추출한다.

신경망에서 가중치를 조정해 필터를 만든다.



## 인공 신경망의 합성곱 연산

커널 == 필터 (컴비에서의 윈도우)

출력은 특징맵, feature map

- 컨볼루션은 해당하는 요소끼리 곱하고 결과를 모두 더하는 선형 연산이다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/29638f59-58ab-4461-8bfb-ceeb60270b79)

1차원 예제를 보면 필터와 입력을 연산해 출력인 특징맵을 얻는다. 이 때 보통 사이즈가 줄어든다. (아래에서 해결)

![image](https://github.com/hhzzzk/studyLog/assets/67236054/596a2217-e7ce-48ae-9d53-785ca4e71bac)

![image](https://github.com/hhzzzk/studyLog/assets/67236054/935c1008-c946-4bc9-a326-4cabf0a00cc4)

> 컨볼루션 연산으로 부각되는 정보가 추상화된다.

## 3차원 합성곱 연산의 예

rgb 컬러 영상은 3차원 텐서를 겹친 것이다. 

✅**0 덧대기** : 입력 크기에서 테두리를 0으로 채운다. 위에서 사이즈가 출력의 사이즈가 줄어드는 것을 방지한다. 아래에서 더알려줌

![image](https://github.com/hhzzzk/studyLog/assets/67236054/ecb4b724-6c2e-4491-9a26-22088ba58c63)

RGB가 최종 특징맵으로 출력되어야 한다.

RGB 즉 3\*3\*3차원이 커널과 연산하면서 3*3의 값으로 출력된다. 

즉 depth를 같이 고려해야 한다. 3,3,3의 하나의 볼륨으로 접근해야 한다. 그렇게 생성된 특징맵을 3개르 하나로 봐서 다시 input으로 들어가고의 반복이다.



![image](https://github.com/hhzzzk/studyLog/assets/67236054/7248bfbd-4855-4b7a-9920-812d999c3d48)



## 합성곱 연산에 따른 합성곱 신경망의 특성

컨볼루션 연산은 어느정도 형상을 유지한다.

피처맵에는 형상 유지한다는 의미가 내포되어 있다.

- CNN은 이동 불변성, 입력의 이동을 특징맵에서 그대로 반영한다.

병렬 분산 구조 : 각 노드는 독립적 계산 가능하므로 병렬 구조 (GPU)



노드는 깊은 층을 거치며 전체에 영향을 미치므로 분산 구조 : 특징을 점진적으로 통합 > 추상화

- 3개의 가중치를 통해 1개의 특징맵을 추출한다. 즉 이때 특징맵은 부분 특징만 내포한다.
  - 위에서 추출된 특징맵이 다시 입력으로 들어가며 층이 거듭된다.
  - 이를 반복해 층이 거듭될수록 특징맵은 전체의 정보를 가지게 된다. 
    - 점진적 추상화, 파라미터 효율적으로 줄어든다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/d439fc04-9588-4fbf-9cb7-ff0132e5ff5c)



## 흑백 사진에서 합성곱 연산 예

수직필터, 수평필터를 인간이 경험적으로 찾았다. 

그러나 이제는 신경망이 필터를 오류 역전파하며 찾는다.

10개의 필터로 10개의 피처맵을 얻는다.

​	이를 depth 10개로 겹쳐서 다음 레이어에서 입력으로 들어간다.



## RGB 동영상

4차원 텐서이다. 사진이 시간순서로 묶인 연속된 사진

## 복수의 특징맵 추출

실제 필터는 여러 개를 사용한다. 다양한 필터를 사용해 다각도로 관찰해 강한?특징을 추출한다.

각 레이어마다 컨볼루션 연산이 수행된다.

3*3이면 필터 64개, 128개 가중치로 설정한다.



3개의 커널을 사용하면 3개의 특징맵이 추출된다.

서로 다른 관점들의 피처맵들을 추출해 겹쳐서 또 input으로 들어가고의 반복



## 하이퍼 파라미터

하이퍼 파라미터는 파라미터와 다르다.

하이퍼 파라미터는 은닉층의 개수나 합성곱 필터를 설정하는 등



## 패딩, 덧대기

패딩은 가장자리에서 영상의 크기가 줄어드는 효과를 방지한다 == 각층의 입출력 특징형상유지

즉 입력사이즈가 출력에서 그대로 유지되도록 한다.

0패딩은 값이 유지된다. 

- 편향 추가

bias term 추가

![image](https://github.com/hhzzzk/studyLog/assets/67236054/58ff3a63-a403-4844-910f-7ec16b670c63)



---

다른 방법으로 stride를 2로 해서 블럭단위로 기계적으로 특정층 이후부터 줄어들도록 한다 ?



## stride에 의한 다운샘플링(축소)

stride를 2로 하면 2개마다 하나씩 추출해서 필터를 적용한다.

2차원 영상의 경우 특징맵이 1/4로 작아진다. (보폭 k, 특징맵 1/k^2)



특징맵 줄이는 방법 2가지

1. stride
2. 풀링 레이어로 가로세로 줄이기

35페이지 시험나옴@@@@@@@ 아래 이미지 35p

![image](https://github.com/hhzzzk/studyLog/assets/67236054/53bd02ca-a581-45c2-bbc4-502c92a88598)

컴비랑 엄청 겹친당 같이 보기



## 활성함수

ReLU는 max(0,z)라 0보다 크면 output gradient가 그대로 나오는 bypass?



## 풀링(통합) 연산

통계적 대표값을 활용해 특징맵의 정보 요약(다운샘플링) 혹은 부각

- 다운사이징은 중요한 부분만 보겠다는 것으로 연산효율성이 올라간다.
- 단점은 학습 요소를 포함하지 않아 정보 손실이 가능하다.
  - !!! 최신에는 풀링층을 사용하지 않는다. 정보손실이 크기 때문이다.

그래서 사이즈를 줄일 때 stride를 사용하는 경우가 많다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/f4759fae-eeb7-45bb-bcce-d6c0e28bf2ac)

그림처럼 보폭을 조절하거나 max나 avg풀링을 사용해 다운샘플링 가능하다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/d35eb9d0-ae8a-4c82-97f5-46d991d77374)



## 합성곱 신경망 전체 구조

컨볼루션-풀링-완전연결층 연결하고 깊은 구조로 확장한다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/256c670f-fb8e-496e-b423-cf888e8d07dc)



# 대표적인 합성곱 신경망

## Lenet-5

르넷은 CNN의 초창기 버전으로

필기 숫자 인식기를 만들어 수표 인식 자동화시스템을 구현한 것이다.

**특징 추출** : CONV-POOL-CONV-POOL-CONV의 다섯층으로 특징을 추출한다.

- 28X28 명암, 흑백 영상을 120차원의 특징 벡터로 변환한다.

**분류** : 특징 추출을 하고 하나의 완전연결층으로 출력으로 가능한 클래스=여기서는 0-9까지의 숫자,를 예측한다.



르넷의 주요 기여 중 하나는 필터와 가중치 공유, 그리고 합성곱 연산을 사용해 이미지의 지역적인 패턴을 탐지하는 방법을 도입했다. 이후 후속 CNN 아키텍처의 기초가 되었다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/6e240c71-5109-43e6-b026-48965c8e639e)

## AlexNet

알렉스넷은 2012년 우승

- 총 8개의 층으로 구성, 5개의 합성곱 층, 완전연결 3개층
  - 합성곱 층과 완전 연결 층의 구조를 혼합해서 사용해 합성곱 연산의 효과를 증대, 복잡한 이미지 특징 추출에 성공
- 각 층마다 290400-186624-64896-43264-4096-4096-1000개의  매개변수
  - CONV - CONV - CONV - CONV - CONV - FC - FC - FC
  - 합성곱 층: 290,400개, 186,624개, 64,896개, 43,264개, 4,096개
  - 완전 연결 층: 4,096개, 4,096개, 1,000개
    - (합성곱층은 파라미터를 공유해 완전 연결층보다 혁신적으로 적은 수의 파라미터 사용한다.)
- 합성곱 층은 200만 개, 완전 연결층은 6500만개의 매개변수 > 완전연결층에 30배 더 많으 매개변수가 존재
  - 이후 CNN의 구조는 완전연결층의 매개변수를 줄이는 방향으로 발전했다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/e5cff2d6-4f66-4277-a03a-aff439651a14)



1000개의 분류를 위해 소프트 맥스 함수를 사용한다.

- 처음 5개의 층은 특징 추출을 담당하며, 공간적인 특징을 감지하고 추출합니다.
- 그 이후의 3개의 완전 연결 층은 이러한 특징을 사용하여 이미지 분류를 수행합니다.



## AlexNet 학습  성공의  외적  요인

1. 대규모 사진 데이터인 ImageNet 훈련을 사용
2. GPU 활용한 병렬처리
   - AlexNet은 여러 개의 GPU에 모델을 분할하고, 병렬 처리를 통해 훈련을 진행했습니다. 이러한 GPU 분산 학습은 효율적인 학습 가능하게 함

![image](https://github.com/hhzzzk/studyLog/assets/67236054/e1597550-9080-4a9b-b21a-4dddd0327a1e)

3. ReLU 활성함수 사용 > 그래디언트 소실 문제 완화
4. 지역  반응  정규화local response normalization 기법  적용 LRN
   - 인접한 뉴런의 활성을 정규화해 경쟁적인 활성화를 유발, 인간 신경망의 억제 현상을 모방
     - 주변의 뉴런 활성이 활성화된 뉴런을 억제하는 현상인 억제, 이는 주변 패턴과 더 두드러진 패턴 구분에 도움, 더 높은 레벨의 특징 추출
   - ReLU 적용하는데 렐루는 정규화 기능 수행 안함. 오버피팅 방지 위해 렐루 이전에 LRN을 적용!!!!!!
   - 컨볼루션과 최대 풀링 레이어 이전에 LRN 적용!!! 이러면 레이어에서 특징 추출 후 해당 레이어의 활성화에 대한 정규화를 수행
5. 과잉적합  방지하는  여러  규제  기법  적용
   - 데이터 확대 = data augmentation, 잘라내기와 반전으로 2048배로 확대
   - 드롭아웃 > 완전 연결 층에서 사용
6. 추론inference 단계에서  앙상블  적용
   - 테스트나 추론 단계에서 입력된 영상을 데이터 확대 수행, 이 증대된 영상들의 예측을 평균해 최종 이식을 수행하는 앙상블을 적용 > 오류 감소



- LRN: 1번째, 2번째, 5번째 합성곱 층 (CONV)
- 드롭아웃: 6번째, 7번째, 8번째 완전 연결 층 (FC)
- 앙상블: 추론(inference) 단계에서 전체 모델에 적용





## VGGNet

1. 3*3의 작은 필터를 사용한다.
   - 작은 필터를 연속적으로 적용하면 더 복잡한 패턴을 학습할 수 있으며, 여러 개의 작은 필터를 적용한 결과는 하나의 큰 필터를 사용한 것보다 효과적
2. 알렉스넷에 비해 2,3배 더 깊어짐



## VGGNet : 작은 필터의 이점

이후 깊은 cnn 구조에 영향

큰 크기의 필터는 여러 개의 작은 크기 필터로 분해 가능 = 매개변수 수는 감소, 신경망은 깊어진다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/2d35d0df-ff9a-481a-a37c-d81428b9e32f)



## 1x1 컨볼루션 필터

- vgg넷에서 가능성을 실험했지만 최종 적용은 안함. 적용된 것 구글넷에서 사용됨
- 차원 통합, 차원 축소 효과
  - 특징 맵의 차원을 통합해 특징 맵의 깊이, 채널 수를 줄인다.
  - 입력 특징 맵의 각 위치에서 채널 간의 선형 결합을 수행, 차원 축소 효과
- 특징 맵 크기 축소!! 

>  1x1 합성곱은 입력 특징 맵의 채널 수를 줄이는 역할

## 참고 NIN 구조

기존 합성곱 연산을 MLPConv 연산으로 대체한다.

- 신경망의 미소 신경망, micro neural network가 주어진 수용장(receptive field)의 특징을 추상화 시도
  - 미소신경망으로 더 복잡한 특징 학습



전역 평균 요약 global average pooling 사용

- 부류 수만큼 대응되는 특징맵을 생성하고 특징맵의 평균값을 출력 노드와 연결
  - 완전연결 층의 과도한 매개변수를 줄인다!!



## GoogleNet

인셉션 모듈

- 다양한 특징을 추출하기 위해 NIN의 구조에 기반해 여러 수용장 크기를 병렬적으로 적용한 층
  - 다양한 수용장 크기는 다양한 크기와 형태의 특징을 동시에 추출하여 네트워크의 표현 능력을 향상
  - 인셉션 모듈은 한 층 내에서 복수의 합성곱 연산을 병렬로 수행하고, 이 결과를 결합하여 최종 특징
- 미소 신경망 대신 4가지의 합성곱 연산 사용
- 1x1 합성곱을 사용해 차원 축소!!!!
  - 매개변수 수=특징맵의 수를 줄이고 신경망이 깊어진다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/a9fc678d-5a3f-40d6-999a-dd835714e976)



## 구글넷 전체 구조

- 인셉션 모듈을 9개 결합
- 매개변수가 있는 층 22개, 없는 층 5개로 총 27개의 층
- 완전 연결층은 1개뿐!!!! = 백만개의 매개변수만 가진다! vgg에 비교하면 1퍼센트



- 보조 분류기 auxillary classifier
  - 원 분류기의 오류 역전파 결과와 보조 분류기의 오류 역전파 결과를 결합해 경사 소멸 문제를 완화한다.
  - 훈련할 때 도우미 역할을 하고 추론할 때 제거된다.



## ResNet

진도 56페이지 (11.13월 11w1) 11w2에는 선배 강연함



레저넷?은 Residual Networks로 매우 깊은 신경망을 효과적으로 훈련하기 위해 

*잔차학습*(residual learning)의 개념을 도입했다.

![image](https://github.com/hhzzzk/studyLog/assets/67236054/0db83a80-f7ba-406d-8cf0-86455457a054)

레이어 20개와 56개를 비교했을 때 레이어 늘릴 수록 성능이 높아진다고 기대했는데 실제는 그렇지 않다. (성능은 오류의 수와 반비례한다. 성능이 좋을수록 오류가 적어야 한다. 그래프의 추이가 아니라 절대값으로 비교 해야 한다.)



problem? 전통적인 cnn은 레이어 수가 증가함에 따라 성능이 향상되는 대신 악화된다.

- why? 기울시 소실 문제 때문에 레이어 수가 깊어질수록 훈련이 단조 증가하는 것이 아니라 어느 순간 악화된다.

잔차 학습 : 가장 중요한 개념은 bypass이다.

- 기울기 소실 문제를 극복하기 위해 두 개의 경로를 만들어 한 가지 길은 이전의 값이 그대로 통과, bypass 한다. 이렇게 해서 최소한 이전보다 악화되는 않는. 레이어가 "F(x) + x"의 출력을 내도록 한다.

레저넷의 기본 구성 요소는 잔차 블록(residual block)이다. 

- 두 가지 경로로 이루어진다. identity 경로 x와 잔여경로 Fx
- identity 경로는 입력 x를 다음 레이어로 그대로 전달한다.
- 잔여 경로는 잔여 Fx를 계산한다.
- 블록의 출력은 두 경로의 합이다.