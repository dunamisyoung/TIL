# 🎈35. 스프레드 문법 part arrangement

## 🔎 스프레드 문법이란?

ES6에서 도입된 스프레드 문법`...`은 하나로 뭉쳐 있는 여러값들의 집합을 펼쳐서 전개, 분산하여 개별적인 값들의 목록으로 만든다.

스프레드 문법을 사용할 수 있는 대상은 Array, String, Map, Set, DOM컬렉션(NodeListHTMLCollection), arguments와 같이 for...of문으로 순회할 수 있는 이터러블에 한정된다.

스프레드 문법의 결과는 값이아니라 값들의 목록이다.

```jsx
const list = ...[1, 2, 3]; // SyntaxError : Unexpected token ...
```

이처럼 스프레드 문법의 결과물은 값으로 사용할 수 없고, 다음과 같이 쉼표로 구분한 값의 목록을 사용하는 문맥에서만 사용할 수 있다.

- 함수 호출문의 인수 목록
- 배열 리터럴의 요소 목록
- 객체 리터럴의 프로퍼티 목록

### 1. 함수 호출문의 인수 목록에서 사용하는 경우

요소들의 집합인 배열을 펼쳐서 개별적인 값들의 목록으로 만든후 이를 함수의 인수 목록으로 전달해야 하는경우

```jsx
const arr = [1, 2, 3];

const max = Math.max(arr); // NaN
```

Math.max메서드는 매개변수 개수를 확정할 수 없는 가면 인자 함수이다.

다음과 같이 개수가 정해져 있지 않은 여러 개의 숫자를 인수로 전달 받아 인수 중에서 최대 값을 반환한다. 위 예제에서 NaN이 나온이유는 숫자가 아닌 배열자체를 인수로 전달했기 때문이다.

이 같은 문제를 해결하기 위해 배열을 펼쳐서 요소들을 개별적인 값들의 목록으로 만든후 Math.max 메서드의 인수로 전달해야한다.

```jsx
const max = Math.max(...arr); // -> 3
```

기존에 스프레드 문법이 적용되기 전에는 Function.prototype.apply를 사용했다.

```jsx
var arr = [1, 2, 3];

// apply 함수의 2번째 인수(배열)는 apply 함수가 호출하는 함수의 인수 목록이다.
// 따라서 배열이 펼쳐져서 인수로 전달되는 효과가있다.
var max = Math.max.apply(null, arr); -> 3
```

- 스프레드 문법은 전개
- REST 파라미터는 함수에 전달된 인수들의 목록을 배열로 전달 받는다. `(...args)`

## 2. 배열 리터럴 내부에서 사용하는경우

### 2.1 concat

```jsx
var arr = [1, 2].concat([3, 4]);
console.log(arr); // [1 ,2 ,3 ,4]
```

concat → 스프레드 문법사용

```jsx
const arr = [...[1, 2], ...[3, 4]];
console.log(arr); //[1, 2, 3, 4]
```

### 2.2 splice

```jsx
var arr1 = [1, 4];
var arr2 = [2, 3];

// 세 번째 인수 arr2를 해체하여 전달해야 한다.
// 그렇지 않으면 arr1에 arr2 배열 자체가 추가된다.
arr.splice(1, 0, arr2);
// splice(원본배열의 제거를 시작할 인덱스, 제거할갯수, 제거위치에 추가할 요소)

console.log(arr1); // [1, [2, 3], 4]
```

splice → 스프레드 문법사용

```jsx
const arr1 = [1, 4];
const arr2 = [2, 3];

arr.splice(1, 0, ...arr2);
console.log(arr1); // [1, 2, 3, 4]
```

### 2.3 slice를 이용한 배열복사

```jsx
var origin = [1, 2];
var copy = origin.slice();

console.log(copy); // [1, 2]
console.log(copy === origin); // false
```

slice → 스프레드 문법사용

```jsx
const origin = [1, 2];
const copy = [...origin];

console.log(copy); // [1, 2]
console.log(copy === origin); // false
```

### 2.4 이터러블을 배열로 변환

```jsx
function sum() {
  // 이터러블이면서 유사 배열 객체인 arguments를 배열로 변환
  var args = Array.prototype.slice.call(arguments);

  return args.reduce(function (pre, cur) {
    return pre + cur;
  }, 0);
}

console.log(sum(1, 2, 3)); //6
```

스프레드 문법을 이용한 이터러블 → 배열

```jsx
function sum() {
  return [...arguments].reduce((pre, cur) => pre + cur, 0);
}

console.log(sum(1, 2, 3)); //6
```

이터러블이 아닌 유사 배열 객체는 스프레드 문법의 대상이 될수 없다.

이터러블이 아닌 유사 배열 객체를 **배열로 변경하려면 ES6에서 도입된 Array.from메서드를 사용**한다.

```jsx
const arrayLike = {
  0: 1,
  1: 2,
  2: 3,
  length: 3,
};

Array.from(arrayLike); // -> [1, 2, 3]
```

### 3. 객체 리터럴 내부에서 사용하는 경우

스프레드 프로퍼티를 사용하면 객체 리터럴의 프로퍼티 목록에도 스프레드 문법을 사용할 수 있다.

```jsx
// 스프레드 프로퍼티
// 객체복사(얕은 복사)

const obj = {x: 1, y: 2};
const copy = {...obj};

console.log(copy); {x :1, y: 2}
console.log(obj === copy); //false

// 객체 병합
const merged = {x :1, y: 2, ...{a: 3, b: 4}};
console.log(merged)// {x: 1, y: 2, a: 3, b: 4}
```

스프레드 프로퍼티가 제안되기 전에는 ES6에서 도입된 Object.assign 메서드를 사용하여 스프레드 문법을 대신했다.

```jsx
// Object.assign
const merged = Object.assign({}, { x: 1, y: 2 }, { y: 10, z: 3 });
console.log(merged);

// 스프레드 프로퍼티
const merged = { ...{ x: 1, y: 2 }, ...{ y: 10, z: 3 } };
```

2020년 12월 2일
