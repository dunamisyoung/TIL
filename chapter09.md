# 🎈9. 타입 변환과 단축 평가 part arrangement

## 🔎 타입변환이란?

**자바스크립트의 모든 값은 타입이 있다.**

개발자가 **의도적으로 값의 타입을 변환하는것을 명시적 타입변환**(explicit coercion)또는 **타입 캐스팅**(type casting)이라 한다.

```javascript
var result = 100;
result = '백점';
// 위코드는 명시적 타입변환이 아니다. 이것은 재할당을 의미한다.

var score = 90;
var newScore = score.toString();

console.log(typeof newScore, newScore);
// 이것이 명시적 타입변환이다. 출력하게되면 string, 90이 나오는데 뒤에 있는 90은 숫자값 90이 아니라 문자열 90이다.

console.log(typeof score);
// 기존의 score 90의 값은 변하지 않는다. 그저 새로운 값을 만들어 낸것이다.
```

위의 코드처럼 **개발자가 의도하여서 타입을 변경한것이 아니면 바로 그것이 암묵적 타입 변환이다.**

```javascript
var score = 10;

var newScore = score + '';
console.log(typeof newScore, newScore);
// 숫자값 10과 빈문자열이 더해져 암묵적으로 숫자값 10이 아닌 문자열 10을 만들어 낸다.

console.log(typeof score);
// 기존에 score라는 변수 식별자에 담겨 있던 10이라는 숫자값은 변하지 않았다.
```

**암묵적타입변환**과 **명시적타입변환**을 통해 예제에서 살펴본 score라는 변수에 담긴 **원시값을 변경할수는 없다.**
**원시값은 변경 불가능한 값**이기 때문이다.
타입변환은 <u>**기존의 원시값을 이용해 새로운 원시값을 생성하는것 일뿐이다.**</u>

그렇다면 이렇게 예측하기 힘든 암묵적 타입변환을 도출하는 소스코드는 작성하면 안되는것일까?
옳고 그름을 벗어나 두가지 방법 모두다 **제대로 동작원리를 이해하고 사용하는것에 초점을 두면 좋을것이라고 생각한다.**

## 🕶 암묵적 타입변환

자바스크립트 엔진은 표현식을 평가할때 오류를 최소화 하기위해 개발자의 의도와 다르게 동작한다. 즉, 암묵적으로 데이터 타입을 강제 변환하는경우가있다.

```javascript
// 좌항과 우항의 값이 암묵적으로 타입변환되어 문자열로 해석된다.
'10' + 7; // '107'

// 좌항과 우항의 값이 암묵적으로 타입변환되어 숫자로 해석된다.
10 * '7'; // 70

// boolean 타입으로 변환되어 해석된다.
!1; // false
```

### 📰 문자열 타입으로 변환

```javascript
10 + '7'; // 17
```

위 예제에서의 `+`연산자는 문자열 연결 연산자로 동작하였다.
자바스크립트 엔진은 표현식을 평가하기위해 **문자열이 아닌 다른 피연산자의 타입을 암묵적으로 문자열로 변환시킨다.**

**문자열 연결연산자의 동작조건은 피연산자중 <u>하나 이상이 문자열 일때 동작</u>한다.**
이뿐만이 아니라 ES6에서 도입된 **탬플릿 리터럴의 표현식 삽입에서도 암묵적으로 타입변환이 이루어진다.**

```javascript
`우리팀의 점수는 ${90 + 7} 점이다.`; //우리팀의 점수는 97점이다.
```

아래의 예시들로 문자열 타입의 암묵적 타입변환을 살펴보자.

```javascript
// 숫자타입
0 + ''; // '0'
-0 + ''; // '0'
1 + '' // '1'
-1 + '' // '-1'
NaN + '' // 'NaN'
Infinity + ''//'Infinity'
-Infinity + ''//'-Infinity'

// 불리언 타입
true + '' // "true"
false + '' // "false"

// null 타입
null + '' // "null"

//undefined + '' // "undefined"

({}) + '' // '[object Object]'
Math + '' // "[object Math]"
[] + ''; // ''
[10, 20] + ''; // '10,20';
(function () {} + ''); // "function(){}"
Array + ''; // "function Array(){[native code]}"
```

### 🧮 숫자 타입으로 변환

```javascript
10 - '1'; // 9
10 * '1'; // 10
10 / 'one'; // NaN
```

위 예제에서 사용한 연산자는 모두 산술연산자이다.
**산술연산자의 피연산자에는 코드 문맥상 숫자값이 위치해야한다.**

자바스크립트엔진에 의해 **피연산자의 표현식의 값이 타입이 숫자값이 아닌경우 암묵적으로 숫자타입으로 변환**시킨다.
만약, **피연산자를 숫자타입으로 변환할수 없는경우에는 NaN을 출력**하게된다.

```javascript
'1' > 0; // true
```

비교 연산자의 역할은 불리언 값을 만드는 것이다.
`>` 비교연산자는 피연산자의 크기를 비교함으로 **피연산자의 타입값을 숫자 값으로 암묵적 변환하여서 출력한다.**

자바스크립트 엔진에 의해 숫자타입으로 값을 변환한다는것은 **`+`단항 연산자는 숫자 타입의 값이 아니면 숫자 타입의 값으로 암묵적 타입 변환을 수행**한다고 할수있다. 아래의 예시를 보자.

```javascript
// 문자열 타입
+''; //0
+'0'; //0
+'10'; //10
+'string'; //NaN

//boolean타입
+true; //1
+false; //0

//undefined타입
+undefined; // NaN

//심벌 타입
+Symbol(); // ypeError : Cannot convert a Symbol value to a number

//객체 타입
+{}; //NaN
+[]; //0
+[10, 20]; //NaN
+function () {}; //NaN
```

### 🔐 불리언 타입으로 변환

다음 예제를 살펴보자.

```javascript
//'' 빈문자열은 false로 평가되어 어느것도 반환하지 않는다.
if ('') console.log(x);
```

if문이나 for문과 같은 **제어문 또는 삼항 조건연산자에서의 조건식은 불리언값으로 평가되어야하는 표현식**이다. 그렇기에 자바스크립트 엔진은 **불리언 타입으로 암묵적인 타입변환**을 한다.

```javascript
if ('') console.log('1'); //빈문자열은 false로 평가된다.
if (true) console.log('2');
if (0) console.log('3'); // 숫자값 0도 false로 평가된다.
if ('str') console.log('4'); //빈문자열이 아닌 문자열은 true로 평가된다.
if (null) console.log('5'); //null도 false로 평가된다.

// 2 4
```

자바스크립트 엔진은 불리언 타입이 아닌 값을 **Truthy 값(참으로평가되는 값)** 또는 **Falsy값(거짓으로 평가되는 값)으로 구분**한다. 즉, 제어문의 조건식에서의 평가결과를 `Truthy = true` , `Falsy = false`로 평가한다.

아래의 값들은 자바스크립트 엔진에 의해서 `false`로 평가되는값이다.

- false;
- undefined;
- null;
- 0, -0;
- NaN;
- '';

<u>이것들을 제외한 모든 값</u>은 **true로 평가되는 Truthy 값이다.**

```javascript
if (!false) console.log(false + 'is falsy value');
if (!undefined) console.log(undefined + 'is falsy value');
if (!null) console.log(null + 'is falsy value');
if (!0) console.log(0 + 'is falsy value');
if (!NaN) console.log(NaN + 'is falsy value');
if (!'') console.log('' + 'is falsy value');
```

## 👓 명시적 타입변환

이번에는 **개발자의 의도에 따라 명시적으로 타입을 변경하는 명시적 타입 변환**에대해서 살펴보자.

### 📰 문자열 타입으로 변환

**문자열 타입이 아닌 값을 문자열 타입으로 변환하는 방법**에는 이런것이있다.

1. String 생성자 함수를 new 연산자 없이 호출하는 방법
2. Object.prototype.toSrting 메서드를 사용하는 방법
3. 문자열 연결 연산자를 이용하는 방법

```javascript
//1. String 생성자 함수를 new 연산자 없이 호출하는 방법
// 숫자 타입 => 문자열 타입
String(1); // '1'
String(NaN); // 'NaN'
String(Infinity); // 'Infinity'

// 불리언 타입 => 문자열 타입
String(true); // 'true'
String(false); // 'false'
```

```javascript
//2. Object.prototype.toString 메서드를 사용하는 방법
// 숫자 타입 => 문자열타입
(1).toString(); // '1'
NaN.toString(); // 'NaN'
Infinity.toString(); // 'Infinity'

// 불리언 타입 => 문자열 타입
true.toString(); // 'true'
false.toString(); // 'false'
```

```javascript
//3. 문자열 연결 연산자를 이용하는 방법
// 숫자타입 => 문자열타입
1 + ''; // '1'
NaN + ''; // 'NaN'
Infinity + ''; // 'Infinity'

//불리언 타입 => 문자열 타입
true + ''; // 'true'
false + ''; // 'false'
```

### 🧮 숫자 타입으로 변환

숫자 타입이 아닌 값을 숫자 타입으로 변환하는 방법은 다음과 같다.

1. Number 생성자 함수를 new 연산자 없이 호출하는 방법
2. parseInt, parseFloat 함수를 사용하는 방법(문자열만 숫자 타입으로 변환 가능)
3. +단항 산술 연산자를 이용하는 방법
4. `*`산술 연산자를 이용하는 방법

```javascript
// 1. Number 생성자 함수를 new 연산자 없이 호출하는 방법
// 문자열 타입 => 숫자 타입
Number('0'); //0
Number('-1'); //-1
Number('13.05'); //13.05

// 불리언 타입 => 숫자 타입
Number('true'); //1
Number('false'); //0
```

```javascript
//2. parseInt(정수로 변환), parseFloat(실수로 변환) 함수를 사용하는 방법(문자열만 변환 가능)
// 문자열 타입 => 숫자 타입
parseInt('0'); //0
parseInt('-1'); //-1
parseInt('13.05'); //13.05
```

```javascript
// 3. + 단항 산술 연산자를 이용하는 방법
// 문자열 타입 => 숫자 타입
+'0'; // 0
+'-1'; // -1
+'13.05'; // 13.05

//불리언 타입 => 숫자 타입
+true; // 1
+false; // 0
```

```javascript
// 4. *산술 연산자를 이용하는 방법
// 문자열 타입 => 숫자 타입
'0' * 1; // 0
'-1' * 1; // -1
'13.05' * 1; //13.05

//불리언 타입 => 숫자 타입
true * 1; // 1
false * 1; // 0
```

### 🔐 불리언 타입으로 변환

불리언 타입이 아닌 값을 불리언 타입으로 변환하는 방법은 다음과 같다.

1. Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
2. !부정논리 연산자를 두번 사용하는 방법

```javascript
//1. Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
// 문자열 타입 => 불리언 타입
Boolean('x'); // true;
Boolean(''); // '';
Boolean('false'); // false;

// 숫자 타입 => 불리언 타입
Boolean(0); // false
Boolean(1); // true
Boolean(NaN); // false
Boolean(Infinity); // true

// null 타입 => 불리언 타입
Boolean(null); // false

// undefined 타입 => 불리언 타입
Boolean(undefined); // false

//객체 타입 => 불리언 타입
Boolean({}); //true
Boolean([]); //true
```

```javascript
// 2. !부정 논리 연산자를 두번 사용하는 방법
// 문자열 타입 => 불리언 타입
!!'go'; //true
!!''; //false
!!'false'; //true

//숫자 타입 => 불리언 타입
!!0; //false
!!1; //true
!!NaN; //false
!!Infinity; //true

//null 타입 => 불리언타입
!!null; //false

//undefined 타입 => 불리언 타입
!!undefined; //false

//객체 타입 => 불리언타입
!!{}; // true
!![]; // true
```

## 📌 단축평가

논리합(||)연산자와 논리곱(&&)연산자 표현식의 평가 결과는 불리언 값이 아닐수도 있다.
좌항과 우항의 피연산자중 어느 한쪽으로 평가된다는 것이다.

### 📕 논리 연산자를 사용한 단축 평가

**논리 곱 연산자는 두개의 피연산자 모두 true로 평가되면 true를 반환한다.**

```javascript
'tangerine' && 'peanut'; // -> 'peanut'
```

첫번째 피연산자는 빈문자열이 아니기에 true로 평가된다. 좌항과 우항의 값이 모두 true 일떄 true를 반환하는 논리곱 연산자는 'peanut' 이라는 수를 통해 true가 결정되기에 peanut을 반환한다.

**이때, peanut의 타입변환은 이뤄지지 않고 그대로 반환된다.**

논리 합 연산자는 논리곱 연산자랑 무엇이 다른지 살펴보자.

**논리합 연산자는 둘중 하나의 피연산자가 true이어도 true를 반환한다.**

```javascript
'tangerine' || 'peanut'; ->// 'tangerine'
```

첫번째 피연산자인 'tangerine'은 빈문자열이 아니기에 true로 평가되며, 좌항과 우항의 피연산자중 하나의 값이라도 true 이면 true로 평가하기에 우항의 값을 평가할 필요없이 좌항의값, tangerine을 반환한다.

이때도 동일하게 타입변환은 이루어지지 않고 tangerine을 반환한다..

이와같이 단축평가란 표현식을 평가하는 도중에 평가결과가 확정되게 되면서 나머지 평가과정을 생략하는 과정을 의미한다.

즉, 단축평가에서는 코드의 흐름을 보고 값에대한 결정권을 어떠한 피연산자가 가지고 있는지 파악해야한다.

단축평가를 사용하면 if문을 대체할수 있다.

```javascript
var done = true;
var res = '';

if (done) res = '출력';

res = done && '출력';

console.log(res); // done이 true 이면 '출력'
```

여기서는 자바스크립트의 Falsy 값(false,'',null,undefined,NaN,0,-0)과 truty 값에 관해서 잘파악해서 변형시켜야 할것이다.

### 📗 옵셔널 체이닝 연산자

### 📘 null 병합 연산자
