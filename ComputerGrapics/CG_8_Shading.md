# CG_8_Shading

5/3 수요일

```
7 뒷부분

유니폼 변수는 read-only, 나중에 값 바꾸거나 덮어쓰기 불가능

쉐이더가 글로벌 변수 건들기 x
vertex가 attribute도 변경 불가능

필요하다면 경우에 따라 로컬 변수로 가져오기

vatying도 기본적으로 변경이 불가능, 화살표 관계 잘보기,7에 그림 23페이지

/

25페이지



```

shading >>> fragment 프로세서 / vertext 프로세서에서의 컬러 결정하기

/

오픈지엘에서 글로벌 이펙트 계산안함 ,그림자 다 가짜임



__Light-material interaction__

8페이지

빛 튕김, 난반사, 투명 3가지 케이스

 specular, diffuse, translucent



__color__

물체가 가진게 아님

컬러는 광원, 라이트 소스만 가짐



백색광원이 표면을 때렸을때 나오는 반응, 

빨간색물체는 빨간색을 튕김거임 백색광원에서 다른 컬러는 흡수한것



그래서 광원, 다른 빛을 쏘면 물체가 다른색을 보임

물체의 고유칼라는 없다.



보는 각도에 따라서도 컬러 바뀜, 

광원의 컬러, 지점의 재질, 광원의 입사각과 반사각 등 을 종합해서 컬러가 결정된다.



11페이지

bidirectional reflection

두 방향의, 

빛,방향과 뷰어 방향을 바꿔가면서 빛이 어떻게 반응하는지 알고싶다



광원의 위치와 카메라 위치를 바꿔가면서 분포를 측정하는 것

그렇게 게산된 빛이 물리적인 컬러 결정하기



일종의 함수, ㄹ광원 위치와 카메라 위치값이 고정되면 어떤 컬러가 어디 분포해있는지 나옴



__랜더링 이큐에이션__

빛의 전파,

카메라에서 어떤 컬러를 관찰하는가가 좌변, 주황색선

그 지점이 광원이었다면 x가, 그게 Le, x란 지점에서 오메가 방향으로 뿜어낸 집 더함 우변첫번째



인테그랄, 합, 오메가 지역 반구지역을 돌면서 for뤂 돌듯이

인테그랄 안이 for문 로직이라고 보면됨



오메가 프라임은 이렇게 저렇게도 들어오는 값들을 

..

x라는 지점에 w 프라이ㅁ방향으로 빛이 ㄷㄹ어왔는데

람다 t는..걍 무시



Li는 i 방향, 오메가 다시 방향으로 들어온 실제 빛



마지막 -w' 는...



음...









# 5/8

## Phong Reflection Model

```
ortho scale 어쩌구

```

```
리뷰
radiosity

```



각 컬러의 intensity, 값 구하기

ambient 은은한 빛은 걍 값으로 줌

diffuse라는 모델, 물체의 뽀샤시한 면을 지점마다 계산하는 모델, 무광? 난반사

specular, 빛이나는 빛이 하이라이트 되는 지점 계산, 유광?, 

3개를 모아서 렌더링하면 완성

물체가 빛 튕겨내고 그런건 없고 컬러 맞으면 끝

2차로 물체에서 빛 반사하는거 생략 > 로컬일루미네이션

/

ambient

기본적인밝기, 계산생략하고 걍 결정

ambient light 결정

빛에 ambient 요소 부여, 각 물체마다 엠비언트 라이트에 얼마나 반응할지

곱하면 ambient intensity 값 결정됨

물리적으로는 말이 안됨



/

diffuse

표면이 거칠어서 어느빛이 들어와도 모든방향으로 튕기면서 매끈?

모든 방향에 대해 동일한 밝기로 튕겨냄

__모든방향으로 동일하게 밝기 관찰됨__



빛을 얼마나 튕겨내나/흡수하나의 정도, intensity

파랑은..1..레드그린은..0..



mat_kd, rgb를 얼마나 튕겨낼것인가, 재질임, 10프로씩만 튕겨내겠다

light_ld, rgb가 다 1세기, 백색광

> 회색

/

max, 물체표면 벗어난 지역에서 온건 무시

max 사용 이유

/

specular

reflection과 view, 각도가 rv의 각도가 일치되면 1, 아니면 0에 가까운 값

뷰가 눈,

light에 대해서로 specular에 관련된 rgb값이 있음

그게 angle만큼의 세기로 관찰자에게 전달

Ks, 빛이 오면 흡수하는것과 튕겨내는게 있는데 rgb별로 그 세기

알파,  25페이지

승수를 곱하는 식으로 해서 더 빠르게 줄어들어서 반-짝하도록



/

26페이지

광원 하나에 ㄷ해ㅐ ambient, diffuse 등 여러개가 존재함

카파 ,얼마나 튕겨낼건가, 1이면 걍 튕김, 반사계수



재질마다도 reflection 3, 각 rgb마다 또 있음



26페이지 완





# 5/10

난반사, lambertain surface, 

빛이 들어오면 모든방향으로 동일세기로 반사,

각도에 따라 세기의 정도가 다름을 표현하기 위해   l 방향의 방향벡터와

n벡터, 사이의 cos세타, 

l과 n을 dot product해서 빛이 얼마나 강하게 들어오는지

```
Phong Reflection Model은 주변광(ambient), 난반사광(diffuse), 정반사광(specular) 세 가지 유형의 조명을 결합하여 표면과 빛의 상호작용을 시뮬레이션하는 로컬 조명 모델입니다. 이 모델은 표면의 색상을 계산하기 위해 여러 가지 빛의 정보, 현재 재질의 정보, 그리고 표면의 법선 벡터를 사용합니다.

Phong Reflection Model은 물체의 표면에서 발생하는 주변광을 모델링하여 물체 주변의 간접적인 조명을 표현합니다. 또한, 난반사광을 사용하여 표면이 빛을 서로 다른 방향으로 분산시키는 거친 표면의 느낌을 제공하며, 정반사광을 사용하여 표면에서 거울처럼 반사되는 광택이 있는 부분을 표현합니다.

Phong Reflection Model은 광원과 표면 사이의 거리에 따라 유효한 광의 강도가 약해지는 현상도 고려합니다. 이를 통해 물체의 입체감과 조명에 따른 그림자 효과를 재현할 수 있습니다.

또한, Phong-Blinn Reflection Model은 Phong Reflection Model의 변형으로, 특히 뷰어와 광원을 무한대로 가정할 때 정점 단위 계산을 없애고 계산 시간을 줄이는 데 중점을 둔 모델입니다.
```

### Ambient Reflection (주변광)

18페이지

```
Phong Reflection Model에서 주변광(ambient light)은 표면에 존재하는 모든 빛에 대한 일정한 양의 광을 나타냅니다. 이는 표면에 동일하게 분산되어 반사되는 빛으로, 주변 환경의 간접 조명을 모델링합니다.

주변광 계산은 다음과 같은 공식을 사용합니다:

Ia = ka * La

여기서,

Ia는 주변광의 색상과 강도를 나타내는 값입니다.
ka는 표면의 주변광 반사 계수(ambient reflection coefficient)로, 표면의 색과 강도를 조절합니다.
La는 주변광의 색상과 강도를 나타내는 값으로, 주변 조명의 색과 강도를 나타냅니다.

이 공식은 주변광을 계산하기 위해 주변광 반사 계수와 주변 조명의 색과 강도를 곱하여 얻은 값으로, 표면의 주변광 반사 효과를 나타냅니다. 

주변광 반사 계수가 높을수록 표면이 주변광을 강하게 반사하고, 낮을수록 약하게 반사합니다. 
주변광의 색과 강도는 주변 조명의 색과 강도를 나타내며, 이를 조절하여 주변광의 색상과 강도를 조정할 수 있습니다.

이러한 주변광 계산은 Phong Reflection Model의 일부로, 표면의 총 조명 효과에 기여합니다.
```



```
주변광을 "강하게" 반사한다는 것은 표면이 주변광에 대해 더 많은 빛을 반사하도록 하는 것을 의미합니다. 주변광 반사 계수(ka)를 높이는 것으로 이를 조절할 수 있습니다.

주변광은 표면 주변에 있는 모든 방향에서 일정한 양의 빛을 반사하는 조명입니다. 이 빛은 주변 환경에서 표면에 동일하게 분산되어 반사됩니다. 주변광은 직접적인 광원으로부터 오는 빛이 아니기 때문에 표면의 입체감과 조명에 의한 그림자 효과를 주는 데 사용됩니다.

주변광 반사 계수(ka)는 표면의 재질 특성을 나타내며, 이 값을 높일수록 표면은 주변광에 민감하게 반응하여 강하게 반사합니다. 즉, 높은 주변광 반사 계수는 주변광을 강하게 반사하는 것을 의미합니다.

예를 들어, 만약 표면의 주변광 반사 계수가 매우 높다면, 표면은 주변광에 많은 빛을 반사하여 주변의 색과 밝기를 크게 영향을 받게 됩니다. 이는 표면이 주변 환경의 색상과 밝기를 잘 반영하고, 주변의 색조와 조명을 표면에 더 강하게 녹여내는 효과를 만들어냅니다.

따라서, 주변광을 강하게 반사하는 것은 표면이 주변 환경의 조명을 강하게 수용하고 반영하여 주변의 색과 밝기를 더 강하게 표현하는 것을 의미합니다. 이는 시각적으로 더 현실적이고 입체감 있는 표면을 구현하는 데 도움을 줍니다.
```



### Diffuse Reflection (난반사광)

```

```



/

##  Computing Per-vertex Normals



41페이지

flat shading

smooth shading



플래슨 삼각형, 각 vertex의 normal을 줄때 폴리곤의 노말을 줌

세 정점이 폴리곤의 노말과 동일한 노말을 가짐



vertex의 정보는 폴리곤의 개수만큼 존재,

- 같은 버텍스라도 해당 폴리곤의 노말

스무스는

폴리곤 노말들을 계산하고 vertex의 노말을 주변 폴리곤 노말들의 average로 설정

- 같은 버텍스는 같은...



42페이지

같은코드라도 어디서 쉐이더에서 게산하는지에 따라 차이남



43페이지

이전과 다르게 폴리곤마다 노말 주는 flat으로 줘도,,

머해서 예쁘게 나옴 위랑은 다르게



