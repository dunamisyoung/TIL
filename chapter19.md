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

- ### `__proto__` 접근자 프로퍼티
- ### 함수 객체의 prototype 프로포터티
- ### 프로토타입의 constructor 프로퍼티와 생성자 함수

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
