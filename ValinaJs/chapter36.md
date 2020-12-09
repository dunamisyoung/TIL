# 🎈36. 디스트럭처링 할당 part arrangement

## 🔎 디스트럭처링 할당이란?

구조화된 배열과 같은 이터러블 또는 객체를 **구조 파괴해 1개 이상의 변수에 개별적으로 할당하는것**을 말하며, 필요한 값만 추출해서 변수에 할당할때 유용하다.

### 🎢 1. 배열 디스트럭처링 할당

ES5에서 구조화된 배열을 디스트럭처링 하여 1개 이상의 변수에 할당하는 방법은 다음과 같다.

```javascript
// ES5
var arr = [1, 2, 3];

var one = arr[0];
var two = arr[1];
var three = arr[2];

console.log(one, two, three); // 1 2 3
```

ES6에서 구조화된 배열을 디스트럭처링 하여 1개 이상의 변수에 할당 할때 배열 디스트럭처링 할당의 대상(할당문의 우변)은 **이터러블** 이어야하며 **할당 기준은 배열의 인덱스다**. - 순서가 중요하다.

```javascript
const arr = [1, 2, 3];

const [one, two, three] = arr;
console.log(one, two, three); // 1 2 3
```

배열 디스트럭처링 할당을 위해서는 할당 연산자 왼쪽에 값을 할당 받을 변수를 선언하는데 이때 **변수를 배열 리터럴 형태로 선언**한다. 이때 우변에 이터러블을 할당하지 않는다면 에러가 발생한다.

```javascript
const [x, y] = [1, 2];
```

배열 디스트럭처링 할당에 있어 변수의 갯수와 이터러블 요소의 갯수가 반드시 일치할 필요는 없으며, 초기값을 설정할수도있다. 하지만 할당받는 값이 우선시 된다.

```javascript
const [a, b] = [1];
console.log(a, b); // 1 undefined

const [c, d, e = 3] = [1, 2];
console.log(c, d, e); // 1 2 3

const [e, f = 10, g = 3] = [1, 2];
console.log(e, f, g); // 1 2 3
```

배열 디스트럭처링 할당을 위한 변수에 Rest 파라미터와 유사하게 **Rest 요소**`...`를 사용할 수 있다. Rest 요소는 Rest 파라미터와 마찬가지로 반드시 마지막에 위치해야한다.

```javascript
//Rest 요소
const [x, ...y] = [1, 2, 3];
console.log(x, y); // 1 [2, 3]
```

### 🚗 2. 객체 디스트럭처링 할당

ES5에서 객체의 각 프로퍼티를 객체로부터 디스트럭처링 하여 변수에 할당하기 위해서는 프로퍼티 키를 사용해야 한다.

```javascript
var user = { firstName: 'Youngsang', lastName: 'Lee' };

var firstName = user.firstName;
var lastName = user.lastName;

console.log(firstName, lastName); // youngsang Lee
```

ES6의 객체 디스트럭처링 할당은 객체의 각프로퍼티를 객체로 부터 추출하여 1개 이상의 변수에 할당한다. **할당 기준은 프로퍼티 키며, 순서는 의미가 없다**. 선언된 변수이름과 프로퍼티키가 일치한다면 할당된다.

```javascript
const user = { firstName: 'Youngsang', lastName: 'Lee' };

const { lastName, firstName } = user;
console.log(firstName, lastName); // Youngsang Lee
```

객체 디스트럭처링 할당을 위해서는 할당 연산자 왼쪽에 프로퍼티 값을 할당받을 변수를 선언해야 하는데 이때 **변수를 객체리터럴 형태로 선언**한다. 이때 우변에 객체로 평가될수 있는 표현식을 할당하지 않으면 에러가 발생한다.

```javascript
// 프로퍼티 축약표현
// 위와 아래는 동치다.
const { lastName, firstName } = user;
const { lastName: lastName, firstname: firstName } = user;
```

객체의 프로퍼티 키와 다른 변수 이름으로 프로퍼티 값을 할당 받으려면 다음과 같이 변수를 선언한다.

```javascript
const user = { firstName: 'Youngsang', lastName : 'Lee' };

// 프로퍼티 키에 따른 프로퍼티 값으로 또다른 프로퍼티 키를 전달.
// 결국 전달된 프로퍼티 키를 따라가보면 위에서 전달한 값이 나오게된다.
const { lastName : ln, firstName: fn } = user;

console.log(fn, ln}; //  Youngsang Lee
```

객체 디스트 럭처링 할당시에도 변수에 기본값을 설정할수 있으며, 할당된 값이 기본값보다 우선시 된다.

```javascript
const user = ({ firstName: 'Youngsang', lastName } = { lastName: 'Lee' });
console.log(firstName, lastName); // Youngsang Lee

const user = ({ firstName: fn = 'Youngsang', lastName: ln } = { lastName: 'Lee' });
console.log(fn, ln); // Youngsang Lee
```

객체 디스트럭처링 할당은 객체를 인수로 전달받는 함수의 매개변수에도 사용할 수 있다.

```javascript
function printTodo(todo) {
  console.log(`할일 ${todo.content}은 ${todo.completed ? '완료' : '비완료'} 상태입니다.`);
}

printTodo({ id: 1, content: 'HTML', completed: true });
// 할일 HTML은 완료 상태입니다.
```

매개변수 todo에 객체 디스트 럭처링 할당을 사용하면 조금더 가독성 좋게 표현할 수 있다.

```javascript
function printTodo({ content, completed }) {
  console.log(`할일 ${content}은 ${completed ? '완료' : '비완료'} 상태입니다.`);
}

printTodo({ id: 1, content: 'HTML', completed: true });
// 할일 HTML은 완료 상태입니다.
```

위 코드는 인수로 넘겨주는 객체를 받아서 객체디스트럭처링 할당까지 진행했다.

### 👓 3. 배열 요소가 객체인경우

**배열요소가 객체라면 배열 디스트럭처링 할당과 객체 디스트럭처링 할당을 혼용할수 있다.**

```javascript
const todos = [
  { id: 1, content: 'HTML', completed: true },
  { id: 2, content: 'CSS', completed: false },
  { id: 3, content: 'JS', completed: false },
];

const [, { id }] = todos;
console.log(id); // 2
// todos 배열의 2번째 인덱스 값안에 있는 id프로퍼티키의 값을 가져왔다.
```

### 🧱 4. 중첩객체에서의 객체디스트럭처링

중첩 객체의 경우는 다음과 같이 사용할수 있다.

```javascript
const user = {
  name: 'Lee',
  address: {
    zipCode: '03068',
    city: 'Seoul',
  },
};

const {
  address: { city },
} = user;
console.log(city); // 'Seoul'
// user프로퍼티 키-> 객체추출 -> address객체의 프로퍼티키 -> 값추출
```

### 🧮 5. Rest 요소와 Rest 프로퍼티

Rest요소에서 요소는 배열리터럴 안에 위치하는 값형태인 **요소를 의미**하며,

Rest프로퍼티 에서 프로퍼티는 객체리터럴 안에 위치하는 값형태인 **프로퍼티를 의미**한다.

객체 디스트럭처링 할당을 위한 변수에 **Rest 요소(Rest element)** `const [ x, ...y ] = [1, 2, 3] // 1 [2, 3]` 와 유사하게 **Rest 프로퍼티(Rest property)** `const { x, ...y } = {1, 2, 3} // 1 {2, 3}` 를 사용할 수 있다.

```javascript
//Rest 프로퍼티
const { x, ...rest } = { x: 1, y: 2, z: 3 };
console.log(x, rest); // 1{ y: 2, z: 3}
```
