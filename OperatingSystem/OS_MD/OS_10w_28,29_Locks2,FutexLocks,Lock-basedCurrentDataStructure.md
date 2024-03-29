[TOC]



# OS_10w_28,29_Locks2,FutexLocks,Lock-basedCurrentDataStructure

뀨..포기놉

# OS_28 Locks-Yield(1)

https://www.youtube.com/watch?v=PYccLY3DkRc&list=PLGgVuvaPty_3qfOOl_UXQ3XSm02fCwLeK

스핀이 너무 많다! 문제

28.12 -  389페이지

교재정리

```markdown
# 28.12 과도한 스핀
스핀을 줄여보자
# 28.13 조건 없는 양보
락이 해제되기 기다리면서 스핀하지 말고 cpu를 다른 쓰레드에게 양보, yield하자
yield하면 쓰레드는 running에서 ready 상태로 변환됨
다른 쓰레드가 running 됨
결과적으로 양보는 스케줄 대상에서 자신을 deschedule, 빼는 것

정리
단일 CPU 시스템에서 두 개의 쓰레드를 실행하는 예에서 양보를 기반으로 한 기법은 잘 동작한다.
이 방법의 단점은 문맥교환이 많아질수록 엄청난 낭비가 생긴다는 것이다.
더 안 좋은 것은 굶주림 문제는 전혀 손도 대지 못한 상황이라는 것이다. 나머지 
쓰레드들은 임계 영역에 반복적인 출입을 하고 있는데, 어떤 쓰레드는 무한히 양보만 
하고 있는 경우가 있을 수 있다. 이 문제를 직접적으로 다루는 해법이 필요

# 28.14 큐의 사용 : 스핀 대신 잠자기
이전 방법들은 운빨이 심했다. 스케줄러가 다음 실행될 쓰레드를 잘못 선택하면
선택된 쓰레드는 락을 대기하면서 스핀하거나, cpu를 즉시 반납, 양보하거나 해야 함.

다수의 쓰레드가 락을 대기중인 경우
다음으로 락을 획득할 쓰레드를 명시적으로 선택 가능해야 함
이를 위해 큐를 이용한 대기 쓰레드들의 관리 필요

    park()는 호출하는 쓰레드를 잠재우는 함수
    unpark(쓰레드ID)는 쓰레드ID에 해당하는 특정 쓰레드를 깨우는 함수

    이 두 함수는 이미 사용중인 락을 요청하는 프로세스를 재우고
    해당 락이 해제되면 깨우도록 하는 락을 제작할 때 앞뒤로 사용 가능

1. 테스트 앤 셋 개념과 락 대기자 전용 큐를 사용한 락 만들기
2. 큐를 사용해 다음으로 락을 획득할 대상을 제어해 기아 현상 피하기

# 그림 28.9 guard 변수를 이용한 스핀락
큐와 flag 변수를 보호중임. 스핀 대기를 사용하지만 오버헤드는 적은 편이다.
쓰레드는 가드 변수를 획득하거나 해제하는 과정에서 인터럽트 가능
다른 쓰레드들은 락의 해제를 대기하며 스핀
__락과 언락 코드 내의 몇 개의 명령어만 수행하면 풀린다__ 스핀 대기 시간이 짧은 편
또 lock()에서 쓰레드가 락을 획득할 수 없을때
gettid() 함수를 호출해 자신의 쓰레드 ID를 얻기
큐에 자신을 추가함
가드를 0으로 설정
CPU 양보
??모르겟다


# 28.15 다른 운영체제, 다른 지원
리눅스의 경우 futex 지원함
futex는 특정 물리 메모리 주소 그리고 커널에 정의된 큐를 가짐
호출자는 futex 관련 함수를 호출해 잠을 자거나 잠에서 깨어남

futex_wait (address, expected)는 address의 값과 expected의 값이 동일하면 쓰레드 블락시킴
다르면 리턴
futex_wake (address)는 큐에서 대기하고 있던 쓰레드 하나를 깨움

(((이 코드에서는 하나의 정수를 이용하여 락의 
사용 중 여부와(최상위 비트를 사용하여), 대기자 수를 동시에 표현한다(나머지 비트를 
사용하여). 따라서 락이 음수라면 락이 사용 중(최상위 비트는 정수의 부호를 나타내기 
때문) 인 것을 나타낸다.

둘째, 이 코드는 경쟁이 없는 경우에 대해 최적화 되어있다. 하나의 쓰레드가 락 획득과 
해제를 반복할 경우, 특별히 빠르게 동작한다 (원자적으로 비트 단위의 test-and-set 
로 락을 획득하고 원자적 덧셈을 하여 락을 해제한다).)))

```



A만 일하고 b,c,d 다 스핀

![image](https://user-images.githubusercontent.com/67236054/236804135-721a998d-90a7-4c28-a1a2-45fa33107a68.png)

스핀 대신에 yield, while 루프 대신에 일드함

일드 yield하면 running에서 레디상태됨

일드 안쓰면 타임아웃될때까지 spin함



일드 쓰면 조금 running하다 레디상태됨

context switching 하는 시간은 소모되나 spin하는 시간은 줄일 수 있음



  

![image](https://user-images.githubusercontent.com/67236054/236804741-26682030-47d8-4549-8319-bb172f78de63.png)

## Locks-Yield(2) (2/5)

spin 했던 부분들을 다 yield로 바꿀 수 있음

티켓 락이나 테스트 앤셋 등

## Locks-Priority Inversion(3/5)

스핀락이면 안되는 이유들 394페이지



 priority inversion, 역전 현상

preemption해서 우선순위 따짐



해결, priority inheritance, 우선순위를 빌려줌, 나중에 반납

우선순위를 최대 자기 수준까지 빌려주기 가능

```markdown
교재 394페이지
# 스핀 락을 배제해야 하는 중요한 이유 : 우선순위 역전  priority inversion
한 시스템에 두 개의 쓰레드 존재, 쓰레드2는 높은 스케줄링 우선순위 가짐
두 쓰레드가 모두 실행가능하면 스케줄러는 2를 먼저 실행함
1은 2를 실행할 수 없을 때만 실행됨(2가 io 기다리며 blocked 된 경우)

문제
만약 2가 블락되면 1이 실행되어 스핀 락을 획득. 임계 영역 진입
2의 블락이 해제되면
스케줄러는 즉시 2를 스케줄링함
2는 락을 획득하려고 시도, 그러나 1이 락을 가지고 있기 때문에 스핀
2는 영원히 스핀, 시스템 정지됨

우선순위 역전 문제는 여러 가지 방법으로 해결할 수 있다. 스핀 락 때문에 생긴 
문제인 경우 스핀 락을 사용하지 않으면 된다（자세한 내용은 아래에서 설명함）. 

보다 일반적으로 우선순위가 낮은 쓰레드를 기다리는 높은 우선순위 쓰레드는 
낮은 쓰레드의 우선순위를 일시적으로 높여 먼저 실행되게 함으로써 역전 문제를 해결할 수 있다.
이러한 기 법은 우선순위 상속（priority inheritance）이라고 알려져 있다. 
마지막 해결책은 가장 간단하다. 
모든 쓰레드가 동일한 우선순위를 갖도록 만드는 것이다.
```



## Locks-with Sleeping (4/5)

queue 필요, 기다릴 장소 필요 sleep하려면, waiting queue

go to sleep > waiting 큐에 넣음

wake up > 레디큐에 넣음

가드는 큰 락이고 큰 락의 작은 락이 guard임

두 개의 쓰레드가 락을 공유함



```markdown
다수의 쓰레드가 락을 대기중인 경우
다음으로 락을 획득할 쓰레드를 명시적으로 선택 가능해야 함
이를 위해 큐를 이용한 대기 쓰레드들의 관리 필요

    park()는 호출하는 쓰레드를 잠재우는 함수, __큐에추가!__, blocked시킴
    unpark(쓰레드ID)는 쓰레드ID에 해당하는 특정 쓰레드를 깨우는 함수, wake up, 큐에 있는 걸 레디상태로 보냄

    이 두 함수는 이미 사용중인 락을 요청하는 프로세스를 재우고
    해당 락이 해제되면 깨우도록 하는 락을 제작할 때 앞뒤로 사용 가능

```

![image](https://github.com/hhzzzk/capstone-2023-20/assets/67236054/8bfa0ed2-e63d-4f73-bbcb-e50101c7f39c)



케이스 설명해주는데 졸라 머지

락과 락이 경쟁

언락과 락이 경쟁

언락과 락이 경쟁

락과 언락이 경쟁 > 여기서 문제 생김

경쟁조건이 남아있다,



setPark()의 존재



## Locks-Two Phase Locks (5/5)

멀티프로세서, cpu가 1개보다 많은 경우에는

임계영역의 길이에 따라 spin이나 sleep이나 더 유리한 경우가 존재함

길이가 길면 sleep이 유리하고

길이가 짧으면 spin이 더 유리함

​	__단일 프로세서 상에서는 sleep이 무조건 유리함__



28.16

2단계 락

일단 c만큼 스핀하다가 그래도 안되면 sleep함

![image](https://github.com/hhzzzk/capstone-2023-20/assets/67236054/aa336f75-878b-452b-be41-09daaa1d2976)



---

# OS, 28 Locks: Futex Locks 

강의머라는거야아나개빡치네ㅣㄴ짜운체만듣는줄아시나봐요교수님저희는운체만듣는게아니잖아요..

![image](https://github.com/hhzzzk/capstone-2023-20/assets/67236054/b5b6947d-8737-4a7a-b5a5-b2bb9f4c176b)

```markdown
 위에서 futex_wait 옆에 // *mutex == v면 goto sleep
 
# mutex_lock: 뮤텍스를 획득하는 함수입니다.
atomic_bit_test_set(mutex, 31): 뮤텍스의 31번째 비트를 확인하고 설정합니다. 비트가 0이면 이미 뮤텍스를 획득한 상태이므로 바로 리턴합니다.
atomic_increment(mutex): 뮤텍스 값을 1 증가시킵니다. 이를 통해 뮤텍스를 획득한 쓰레드의 개수를 추적합니다.
while (1): 무한 루프를 시작합니다.
atomic_bit_test_set(mutex, 31): 다시 한 번 뮤텍스의 31번째 비트를 확인하고 설정합니다. 비트가 0이면 다른 쓰레드가 뮤텍스를 획득한 상태이므로 획득을 시도하는 쓰레드는 대기합니다.
v = *mutex;: 뮤텍스 값을 읽어옵니다.
if (v >= 0) continue;: 읽어온 값이 0 이상인 경우 다른 쓰레드가 뮤텍스를 해제한 것이므로 다시 시도합니다.
futex_wait(mutex, v);: 뮤텍스 값이 음수인 경우, 쓰레드를 대기 상태로 전환하고 futex_wait 함수를 호출하여 뮤텍스 값이 변경될 때까지 대기합니다.


# mutex_unlock: 뮤텍스를 해제하는 함수입니다.
atomic_add_zero(mutex, 0x80000000): 뮤텍스에 0x80000000 값을 더한 후 결과가 0인지 확인합니다. 이를 통해 다른 쓰레드가 대기 중인지를 확인합니다. 대기 중인 쓰레드가 없다면 바로 리턴하여 뮤텍스를 해제합니다.

/
32비트를 사용하는 경우, 정수 값의 최상위 비트가 1인 경우 해당 값을 음수로 간주합니다. 이는 2의 보수 표현 방식을 사용하기 때문입니다. 따라서 최상위 비트가 1이 경우면 음수임

위의 코드에서 futex_wait(mutex, v); 부분은 뮤텍스 값이 음수인 경우에 실행되는 부분입니다. 이는 다른 스레드가 이미 뮤텍스를 획득한 상태이므로, 현재 스레드는 뮤텍스를 획득하기 위해 대기해야 함을 나타냅니다.

따라서, 뮤텍스 값이 음수라는 것은 다른 스레드가 이미 뮤텍스를 획득한 상태이고, 현재 스레드가 뮤텍스를 획득하기 위해 대기해야 한다는 의미
```



```
go to sleep하면 대기 큐에 넣는 것고
wake up하면 대기큐에 있는걸 지우고 레디큐에 넣는것
```



## 28 Locks - Futex Locks

삼성노트참고



# OS, 29 Lock-based Concurrent Data Structure

402페이지

```markdown
락 기반의 병행 자료구조
자료 구조에 락을 추가하면 해당 자료구조를 경쟁조건으로부터 안전한, thread safe한 자료구조로 만들기 가능


# 29.1 병행 카운터
가장 간단한 자료구조, 보편적으로 사용, 인터페이스 간단
## __간단하지만 확장성이 없음__
병행 가능한 카운터는 간단하지만 정확하게 동작

자료 구조를 조작하는 루틴을 호출할 때 락을 추가,
그 호출문이 리턴될 때 락이 해제
    이 방식은 모니터를 사용해 만든 자료구조와 유사
    모니터 기법은 객체에 대한 메소드를 호출하고 리턴할 때 자동적으로 락을 획득하고 해제함

제대로 동작하지만 성능이 문제
쓰레드 개수가 늘어날수록 성능 나빠짐

__perfect scaling__
작업양이 cpu의 개수에 비례해 증가하더라도 각 작업이 병렬적으로 처리되어
전체 완료 시간이 늘어나지 않는 것

## __확장성 있는 카운팅__ > 근사 카운터
근사 카운터, approximate counter
cpu 코어마다 존재하는 하나의 물리적인 지역 카운터와 하나의 전역 카운터로 구성
(cpu 코어 - 1지역카운터,1전역카운터)
	어떤 기기가 네 개의 cpu 가지면 그 시스템은 네 개의 지역 카운터와 하나의 전역 카운터 가짐
이외에도 지역 카운터를 위한 락들과 전역 카운터를 위한 락이 존재함
     각 코어마다 하나 이상의 쓰레드가 있을 것이라고 가정하기 때문에 카운터 마다 지역 락이 필요하다. 만일 그렇지 않고 오직 하나의 쓰레드만 코어에서 실행된다면 지역 락은 필요하지 않다.


### 근사 카운터 기본 개념
쓰레드는 지역 카운터를 증가시킴
지역 카운터는 지역 락에 의해 보호됨
각 cpu는 각각 지역 카운터를 갖기 때문에 
cpu들에 분산되어 있는 쓰레드들은 지역카운터를 경쟁 없이 갱신 가능
> 카운터 갱신은 확장성이 있다.

쓰레드는 전역 카운터를 읽어서 카운터 값을 판단함
전역 카운터의 값은 주기적으로 지역 카운터 값을 반영하여 주기적으로 갱신되어야 함
전역 락을 사용해 지역 카운터의 값을 전역 카운터의 값에 더하고, 그 지역 카운터 값은 0으로 초기화

지역에서 전역으로 값을 전달하는 빈도는 정해 놓은 S값에 의해 결정됨
S의 값이 작다 > 갱신 빈도가 크다, 카운터의 확장성 없어짐
S의 값이 크다 > 갱신 빈도가 작다, 전역 카운터의 값과 실제 카운터의 값이 일치하지 않을 확률 커짐

정확한 카운터 값을 계산하기 위해 모든 지역 카운터와 전역 카운터에 대한 락을 획득한 후 계산
락 연산으로 인한 성능 하락 심각할 수 있음
또 지역 카운터에 대한 락을 획득 순서를 적절히 제어하지 않으면 교착 상태가 발생함.
```



## 29 Lock-based Concurrent DS - Counter (1/4)

thread safe, MT-safe, 멀티 프로세서 환경에서도 safe해야 



카운터, 

scalable == 확장성이 있다, cpu가 여러개 있을때 그 개수만큼 빠르게 할 수 있느냐



락을써서 경쟁조건을 제거하자

병목현상, bottle neck발생가능,,



​	approximate, counter 구현,

락을 쓰레드별로 가짐

글로벌 락, 카운터는 1개씩

각 쓰레드마다 로컬 카운터가 존재 > 자기만 써서 경쟁조건없음

글로벌 업뎃하고 로컬카운트를 0으로 하고



글로벌 카운터는 글로벌 락을 통해 경쟁조건 제거

/



 







# 퀴즈

리무브 스핀

```markdown
Fig 28.8에서 CPU가 1개 일 때 우선 순위가 낮은 쓰레드가 먼저 락을 얻어 사용하는 중에 우선 순위가 높은 쓰레드가 락을 얻으려고 하면 이 spin 상태를 영원히 빠져나오지 못하는데 이를 Yield()를 사용하여 해결하였다.
> 

Fig 28.9에서 쓰레드 T1의 실행이 21, 22번 사이에 있을 때  다른 쓰레드 T2의 unlock()이 실행되면 큐에 있던 T1이 제거되고 나중에 park()로 sleep하게 되어  이 상태를 깨울 수 없게 된다.
>

Fig 28.9 처럼 락을 못 얻었을 때 spin 대신 wait queue에서 대기 하면 priority inversion 현상을 제거 할 수 있다.
>

Fig 28.9에서 CPU가 2개 이상이라면 guard 때문에 기다리는 spin의 길이는 예측 불가하지않고 flag를 검사하고 바꾸는 정도의 정해진 길이이다.
>

Fig 28.8에서 Yield()를 통해 spin을 줄였으므로 starvation 현상이 제거된다.	답 5
>

Fig 28.9의 21, 22번 줄의 순서를 바꿔야 lock()과 unlock()사이의 경쟁 조건을 제거한다.
>

Fig 28.9는 락을 얻을 쓰레드를 운영체제가 관리하도록 하여 starvation 현상을 제거하려는 시도이다.
>
```







뮤텍스

```markdown
락에서 리턴하면 락 얻은거임

1. Line 16, 17 사이에서 다른 쓰레드가 mutex_unlock() 하게 되면 Line 17에서 mutex가 가리키는 곳의 값과 v의 값이 다르게 된다.
> ㅇ

2. Line 15에서 v가 양수가 되는 경우는 Line 14, 15 사이에서 다른 쓰레드가 mutex_unlock() 했다고 볼 수 있다.
> ㅇ 양수인 경우는 다른 쓰레드가 언락해서 최상위비트가 0인 경우죠. 맞다
> 아니래 시바

3. LIne 7, 8 사이에서 다른 쓰레드가 mutex_unlock()을 하면 Line 15에서 음수가 아닌지 확인해야 한다.
> 아님 8에서 바로 확인할듯 아닌가?
> 아님

4. Line 5, 6 사이에서 다른 쓰레드가 mutex_unlock() 했다면 Line 8에서 Lock을 얻게되고 Line 6에서 증가된 것은 Line 9의 감소로 상쇄된다.
> ㅇ


5. Line 7, 8 사이에서 다른 쓰레드가 mutex_unlock() 했다면 Line 9의 atomic_decrement()에 의해서 mutex는 음수가 된다.
> 이미 위에서 증가해서 음수가 아니라 0이 되거나 할듯 최소 0이겠지
> ㄴ
6. Line 17의 futex_wait()에서 실제 sleep 되었다면 나중에 깨어난 후에 while() 루프에서 바로 빠져 나온다.
> 먼소리야. 
> ㄴ 루프에서 다시 뮤텍스 값 체크하고 그러는

7. Line 17의 futex_wait()에서 깨어났다면 다른 쓰레드가 Line 29의 futex_wake()를 호출한 것이며 이는 Line 6에서 atomic_increment()를 한 덕분이다.
> ㅇ, ㅇ 그치...대기큐에 넣었으니까 깨어난거 아닌가

8. Line 17의 futext_wait()에서 sleep이 되지 않았다면 Line 14, 15 사이에서 다른 쓰레드가 mutex_unlock() 했다고 볼 수 있다.
> 그럴수 있지 ㅇ
```



```
6번 지피티
futex_wait() 함수는 뮤텍스 값을 확인하고 슬립 상태로 전환시키는 기능을 수행합니다. 쓰레드가 futex_wait() 함수를 호출하면, 해당 쓰레드는 대기 상태로 들어가고 스케줄러에 의해 다른 쓰레드가 실행됩니다.

나중에 쓰레드가 깨어나서 다시 실행될 때, while 루프에서 다시 뮤텍스 값을 확인하게 됩니다. 이때, 뮤텍스 값이 여전히 음수인 경우 쓰레드는 다시 대기 상태로 진입하고, 뮤텍스 값이 양수로 변경되었다면 쓰레드는 뮤텍스를 획득한 것입니다.

따라서 실제로 슬립한 후 깨어난 쓰레드는 while 루프에서 뮤텍스 값을 다시 확인하게 되며, 여전히 뮤텍스를 획득하지 못했다면 다시 대기 상태로 진입합니다. 이러한 과정을 반복하여 다른 쓰레드가 뮤텍스를 해제하고 해당 쓰레드가 뮤텍스를 획득할 수 있을 때까지 대기하게 됩니다. 따라서 while 루프를 반복해야만 뮤텍스를 획득할 수 있는 상황이 되는 것이며, 즉시 루프를 빠져나오는 것은 아닙니다.
```





````

void mutex_lock(int *mutex)
{
    int v;
    /* 31번째 비트가 이미 초기화되어 있다. mutex를 이미획득했다.
    바로 리턴한다. (빠르게 실행하는 방법) */
    if (atomic_bit_test_set(mutex, 31) == 0)
        return;
    atomic_increment(mutex);
    while (1)
    {

        if (atomic_bit_test_set(mutex, 31) == 0)
        {
            atomic_decrement(mutex);
            return;
        }
        /* 이제 대기해야 한다. 먼저, 우리가 관찰 중인 futex 값이
        실제로 음수 인지 확인해야 한다(잠겨있는 상태인지). */
        v = *mutex;
        if (v >= 0)
            continue;
        futex_wait(mutex, v);
    }
}
void mutex_unlock(int *mutex)
{
    /* 필요충분조건으로 관심 대상의 다른 쓰레드가 없는 경우에 한해서
    0x80000000를 카운터에 더하면 0을 얻는다. */
    if (atomic_add_zero(mutex, 0x80000000))
        return;
    /* 이 mutex를 기다리는 다른 쓰레드가 있다면
    그 쓰레드들을 깨운다. */
}
````

