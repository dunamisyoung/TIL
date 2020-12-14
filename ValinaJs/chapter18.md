# 함수와 일급객체

## 1. 일급 객체

다음과 같은 조건을 만족하는 객체를 일급 객체라고 한다.

- 무명의 리터럴로 생성이 가능하다.
- 변수나 자료구조(객체, 배열 등)에 저장이 가능하다.
- 함수의 매개변수에 전달할 수 있다.
- 함수의 반환값으로 사용할 수 있다.

**자바스크립트에서의 함수는 일급객체의 조건을 모두 만족함으로 일급객체이다.**

```javascript
// 함수는 무명의 리터럴로 생성이 가능하다.
// 함수는 변수에 저장할 수 있다.
// 런타임에 함수 리터럴이 평가되어 함수 객체가 생성되며 변수에 할당된다.
const increase = function (num) {
	return ++num;
};

const decrease = function (num) {
	return --num
};

// 함수는 객체에 저장할 수 있다.
const predicates = {increase, decrease}

// 함수의 매개변수에 전달할 수 있다.
// 함수의 반환값으로 사용할 수 있다.
function makeCounter(predicate) {
	let num = 0;
	return function ({
		num = predicate(num);
		return num;
	};
}

const increase = makeCounter(predicates.increase);
const decrease = makeCounter(predicates.decrease);
```

함수가 일급 객체라는 것은 함수를 객체와 동일하게 취급할 수 있다. 라는것이며, **변수 할당문, 객체의 프로퍼티값, 배열의 요소, 함수 호출의 인수, 함수 반환문 등 값이 올수 있는 위치에 정의될 수 있다. 라는것이다.**

일급 객체로써 가지는 가장큰 특징은 일반 객체와 같이 함수의 매개변수에 전달이 가능하고, 함수의 반환값으로 사용할수 있다는 것이다.

함수가 일반객체와 다른점 하나는 일반객체는 호출할수 없지만, 함수 객체는 호출할 수 있다는 점이며, 함수 객체에는 일반 객체에 없는 함수 고유 프로퍼티가 있다.

## 2. 함수 객체의 프로퍼티

함수는 객체이다. 따라서 함수도 프로퍼티를 가질 수 있다.

함수의 모든 프로퍼티의 어트리뷰트를 Object.getOwnPropertyDescriptors 메서드로 확인해보자

```javascript
function square(number) {
  return number * number;
}

console.log(Object.getOwnPropertyDescriptors(square));
/*
	arguments: {value: null, writable: false, enumerable: false, configurable: false}
	caller: {value: null, writable: false, enumerable: false, configurable: false}
	length: {value: 1, writable: false, enumerable: false, configurable: true}
	name: {value: "square", writable: false, enumerable: false, configurable: true}
	prototype: {value: {…}, writable: true, enumerable: false, configurable: false}
	__proto__: Object
*/

// __proto__는 square 함수의 프로퍼티가 아닌 Object.prototype 객체의 프로퍼티를 상속받은것이다.
console.log(Object.getOwnPropertyDescriptor(square, '__proto__')); // undefined
// square 함수는 Object.prototype 객체로 부터 __proto__ 라는 접근자 프로퍼티를 상속받습니다.
console.log(Object.getOwnPropertyDescriptor(Object.prototype, '__proto__'));
// {get
```

**arguments, caller, name, prototype** 프로퍼티는 함수 객체의 데이터 프로퍼티이며, 일반객체에는 없는 함수 고유의 프로퍼티이다. 하지만 **`__proto__` 는** Object.prototype 객체의 프로퍼티이며 이는 모든 객체가 사용할수있다.

### 2.1 arguments 프로퍼티

함수 객체의 arguments 프로퍼티 값은 arguments 객체이다.

**arguments 객체는 함수 호출시 인수들의 정보를 담고 있는 순회 가능한 유사배열 이다.**

**함수 내부에서 지역변수처럼 사용이가능**하다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cba3d71d-b154-439e-9b9b-90b2c7a1edb1/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cba3d71d-b154-439e-9b9b-90b2c7a1edb1/Untitled.png)

_poiemaWeb이미지참조_

함수를 정의할때 선언한 매개변수는 함수호출시 선언과 동시에 암묵적으로 **undefined로 초기화되**고, 그이후에 할당한 인수의 값이 전달된다.

자바스크립트는 매개변수와 인수가 일치하는지 확인하지 않으며 개수수가 다르다고 해서 오류가 발생하지 않는다. 인수의 개수와 매개 변수의 개수가 다를때는 어떻게 될까?

매개변수의 개수가 인수의 개수보다 많을때 인수를 할당받지 못한 매개변수는 **undefined 로 초기화된 상태를 유지**하고, 매개변수의 개수보다 인수의 개수를 더많이 전달한 경우에는 위 그림처럼 **암묵적으로 arguments 객체에 프로퍼티로 보관**된다.

**arguments 객체는 인수를 프로퍼티 값으로 소유하며 프로퍼티키는 인수의 순서를 나타낸다.**

**arguments** 객체의 callee프로퍼티는 호출되어 **arguments** 객체를 생성한 함수자신을 가르키며, length프로퍼티는 인수의 갯수를 가리킨다. 이처럼 **arguments** 객체는 유사배열객체이다.

여기서 **유사배열 객체**란 **length 프로퍼티를 가진 객체**로 **for문으로 순회할수 있는 객체**를 말한다.

보통의 **arguments** 객체는 매개변수 갯수를 확정할수 없는 가변 인자 함수를 구현할때 사용된다.

arguments 객체는 배열이 아니므로 배열 메서드를 사용해야할때 Function.prototype.call, Function.prototype.apply를 사용해 간접호출을 해주어야한다.

```javascript
// 아래의 배열고차함수인 reduce 메서드는 나중에 좀더 자세히 알아보자.

function sum() {
  const array = Array.prototype.slice.call(arguments);
  return array.reduce(function (pre, cur) {
    return pre + cur;
  }, 0);
}
```

이러한 번거로움을 해결하기위해 ES6에서는 Rest파라미터를 도입하였다. Rest파라미터는 추후에 좀더 알아보도록하자.

```javascript
function sum(...args){
	return args.reduce((pre, cur) => pre + cur, 0);
}
console.log(sum(1, 2)); // 3
console.log(sum(1, 2, 3, 4, 5); // 15
```

### 2.2 caller 프로퍼티

caller 프로퍼티는 ECMAscript 사양에 포함되지 않은 비표준 프로퍼티이다.

간단한 설명으로는 **함수 객체의 caller 프로퍼티는 함수 자신을 호출한 함수를 가리킨다**.라는것 정도만 알아가자.

### 2.3 length 프로퍼티

함수 객체의 length 프로퍼티는 함수를 정의할때 선언한 매개변수의 개수를 가르킨다.

```javascript
function foo() {
  console.log(foo.length); //0
}

function bar(x) {
  return x;
}
console.log(bar.length); //1

function baz(x, y) {
  return x * y;
}
console.log(baz.length); //2
```

여기서 주의해야 할점은, arguments 객체의 length프로퍼티는 인자(arguments)의 개수를 가르키고, 함수객체의 프로퍼티는 매개변수(parameter)의 개수를 가르킨다.

### 2.4. name 프로퍼티

함수 객체의 name 프로퍼티는 함수 이름을 나타낸다.

name 프로퍼티는 ES5와 ES6에서의 동작이 다른데 익명 함수표현식의 경우 ES5에서 name 프로퍼티는 빈문자열, ES6에서는 함수 객체를 가르키는 식별자를 가진다.

### 2.5 **\*\*proto**\*\* 접근자 프로퍼티

모든 객체는 `[[Prototype]]` 이라는 내부 슬롯을 가진다.

`[[Prototype]]` 내부슬롯은 객체지향 프로그래밍의 상속을 구현하는 프로토타입 객체를 가르킨다.

**P**roto**** 프로퍼티는 `[[Prototype]]` 내부 슬롯이 가리키는 프로토타입 객체에 접근을위한 접근자 프로퍼티 이다. 이는 내부슬롯에는 직접접근할수 없기에 프로토타입 객체에 간접적인 접근 방식을 제공하는 것이다.

```javascript
// 객체 리터럴 방식으로 생성한 객체의 프로토 타입 객체는 Object.prototype 이다.
const tangerine = { age: 20 };

console.log(tangerine.__proto__ === Object.prototype); // true

/*
	객체 리터럴 방식으로 생성한 객체는 프로토 타입 객체인 Object.prototype의 프로퍼티를 상속받으며
	hasOwnProperty 메서드는 Object.prototype의 메서드다.
	이는 전달받은 프로퍼티 키가 고유 프로퍼티인 경우에만 true를 반환한다.
	그렇지 않고 상속받은 프로퍼티인 경우 false를 반환한다.
*/

console.log(tangerine.hasOwnProperty('age')); // true
console.log(tangerine.hasOwnProperty('__proto__')); // false
```
