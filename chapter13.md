# 🎈13. 스코프 part arrangement

## 🔎 스코프란?

**스코프(scope)는 유효범위를 뜻한다.**
스코프는 변수(var ,let, const)와 함수에 밀접한 관련성이 있다.

우리가 지금껏 공부해 왔던 것중에 **함수의 매개변수는 함수 몸체 내부에서만 참조할 수 있다고 했다.**
**매개변수의 스코프가 함수 몸체 내부로 한정되기 때문**이다.
아래의 코드를 살펴보자.

```javascript
function add(x, y) {
  console.log(x, y);
  return x + y;
}

add(20, 5);

// 매개변수는 함수 내부에서만 참조가능
console.log(x, y); // ReferenceError: x is not defined
```

**모든 식별자는 자신이 선언된 위치에 다른 코드가 식별자 자신을 참조할수 있는 범위가 결정**되는데, 이것을 스코프라고 한다.
이처럼 **식별자를 참조하여 실행할수있는 범위를 스코프 라고한다.**

자바스크립트는 코드를 실행할때 **문맥(context)을 파악해서 코드를 실행**하는데 만약 <u>같은이름을 가진 변수가 2개</u>있다고 생각해보자.

```javascript
var x = 10;

function ex() {
  var x = 20;
  console.log(x);
}

ex();

console.log(x);
```

위와 같은 상황에서 예상되는 변수 x의 각각의 출력같은 무엇일까?
ex라는 함수 안에있는 x의 변수는 참조값은 20이라는 값을 출력하고, ex라는 함수 밖에있는 x의 변수는 참조값은 10이라는 값을 출력한다.

스코프란 바로 자바스크립트 엔진에 의해서, **어떤 식별자를 참조해야하는지를 결정짓는 규칙**이라고 할수있다.

## 📚 스코프의 종류

코드는 크게 전역과 지역으로 구분할 수 있다.
스코프의 종류에는 **전역스코프**와 **지역스코프**가있다.

변수는 자신이 선언된 위치에 의해서 스코프를 가지게 되는데, **전역에서 선언하면 전역변수**가 되고, **함수 몸체 내부에서 선언되면 지역변수**가 된다.

### 📕 전역과 전역 스코프

전역이란, 코드의 가장 바깥영역을 뜻하며, **전역변수는 어디서든지 참조가 가능하다.**

```javascript
var x = 'globalScope';

function move() {
  console.log(x); // 'globalScope'
}

move();
```

### 📗 지역과 지역 스코프

**지역이란, 함수 몸체 내부를 뜻하며, 지역변수는 자신의 지역스코프와 그 아래 하위지역 스코프에서 사용할수 있다.**

```javascript
var x = 'globalScope';

function move() {
  var y = 'localScope';
  console.log(x); // 'globalScope'

  function stop() {
    console.log(y); // 'localScope'
  }
  stop();
}

move();

console.log(y); // ReferenceError y is not defined
```

## 👓 스코프체인

스코프 체인은 위에서 소스코드에서 본것처럼 **스코프들이 계층적 구조를 가지며 서로 연결된것을 말한다.**

스코프는 스코프 체인에 의해 **변수를 참조하는 스코프에서 시작**하여 그위의 **상위 스코프 방향으로 이동하면서 선언된 변수를 검색**하고 이것을 **참조할수 있는지를 파악**한다.

스코프 체인은 물리적인 실체로 존재하며 **코드실행전에 자료구조를 생성하는데 이것의 이름을 렉시컬환경이라고 한다.**

### 📰 스코프 체인에 의한 변수 검색

스코프 체인은 실행 컨텍스트의 렉시컬 환경을 단방향으로 검색하며 연결되어있는것을 말하는데,
이로인해서 **참조를 시작한 스코프에서 시작하여 상위스코프로 올라가며 식별자를 검색하고, 참조한다.
참조를 시작한 스코프의 하위스코프에 있는 식별자는 참조할수 없다.**

말이 너무 어렵기에 코드로 보는것이 더 편하다.

```javascript
var x = 'globalScope';

function move() {
  var y = 'localScope';
  console.log(x); // 'globalScope'

  function stop() {
    function restart() {
      var z = 'noAccess';
    }

    restart();
    console.log(y); // 'localScope'
    console.log(z); // ReferenceError z is not defined
  }
  stop();
}

move();

console.log(y); // ReferenceError y is not defined
```

여기서 restart함수 안에서 선언된 z변수를 stop이라는 상위 스코프를 가진 함수에서 참조할수 없다는것을 보여준다.

### 🧮 스코프 체인에 의한 함수 검색

아래의 예제를 보고 코드가 어떻게 동작할지 예측해보자!

```javascript
function tangerine() {
  console.log('global function tangerine');
}

function peanut() {
  function tangerine() {
    console.log('local function tangerine');
  }
  tangerine();
}

peanut();

//local function tangerine
```

위의 코드를 보면, tangerine함수를 호출하는 것은 peanut함수 내에서 이루어진다.
**함수를 함수 선언문으로 정의하면 런타임 이전에 함수 객체가 생성**된다. 그리고 자바스크립트 엔진은 tangerine이라는 **함수이름과 동일한 함수식별자를 선언하고 생성된 함수 객체를 할당**하게된다.

즉, 함수도 식별자에 할당되기에 스코프를 갖는다 라고 말할수 있다.

## 🔐 함수 레벨 스코프

지역은 함수 몸체 내부를 말하고 지역은 지역 스코프를 만든다고 했으니 이는, 코드블록이 아닌 함수에 의해서만 지역 스코프가 생성된다는 의미이다.

기존에 다른 프로그래밍 언어에서는 **모든 코드블록들이 지역스코프를 만들었지만(블록 레벨 스코프),**
여기서 주의해야하는점은 **var키워드로 선언된 변수는 오로지 함수의 코드 블록(함수 몸체)만을 지역 스코프로 인정한다.** 이러한 특성은 **함수 레벨 스코프**라 불리운다.

```javascript
var x = 'global';

if (true) {
  var x = 'local';
}
console.log(x); //'local'
```

위코드 처럼 **var로 선언된 변수는 함수 레벨 스코프만을 스코프로 인정하기때문에 코드블록 바깥에서도 참조가 가능**하게 된다.

## 📌 렉시컬 스코프

```javascript
var x = 1;

function first() {
  var x = 30;
  second();
}

function second() {
  console.log(x);
}

first();
second();
```

함수를 실행할때 어디서 호출했는지에 따라서 함수의 상위 스코프를 결정하는것을 동적스코프 라고하고,
함수를 어디서 정의하였는지에 따라 함수의 상위 스코프를 결정하는것은 렉시컬스코프,정적 스코프라고 하는데, 자바스크립트는 렉시컬 스코프를 사용한다.

**즉, 함수를 어디서 호출했는지가 아닌, 함수의 상위스코프는 함수가 정의된 곳을 기준으로 결정되고, 함수객체는 자신의 상위 객체를 기억한다.** 이는 함수 호출시 상위 스코프를 참조할 필요가 있기 때문이다.
