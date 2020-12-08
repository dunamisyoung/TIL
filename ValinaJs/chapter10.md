# 10. 객체 리터럴 part arrangement

## 🔎 객체란?

자바스크립트는 객체 기반의 프로그래밍 언어이다.

원시타입은 변경 불가능한 값 즉, immutable value이다.

하지만 객체는 변경 가능한 값인 mutable value이다.

**객체는 0개 이상의 프로퍼티의 집합**을 말하며 프로퍼티키(key)와 프로퍼티값(value)로 구성되어있다.

```javascript
var person = {
  name: 'Lee',
  age: 20,
};
```

**자바스크립트에서 사용할수 있는 모든 값은, 프로퍼티 값이 될수 있으며**,

프로퍼티값으로 함수가 사용되는것을 일반함수와 구분하기위해서 메서드 라고 한다.

프로퍼티는 객체의 상태를 나타내며 메서드는 프로퍼티를 참조하고 조작할수있는 동작을 뜻한다.

객체는 상태와 동작을 하나의 단위로 구조화 할수 있어서 유용하다.

### 🕶 1. 객체 리터럴을 이용한 객체 생성

자바스크립트에서의 객체 생성방식은 크게 5가지로 분류 할수 있다.

- 객체 리터럴
- Object 생성자 함수
- 생성자 함수
- Object.create 메서드
- 클래스(ES6)

이러한 객체 생성 방식중 가장 간단하고 일반적인방식은 객체리터럴을 이용하는것이다.

```javascript
var person = {
  name: 'Lee',
  sayHello: function () {
    console.log(`Hello! My name is ${this.name}.`);
  },
};

console.log(person); // {name: "Lee", sayHello: f}
```

### 📰 2. 프로퍼티

객체는 프로퍼티키(key)와 프로퍼티값(value)로 이루어진 프로퍼티들의 집합이며, `,`를 이용해 구분한다.

- 프로퍼티 키 : 빈문자열을 포함하는 모든 문자열 또는 심볼 값
- 프로퍼티 값 : 자바스크립트에서 사용할수 있는 모든 값

프로퍼티 키는 일반적으로 문자열로써 `따옴표`를 붙여 표기해야 하지만, 식별자 네이밍 규칙을 준수한다면 `따옴표`를 생략할 수 있다.

- 식별자 네이밍 규칙 - 식별자는 특수문자를 제외한 문자,숫자, 언더스코어`_`, 달러기호`$`를 포함할 수 있으며, 단 특수문자를 제외한 문자, 언더스코어`_`, 달러기호`$` 로 시작해야 한다. 숫자로 시작하는 것은 허용하지 않는다. 또한 예약어는 식별자로 사용할 수 없다.

```javascript
var person, $elem, _name, first_name, val1;
```

**식별자 네이밍 규칙을 따르지 않는 이름에는 반드시 `따옴표`를 사용해야한다.**

프로퍼티 키에 문자열이나 심벌 값 이외의 값을 사용하면 암묵적 타입 변환을 통해 문자열이 된다.

빈문자열을 프로퍼티 키로 사용해도 에러가 발생하지 않지만 '키'로서의 의미를 갖지 못하므로 권장하지 않는다.

문자열로 평가할수 있는 표현식을 사용해 프로퍼티키를 동적으로 생성할수 있다.

```javascript
obj[key] = 'world';
```

### 🧮 3. 메서드

프로퍼티 값이 함수로 사용되는 경우 일반함수와 구분하기 위해 메서드(method)라고 부른다.

```javascript
var circle = {
  radius: 5,

  getDiameter: function () {
    return 2 * this.radius; // this는 circle을 가리킨다.
  },
};

console.log(circle.getDiameter()); //10
```

### 🔐 4. 프로퍼티 접근

- 마침표 프로퍼티 접근 연산자 `.` 마침표 표기법
- 대괄호 프로퍼티 접근 연산자 `[]` 대괄호 표기법

프로퍼티키가 **식별자 네이밍 규칙을 준수하는 이름**이라면 마침표표기법, 대괄호표기법 둘다 사용가능하다.

마침표 표기법, 대괄호표기법의 좌측에는 객체로 평가되는 표현식을 기술한다.

마침표 표기법의 우측또는 대괄호 프로퍼티 내부에는 프로퍼티 키를 지정한다.

대괄호 표기법 내부에 지정하는 프로퍼티 키는 반드시 따옴표로 감싼 문자열 이어야 한다.

객체에 존재하지 않는 프로퍼티에 접근하면 undefined를 반환한다.

### 👓 5. 프로퍼티 값 갱신

이미 존재하는 프로퍼티에 값을 할당하면 프로퍼티 값이 갱신된다.

```javascript
var person = {
  name: 'Lee',
};

person.name = 'kim';

console.log(person); // {name: "Kim"}
```

### 📰 6. 프로퍼티 동적 생성

존재하지 않는 프로퍼티에 값을 할당 하면 프로퍼티가 동적으로 생성되어 프로퍼티값이 할당된다.

```javascript
var person = {
  name: 'Lee',
};

person.age = 20;

console.log(person); // {name: "Lee", age: 20}
```

### 🧮 7. 프로퍼티 삭제

delete 연산자는 객체의 프로퍼티를 삭제한다.

피연산자는 프로퍼티 값에 접근할 수 있는 표현식이어야 한다.

```javascript
var person = {
  name: 'Lee',
};

person.age = 20;

delete person.age;

console.log(person); //{name: 'Lee'}
```

### 🔐 8. ES6 에서 추가된 객체리터럴의 확장기능

ES6에서는 프로퍼티 값으로 변수를 사용하는 경우 변수 이름과 프로퍼티 키가 동일한 이름일때, 프로퍼티 키를 생략할수있다. 프로퍼티 키는 변수 이름으로 자동 생성된다.

```javascript
let x = 1,
  y = 2;

const obj = { x, y };

console.log(obj); // {x: 1, y: 2}
```

### 📌 9. 메서드 축약표현

메서드를 정의 하려면 프로퍼티 값으로 함수를 할당한다.

ES5 >

```javascript
var obj = {
  name: 'Lee',
  sayHi: function () {
    console.log('Hi!' + this.name);
  },
};

obj.sayHi(); // Hi Lee
```

ES6 에서는 메서드를 정의할때 function 키워드를 생략한 축약표현을 사용할 수 있다.

```javascript
const obj = {
  name: 'Lee',
  sayHi() {
    console.log('Hi!' + this.name);
  },
};
```
