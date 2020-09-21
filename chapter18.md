# 🎈18. 함수와 일급 객체 part arrangement

## 🔎 일급 객체

다음 조건을 만족하는 객체를 일급 객체(fist-class object)라고 한다.

1. 무명 리터럴 생성 가능, 런타임에 생성 가능
2. 변수나 자료구조(객체, 배열 등)에 저장할 수 있다.
3. 함수의 매개변수에게 전달 할 수 있다.
4. 함수의 반환값으로 사용할 수 있다.

```javascript
// 1. 함수는 무명의 리터럴로 생성할 수 있다.
// 2. 함수는 변수에 저장할 수있다.
// 런타임에 함수 리터럴이 평가되어 함수 객체가 생성되고 변수에 할당된다.

const increase = function (num) {
  return ++num;
};

const decrease = function (num) {
  return --num;
};

// 2. 함수는 객체에 저장할 수 있다.
const predicates = { increase, decrease };

// 3. 함수의 매개변수에게 전달 할 수 있다.
// 4. 함수의 반환값으로 사용할 수 있다.

function makeCounter(predicate) {
  let num = 0;

  return function () {
    num = predicate(num);
    return num;
  };
}

// 3. 함수는 매개변수에게 함수를 전달할 수 있다.
const increaser = makeCounter(predicates.increase);
console.log(increaser()); // 1
console.log(increaser()); // 2
```

**함수가 일급객체 라는것은 함수를 객체와 동일하게 사용할 수 있다는 의미이다.** 객체는 값이므로 **함수는 값과 동일하게 취급할 수 있다.**
함수는 값을 사용할 수 있는 곳(변수 할당문, 객체의 프로퍼티 값, 배열의 요소, 함수 호출의 인수, 함수 반환문)이라면 어디서든지 리터럴로 정의할 수있으며 런타임에 함수 객체로 평가된다.

일급 객체로서 함수가 가지는 가장 큰 특징은 일반 객체와 같이 **함수의 매개변수에 전달할 수 있으며, 함수의 반환값으로 사용할 수도 있다는 것이다.**

## 👓 함수 객체의 프로퍼티

함수는 객체이다. 따라서 함수도 프로퍼티를 가질수 있다.

```javascript
function square(number) {
  return number * number;
}

console.log(Object.getOwnPropertyDescriptors(square));
/*
{
  length: {value: 1, writable: false, enumerable: false, configurable: true},
  name: {value: "square", writable: false, enumerable: false, configurable: true},
  arguments: {value: null, writable: false, enumerable: false, configurable: false},
  caller: {value: null, writable: false, enumerable: false, configurable: false},
  prototype: {value: {...}, writable: true, enumerable: false, configurable: false}
}
*/

console.log(Object.getOwnPropertyDescriptor(square, '__proto__'));

console.log(Object.getOwnPropertyDescriptor(Object.prototype, '__proto'));
```

arguments, caller, length, name, prototype 프로퍼티는 모두 함수 객체의 데이터 프로퍼티이다. 이들 프로퍼티는 일반 객체에는 없는 함수 객체의 고유 프로퍼티이다.

`__proto__`는 접근자 프로퍼티이며, 함수 객체 고유의 프로퍼티가 아니라 Object.prototype 객체의 프로퍼티를 상속받은것을 알 수 있다.

- ### 📩 arguments 프로퍼티

함수 객체의 arguments 프로퍼티 값은 arguments 객체다.
arguments 객체는 **<u>함수 호출시 전달된 인수들의 정보를 담고 있는</u> 순회 가능한 유사배열이다.**
함수내부에서는 지역변수처럼 사용되고, 함수 외부에서는 사용할 수 없다.

자바스크립트는 함수의 매개변수와 인수가 일치하는지 확인하지않는다.
그렇기에 매개변수의 갯수와 인수의 갯수가 동일하지않아도 에러가 발생하지 않는다.

```javascript
function multiply(x, y) {
  console.log(arguments);
  return x * y;
}

console.log(multiply()); // undefined * undefined = NaN
console.log(multiply(1)); // 1 * undefined = NaN
console.log(multiply(1, 2)); // 1 * 2
console.log(multiply(1, 2, 3)); // 1 * 2 3번째 인수는 무시 -> arguments 객체안에 저장
```

함수를 정의할 때 선언한 매개변수는 함수 몸체 내부에서 변수와 동일하게 취급되기에 **함수가 호출되면 함수 몸체내에서 매개변수가 선언되고 undefined로 초기화된 인수가 할당된다.**

인수의 개수를 확인하지 않는 자바스크립트 특성에 의해 호출되면 인수 개수를 확인하고 이에따라 함수의 동작을 달리 정의할 필요가 있을수 있다. 이때 유용하게 **arguments 객체를 이용해서 매개변수 개수를 확정할수 없는 가변인자 함수를 구현할수 있다.**

```javascript
function sum() {
  let res = 0;

  //arguments 객체는 length 프로퍼티가 있는 유사배열 객체 이므로 for 문으로 순회할 수 있다.
  for (let i = 0; i < arguments.length; i++) {
    res = res + arguments[i];
  }

  return res;
}

console.log(sum()); //0
console.log(sum(1, 2)); //6
console.log(sum(1, 2, 3)); //6
```

arguments는 유사 배열 객체로 배열 형태로 인자 정보를 담고 있고 실제 배열은 아니다. **유사배열 객체란? length 프로퍼티를 가진 객체로 for문으로 순회할수 있는 객체를의미한다.**

유사 배열 객체는 배열이 아니므로 배열 메서드를 사용하면 에러가 난다.

- ### 📞 caller 프로퍼티

- ### 📏 length 프로퍼티

- ### 📌 name 프로퍼티

- ### 🔬 **proto** 접근자 프로퍼티

- ### 🧬 prototype 프로퍼티
