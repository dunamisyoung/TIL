# 🎈19. 프로토타입 part arrangement

**자바스크립트는 명령형, 함수형, 프로토타입 기반, 객체지향 프로그래밍을 지원하는 <u>멀티 패러다임 프로그래밍 언어</u>이다.**

**자바스크립트는 객체 기반의 프로그래밍 언어이며 자바스크립트를 이루고 있는 거의 '모든 것'이 객체다.**
원시타입을 제외한 나머지 값들은 모두 객체이다.

## 🔎 객체지향 프로그래밍

객체 지향 프로그래밍은 명령어 또는 함수의 목록으로 보는 전통적인 명령형 프로그래밍을 벗어나 **독립적 단위인 객체의 집합으로 프로그램을 표현하려는 프로그래밍 패러다임을 말한다.**

객체 지향 프로그래밍은 현실 세계의 실체를 프로그래밍에 접목하여 실체의 특징이나 성질을 나타내는 속성을 가지게끔 하여 이를 통해 실체를 인식하고 구별한다.

이름과 주소라는 속성을 갖는 person이라는 객체를 자바스크립트로 표현하면 다음과 같다.

```javascript
// 이름과 주소 속성을 갖는 객체
const person = {
  name: 'Lee',
  address: 'Seoul',
};

console.log(person); // {name : 'Lee', address: "Seoul"}
```

**이처럼 속성을 통해 여러개의 값을 하나의 단위로 구성한 복합적인 자료구조를 객체** 라고 하며 객체지향 프로그래밍이란 **독립적인 객체의 집합으로 프로그램을 표현하려는 프로그래밍 패러다임이다.**

원이라는 걔념을 객체로 만들어보면

```javascript
const circle = {
  radius: 5, // 반지름

  // 원의 지름 : 2r
  getDiameter() {
    return 2 * this.radius;
  },

  // 원의 둘레 : 2πr
  getPerimeter() {
    return 2 * Math.PI * this.radius;
  },

  // 원의 넓이 : πrr
  getArea() {
    return Math.PI * this.radius ** 2;
  },
};

console.log(circle);
// {radiis: 5, getDiamter: f, getPerimeter: f, getArea: f}

console.log(circle.getDimeter()); // 10
console.log(circle.getPerimeter()); // 31.41592653589793
console.log(circle.getArea()); // 78.53981633974483
```

이처럼 객체 지향 프로그램은 **상태(state)를** 나타내는 데이터와 상태 데이터를 조작할수 있는 **동작(behavior)을** 논리적 하나의 단위로 묶어 생각한다.

<u>객체는 상태 데이터와 동작을 하나의 논리적인 단위로 묶은 복합적인 자료구조</u>라 할수있으며,
**객체의 상태는 프로퍼티 동작을 메서드라고 부른다.**

## 👪 상속과 프로토타입

**상속(inheritance)은 객체지향 프로그래밍의 핵심 개념으로, 어떤 객체의 프로퍼티 또는 메서드를 다른 객체가 상속받아 그대로 사용할 수 있는 것을 말한다.**

상속을 통해 불필요한 중복을 제거하며 기존의 코드를 재사용하여 개발비용을 현저히 줄일수 있다.

```javascript
// 생성자 함수
function Circle(radius) {
  this.radius = radius;
  this.getArea = function () {
    // Math.PI는 원주율을 나타내는 싱수다.
    return Math.Pi * this.radius ** 2;
  };
}

// 반지름이 1인 인스턴스 생성
const circle = new Circle(1);
// 반지름이 2인 인스턴스 생성
const circle2 = new Circle(2);

// Circle 생성자 함수는 인스턴스를 생성할 때마다 동일한 동작을 하는
// getArea 메서드를 중복 생성하고 모든 인스턴스가 중복 소유한다.
// getArea 메서드는 하나만 생성하여 모든 인스턴스가 공유해서 사용하는 것이 바람직하다.
console.log(circle1.getArea === circle2.getArea); // false;

console.log(circle1.getArea()); // 3.141592653589793
console.log(circle2.getArea()); // 12.566370614359172
```

생성자 함수는 동일한 프로퍼티(메서드 포함)구조를 갖는 객체를 여러개 생성할때 유용하다.

Circle 생성자 함수가 생성하는 모든 객체(인스턴스)는 radius 프로퍼티와 getArea 메서드를 갖는다. radius 프로퍼티값은 일반적으로 인스턴스마다 다르지만 <u>**getArea 메서드**는 동일한 내용의 메서드를 사용</u>하므로 **단 하나만 생성하여 모든 인스턴스가 공유해서 사용하는 것이 바람직하다.**

하지만 위에 예제는 모든 인스턴스가 메서드를 중복적으로 생성하기에 메모리관점과 퍼포먼스 관점에서 좋지 못하다. 상속을 통해 불필요한 중복을 제거 하면 아래와 같다.

```javascript
// 생성자 함수
function Circle(radius) {
  this.radius = radius;
}

// Circle 생성자 함수가 생성한 모든 인스턴스가 getArea 메서드를
// 공부해서 사용할 수 있도록 프로토타입에 추가한다.
// 프로토타입은 Circle 생성자 함수의 prototype 프로퍼티에 바인딩되어 있다.
Cricle.prototype.getArea = function () {
  return Math.PI * this.radius ** 2;
};

// 인스턴스 생성
const circle = new Circle(1);
const circle = new Circle(2);

// Circle 생성자 함수가 생성한 모든 인스턴스는 부모 객체의 역할을 하는
// 프로토타입 Circle.prototype으로부터 getArea 메서드를 상속받는다.
// 즉, Circle 생성자 함수가 생성하는 모든 인스턴스는 하나의 getArea 메서드를 공유한다.
console.log(circle1.getArea === circle2.getArea); // true

console.log(circle1.getArea()); // 3.141592653589793
console.log(circle2.getArea()); // 12.566370614359172
```

Circle 생성자 함수가 생성한 모든 인스턴스는 자신의 프로토타입, 즉 상위(부모) 객체 역할을 하는 Circle.prototype의 모든 프로퍼티와 메서드를 상속받는다.

getArea 메서드는 단 하나만 생성되어 프로토타입인 Circle.prototype의 메서드로 할당되어있다. 따라서 Circle 생성자 함수가 생성하는 모든 인스턴스는 상속에 의해 getArea 메서드를 사용할수있다.

상속은 코드의 재사용관점에서 매우 유용하며 생성자 함수가 생성할 모든 인스턴스가 공통적으로 사용할 프로퍼티나 메서드를 **프로토타입에 미리구현해 놓으면 생성자 함수를 통해 만들어진 모든 인스턴스는 별도의 구현없이 상위 객체인 프로토타입의 자산을 공유하여 사용**할 수 있다.

## 🎨 프로토타입 객체

프로토타입 객체란 프로그래밍의 근간을 이루는 상속(inheritance)을 구현하기 위해 사용된다.
프로토타입은 어떤 객체의 부모역할을 하는 객체로서 다른 객체에 공유 프로퍼티(메서드 포함)를 제공한다.

**자식객체는 부모객체의 프로퍼티를 자신의 프로퍼티처럼 자유롭게 사용할 수 있다.**

**모든 객체는 `[[Prototype]]`이라는 내부슬롯을 가지며 이 내부 슬롯의 값은 프로토타입의 참조이다.**(null 인경우도 있다.)
`[[Prototype]]`에 저장되는 프로토타입은 객체 생성방식에 의해 결정된다.

예를 들어, 객체 리터럴에 의해 생성된 객체의 프로토타입은 Object.prototype 이고 생성자 함수에 의해 생성된 객체의 프로토타입은 생성자 함수의 prototype 프로퍼티에 바인딩되어있는 객체다.

**모든 객체는 하나의 프로토타입을 가지며. 모든 프로토타입은 생성자 함수와 연결되어있다.**

`[[Prototype]]` 내부 슬롯에는 직접 접근할 수 없지만, 위 그림처럼 `__proto__` 접근자 프로퍼티를 통해 자신의 `[[Prototype]]` 내부 슬롯이 가리키는 프로토타입에 간접적으로 접근할 수 있다.
프로토타입은 자신의 constructor 프로퍼티를 통해 생성자 함수에 접근할 수 있고, 생성자 함수는 자신의 prototype 프로퍼티를 통해 프로토타입에 접근할 수있다.

- ### `__proto__` 접근자 프로퍼티

**모든 객체는 `__proto__` 접근자 프로퍼티를 통해 자신의 프로토타입, 즉`[[Prototype]]` 내부 슬롯에 간접적으로 접근할 수 있다.**

모든 객체는 `__proto__` 접근자 프로퍼티를 통해 프로토타입을 가리키는 `[[Prototye]]` 내부 슬롯에 접근할 수 있다.

👞 **`__proto__`는 접근자 프로퍼티이다.**

**내부슬롯은 프로퍼티가 아니며, 내부슬롯의 값인 프로토타입에 간접적으로 접근할수 있게 해주는 Object.prototype의 접근자 프로퍼티인 `__proto__`를 사용한다.**

이처럼 `__proto__`를 통해 내부슬롯에 **접근하면 내부적으로 `__proto__`의 getter함수인 `get : __proto__()` 가 호출**되고 `__proto__`를 통해 새로운 프로토타입을 **할당하게되면 `__proto__`의 setter 함수인 `set : __proto__()` 가 호출**된다.

👟 **`__proto__` 접근자 프로퍼티는 상속을 통해 사용된다.**

`__proto__` 접근자 프로퍼티는 객체가 직접 소유하는 프로퍼티가 아닌 Object.prototype의 프로퍼티다. 모든 객체는 상속을 통해 `Object.prototype.__proto__` 접근자 프로퍼티를 사용할 수 있다.

```javascript
const person = { name: 'Lee' };

// person 객체는 __proto__ 프로퍼티를 소유하지 않는다.
console.log(person.hasOwnProperty('__proto__')); // false

// __proto__ 프로퍼티는 모든 객체의 프로토타입 객체인 Object.prototype의 접근자 프로퍼티다.
console.log(Object.getOwnPropertyDescriptor(Object.prototype, '__proto__'));
// {get: f, set: f, enumerable : false, configurable: true}

// 모든 객체는 Object.prototype의 접근자 프로퍼티 __proto__를 상속받아 사용 할 수 이싿.
console.log({}.__proto__ === Object.prototype); // true
```

**Object.prototype가 가지고 있는 프로퍼티와 메서드는 모든 객체에게 상속되며, Object.prototype는 프로토타입 체인 최상위에 위치한다.**

🥾 **`__proto__` 접근자 프로퍼티를 통해 프로토타입에 접근하는 이유**

`[[Prototype]]` 내부 슬롯의 값, 즉 프로토타입에 접근하기 위해 접근자 프로퍼티를 사용하는 이유는 상호참조에 의해 프로토타입 체인이 생성되는 것을 방지하기 위해서다.

```javascript
const parent = {};
const child = {};

// child의 프로토타입을 parent로 설정
child.__proto__ = parent;
// parent의 프로토타입을 child로 설정
prrent.__proto__ = child; // TypeError : Cyclic __proto__ value
```

위 예제에서는 parent 객체를 child 객체의 프로토타입으로 설정한후, child 객체를 parent 객체의 프로토타입으로 설정했다. 이러한 코드가 에러를 발생하지 않으면 서로가 자신의 프로토타입이 되는 비정상적 프로토타입 체인이 만들어지기에 `__proto__`접근자 프로퍼티는 에러를 발생시킨다.

만약 그러한 순환 참조하는 프로토타입 체인이 만들어지면 프로토타입 체인에서 프로퍼티 검색시 무한루프에 빠진다. 따라서 아무런 체크없이 무조건적으로 프로토타입을 교체할 수 없도록 `__proto__` 접근자 프로퍼티를 통해 프로토타입에 접근하고 교체하도록 구현되어 있다.

🥿 **`__proto__` 접근자 프로퍼티를 코드 내에서 직접 사용하는 것은 권장하지 않는다.**

모든 객체가 `__proto__`접근자 프로퍼티를 사용하는 것에는 제한이 있다.
아래와 같은 경우 직접 상속을 통해 Object.prototype을 상속받지 않는 객체를 생성할 수도 있기 때문에 `__proto__`를 사용할 수 없는 경우가 있다.

```javascript
// obj는 프로토타입 체인의 종점이다. 따라서 Object.__proto__를 상속받을 수 없다.
const obj = Object.create(null);

// obj는 Object.__proto__를 상속받을 수 없다.
console.log(obj.__proto__); // undefined

// 따라서 Object.getPrototypeOf 메서드를 사용하는 편이 좋다.
console.log(Object.getPrototype(obj)); // null
```

`__proto__` 접근자 프로퍼티 대신 프로토 타입 참조를 취득하고 싶다면 **Objec.getPrototypeOf** 메서드를 사용하고, 프로토타입 교체를 하고 싶다면 **Object.setPrototypeOf** 메서드를 사용하는 것을 권장한다.

```javascript
const obj = {};
const parent = { x: 1 };

// obj 객체의 프로토타입을 취득
Object.getPrototypeOf(obj); // obj.__proto__;
//obj 객체의 프로토타입을 교체
Object.setPrototypeOf(obj, parent); // obj.__proto__ = parent;

console.log(obj.x); // 1
```

Object.getPrototypeOf 메서드와 Object.setPrototypeOf 메서드는 get Object.prototype.**proto**와 set Object.prototype.**proto**의 처리 내용과 정확히 일치한다.

- ### 함수 객체의 prototype 프로퍼티

**함수 객체만이 소유하는 prototype 프로퍼티는 생성자 함수가 생성할 인스턴스의 프로토타입을 가리킨다.**

```javascript
// 함수 객체는 prototype 프로퍼티를 소유한다.
(function () {}.hasOwnProperty('prototype')); // -> true

// 일반 객체는 prototype 프로퍼티를 소유하지 않는다.
({}.hasOwnProperty('prototype')); // -> false
```

**prototype 프로퍼티는 생성자 함수가 생성할 객체(인스턴스)의 프로토타입을 가리킨다.**
따라서 생성자 함수로서 호출할 수 없는 함수, 즉 non-constructor인 화살표 함수와 ES6 메서드 축약표현으로 정의한 메서드는 prototytpe 프로퍼티를 소유하지 않으며 프로토타입도 생성하지 않는다.

```javascript
// 화살표 함수는 non-constructor다.
const Person = (name) => {
  this.name = name;
};

// non-constructor는 prototype 프로퍼티를 소유하지 않는다.
console.log(Person.hasOwnProperty('prototype')); // false

// non-constructor는 프로토타입을 생성하지 않는다.
console.log(Person.prototype); // undefined

// ES6 메서드 축약 표현으로 정의한 메서드는 non-constructor다.
const obj = {
  foo() {},
};

// non-constructor는 prototype 프로퍼티를 소유하지 않는다.
console.log(obj.foo.hasOwnProperty('prototype')); // false

// non-constructor는 프로토타입을 생성하지 않는다.
console.log(obj.foo.prototype); // undefined
```

일반 함수도 prototype 프로퍼티를 소유하지만 객체를 생성하지 않는 일반함수의 prototype 프로퍼티는 의미가없다.

**모든 객체가 가지고 있는 `__proto__`접근자 프로퍼티**와 **함수객체만이 가지고 있는 prototype 프로퍼티**는 결국 <u>동일한 프로토타입객체를 가리킨다.</u>

```javascript
function Person(name) {
  this.name = name;
}

const me = new Person('Lee');

// 결국 Person.prototype과 me.__proto__는 결국 동일한 프로토타입을 가리킨다.
console.log(Person.prototype === me.__proto__); // true
```

- ### 프로토타입의 constructor 프로퍼티와 생성자 함수

**모든 프로토타입 객체는 constructor를 갖는다.**
**constructor 프로퍼티는 prototype 프로퍼티로 자신을 참조하고 있는 생성자 함수를 가리킨다.**

```javascript
// 생성자 함수
function Person(name) {
  this.name = name;
}

const me = new Person('Lee');

// me 객체의 생성자 함수는 Person이다.
// me 는 같은 프로토타입 체인안에 있는 prototye객체의 constuctor를 상속받아 사용할 수 있다.
console.log(me.constructor === Person); // true
```

위 예제에서 Person 생성자 함수는 me 객체를 생성했다.

## 🎭 리터럴 표기법에 의해 생성된 객체의 생성자 함수와 프로토타입

## 🔬프로토타입의 생성 시점

- ### 사용자 정의 생성자 함수와 프로토타입 생성 시점
- ### 빌트인 생성자 함수와 프로토타입 생성 시점

## 🧬 객체 생성 방식과 프로토타입의 결정

- ### 객체 리터럴에 의해 생성된 객체의 프로토타입
- ### Object 생성자 함수에 의해 생성된 객체의 프로토타입
- ### 생성자 함수에 의해 생성된 객체의 프로토타입

## 🔗 프로토타입 체인

## 🕶 오버라이딩과 프로퍼티 섀도잉

## 🎠프로토타입의 교체

- ### 생성자 함수에 의한 프로토타입의 교체
- ### 인스턴스에 의한 프로토타입의 교체

## 🦺 instanceof 연산자

## 🧲 직접 상속

- ### Object.create에 의한 직접 상속

- ### 객체 리터럴 내부에서 **proto**에 의한 직접 상속

## 🚩 정적 프로퍼티/메서드

## 🧷 프로퍼티 존재 확인

- ### in 연산자

- ### Object.prototype.hasOwnProperty 메서드

## 🚄 프로퍼티 열거

- ### for...in 문

- ### Object.keys/values/entries 메서드
