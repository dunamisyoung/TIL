연필 → 볼펜 → 형광펜 = Computer Science

# 2진법 - CS50 (naver boostcourse)

---

## 컴퓨터 과학이란?

문제 해결에 대한 학문으로써 **입력을 받아 출력을 만들어내는 과정**을 뜻한다.

바로 그 중간에 있는 과정이 컴퓨터 과학이다.

이때 입력과 출력을 표현하기 위해 표현방식이 필요하다.

우리는 평상시에 0,1,2,3,4,5,6,7,8,9 총 10개의 기호를 통해 수를 표현한다. 이것을 바로 **10진법**이라고 한다. 하지만 컴퓨터는 모든 데이터를 0과 1로 표현한다. 이것을 바로 **2진법**이라고한다.

우리가 숫자 321을 읽을 떄 이것이 어떻게 삼백이십일 인지 알고있는가? 라고 했을떄, 이것은 백의자리에 위치한수가 3, 십의자리에 위치한수는 2, 일의자리에 위치한수는 1이기 떄문에 이것을 알수있다.

이것을 표현해보자면 3x100 + 2x10 + 1x1 = 321이라고 할수있으며, 각자리별로 10의 거듭제곱을 통해 자리수를 표현하게된다.

2진법이 기록되는 방법을 따져보면 각 자리의 수를 2의 거듭제곱으로 표현하고있다.

2진법으로 숫자 11을 표현한다면 어떻게 될까? 정답은 아래와 같다.

```jsx
128 64 32 16 8 4 2 1
  0  0  0  0 1 0 1 1
```

컴퓨터는 2진법에서 하나의 자릿수를 표현할때 단위를 비트(bit)라고 한다.

### 비트와 바이트

컴퓨터에서 정보를 저장하기위해 그리고 연산을 하기위해 bit라는 측정단위를 사용한다. 이는 0과 1이라는 두가지 값만 가질수 있는 측정단위이며 데이터를 여러비트로 나타냄으로 정보저장이 가능하며, 수학적 연산이 가능하다. 이에따라 많은 양에 데이터를 표현하기위해 만들어진것이 바이트이다.

1바이트(byte)는 8개의 비트가 모여 만들어진것으로 2^8 = 256개의 표현이 가능하며 128개의 비트라고 생각하면된다.