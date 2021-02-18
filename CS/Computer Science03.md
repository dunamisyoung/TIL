# 알고리즘- CS50 (naver boostcourse)

---

## 알고리즘

알고리즘 이라는 것은 무엇일까? 알고리즘은 문제 해결 방식이라고 말할수있겠다. 알고리즘은 입력을 받은 컴퓨터에서 사용되는 출력 이전의 행동이라고 할수있겠는데 이를통해 출력의 값들이 변하게된다. 이때 어떤식으로 문제를 해결해야 문제를 순차적으로 해결해나갈수있을지를 생각하는것 그것이 바로 알고리즘이다. 그 후에 효율성을 극대화 시킬것인가에 대해 판단하고 그에 따라 시간을 단축하는 결과를 얻을수 있을것이다.

### 정확한 알고리즘

정확한 알고리즘은 위에서 언급한것처럼, 문제 해결에 초점이 맞추어져있다. 예를들어 전화번호부에서 **홍길동** 이라는 이름을 찾는다. 라고 가정했을경우에 우리는 어떻게 찾을수있을까? 한장한장 넘겨가며 홍길동을 찾을떄 까지 반복할것이다. 하지만 전화번호부의 페이지가 10000 페이지라고했을때 이렇게 하면 효율성 측면에서 매우 오랜시간을 사용하게 될것이다. 그렇다고 2페이지 씩 넘긴다고 홍길동을 빨리 찾을수 있을까? 결코 그렇지 않다. 결국 2페이지씩 넘어간 곳에 홍길동이라는 이름이 적혀있을수 있기때문이다.

### 정확하고 효율적인 알고리즘

전화번호부에서 홍길동을 찾을떄 이름이 가,나,다 순으로 정렬되어있다고 생각해보자. 그렇다면 조금 더 빠르게 홍길동이라는 이름에 접근할수 있을것이다. **"홍"** 라는 이름이 새겨진 곳을 먼저 파악할것이고 그럼 필요없는 **"홍"** 이전의 값은 버릴수있을것이다. 그리고는 다시 두번째 이름인 **"길"** 이들어있지 않은 부분의 것들의 앞부분은 버릴것이다. 이런식으로 반복하다보면 결국 반복해야하는 데이터들을 줄이면서 빠르게 원하는 값을 찾을수있게된다.

좀더 효율적인 알고리즘은 값에 빠르게 접근할수있게 된다.

### 의사코드(pseudocode)

의사코드를 통해 우리는 문제 해결에 필요한 행동이나 조건을 설정하여 컴퓨터적인 사고방식인 절차지향적 사고를 하게끔 도와준다.

만약 친구와 1부터 100까지 숫자중 1가지 숫자를 맞추는 스무고개 게임을 한다고 했을떄 어떤 알고리즘을 사용할것인가? 의사코드로 표현해보자.

```jsx
1. 술래를 정한다.
2. 술래는 마음속으로 숫자를 정한다.
3. 다른 한명은 1 ~ 100 까지 수중 1개를 말한다. 다른한명이 수를 말할때마다 카운트를 1증가시킨다.(초기값은 0이다)
4. 술래가 정한 수와 친구가 말한 수가 일치하면, **친구의 승리**이며 게임이 종료된다. 친구가 말한 횟수가 20번이 넘으면 **술래의 승리**이며 게임이 종료된다. 어느것도 해당되지 않다면 5번으로 이동한다. 않다면 5번으로 이동한다.
5. 술래는 친구가 말한수가 자신이 정한 수보다 큰지, 작은지를 말해준다. 크다면 6번 작다면 7번으로 이동한다.
6. 친구는 자신이 이전에 말했던 수와 그 이상의 수를 모두 버린다. 다시 3번으로 이동하며 기존 수의 범위에 자신이 버린수를 제외하고 덮어씌운다.
7. 친구는 자신이 이전에 말했던 수와 그 이하의 수를 모두 버린다. 다시 3번으로 이동한다 기존 수의 범위에 자신이 버린수를 제외하고 덮어씌운다.
```

### 1. 컴퓨팅 사고 단원을 마치며 quiz :

![50](https://user-images.githubusercontent.com/66991380/108366538-d5c49800-723b-11eb-8595-9c57d186febf.jpg)
![quiz01](https://user-images.githubusercontent.com/66991380/108366564-de1cd300-723b-11eb-8759-04cf9c0bffbe.jpg)