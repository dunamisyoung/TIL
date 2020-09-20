# 🎈17. 생성자 함수에 의한 객체 생성 part arrangement

객체 리터럴에 의한 객체 생성 방식은 가장 일반적이며 간단한 객체 생성 방식이었다.
객체 생성에는 객체 리터럴 말고 다양한 방법으로 객체 생성이 가능한데 이번에는 **생성자 함수를 이용한 객체 생성방식 및 그에따른 장단점을 살펴보자.**

## 🔎 Object 생성자 함수

**new 연산자와 함께 Object 생성자 함수를 호출하면 빈 객체를 생성하여 반환한다.**
빈 객체 생성이후 프로퍼티 또는 메서드를 추가하여 객체를 완성할 수 있다.

```javascript
const person = new Object();

person.name = 'Vi';
person.sayHello = function () {
  console.log('Hi! My name is' + this.name);
};

console.log(person); // {naem : 'Vi', sayHello : f}
person.sayHello(); // H! My name is Vi
```

**생성자 함수(constructor)란 new 연산자와 함께 호출하여 객체(인스턴스)를 생성하는 함수를 말한다.** 여기서 생성자 함수에 의해서 생성된 객체를 <u>인스턴스(instance)</u>라고 한다.

자바스크립트는 Object 생성자 함수 이외에도 **String, Number, Boolean, Function, Array,Date, RegExp, Promise** 등의 <u>빌트인 생성자 함수를 제공</u>한다.

```javascript
// Function 생성자 함수에 의한 Function 객체(함수) 생성
const func = new Function('x', 'return x * x');
console.log(typeof func); // function

//  Array 생성자 함수에 의한 Array 객체(배열) 생성
const arr = new Array(1, 2, 3);
console.log(typeof arr); // object
console.log(arr); // [1,2,3]

// RegExp 생성자 함수에 의한 RegExp 객체(정규 표현식) 생성
const regExp = new RegExp(/ab+c/i);
console.log(typeof regExp); // object
console.log(regExp); // /ab+c/i

//Date 생성자 함수에 의한 Date 객체 생성
const date = new Date();
console.log(typeof date); // object
console.log(date); // Sun Sep 20 2020 16:01:01 GMT+0900 (대한민국 표준시)
```

반드시 Object 생성자 함수를 사용해서 빈객체를 생성해야 하는것은아니고, 특별한 이유가없다면 유용하지 않을수있다. 일반적인 생성방식인 객체리터럴을 이용하는것이 어떨까?

## 👓 생성자 함수

- ### 🦺 객체 리터럴에 의한 객체 생성 방식의 문제점

객체 리터럴에 의한 객체 생성 방식은 직관적이며 간편하다.
하지만 **객체리터럴에 의한 생성 방식은 <u>단하나의 객체만 생성</u>하기에 동일한 프로퍼티를 갖는 객체를 여러개 생성해야 하는경우 중복해서 기술해야하기에 비효율적이다.**

```javascript
const circle1 = {
  radius: 5,
  getDiameter() {
    return 2 * this.radius;
  },
};
console.log(circle1.getDiameter());

const circle2 = {
  radius : 10,
  getDiameter(){
    return * this.radius
  }
}

console.log(circle2.getDimeter())
```

**객체는 프로퍼티를 통해 고유의 상태(state)를 표현한다.**
**메서드를 통해 상태 데이터인 프로퍼티를 참조하고 조작하는 동작(behavior)을 표현한다.**
따라서 프로퍼티는 객체마다 프로퍼티 값이 다를수 있지만 메서드는 내용이 동일한 경우가 일반적이다.

원을 표현한 객체인 circle1 객체와 circle2 객체는 프로퍼티 구조가 동일하다.
radius 프로퍼티 값은 객체마다 다를 수 있지만 getDiameter 메서드는 완전히 동일하다.

**객체리터럴로 객체를 생성하면 단 하나의 객체를 생성하기에 매번 같은 프로퍼티와 메서드를 기술해야한다. 그렇기에 여러 객체를 생성해야한다면 비효율적이다.** 라고 말할수 있다.

- ### 💡 생성자 함수에 의한 객체 생성 방식의 장점

생성자 함수에 의한 객체 생성 방식은 마치 객체(인스턴스)를 생성하기위한 템플릿(클래스)처럼 생성자 함수를 사용하여 프로퍼티 구조가 동일한 객체 여러개를 간편하게 생성할 수 있다.

```javascript
// 생성자 함수
function Circle(radius) {
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}

// 인스턴스의 생성
const circle1 = new Circle(5); // 반지름이 5인 Circle 객체 생성
const circle2 = new Circle(10); // 반지름이 10인 Circle 객체 생성

console.log(circle1.getDimeter()); //10
console.log(circle.getDimeter()); //20
```

this는 객체 자신의 프로퍼티나 메서드를 참조하기 위한 자기 참조 변수다. **this가 가리키는 값, 즉 this 바인딩은 함수 호출 방식에 따라 동적으로 결정된다.**

| 함수 호출 방식       | this가 가리키는 값(this 바인딩)        |
| -------------------- | -------------------------------------- |
| 일반 함수로서 호출   | 전역 객체                              |
| 메서드로서 호출      | 메서드를 호출한 객체(마침표 앞의 객체) |
| 생성자 함수로서 호출 | 생성자 함수가 (미래에) 생성할 인스턴스 |

```javascript
function deo() {
  console.log(this);
}

// 함수객체 호출
deo(); // window

// 메서드로서 호출
const obj = { foo };
obj.foo(); // obj

// 생성자 함수로 호출
const vi = new deo(); // vi
```

**생성자 함수는 객체(인스턴스)를 생성하는 함수이다.**
일반 함수와 동일한 방법으로 생성자 함수를 정의하고 **new 연산자와 함께 호출하면 해당 함수는 생성자 함수로 동작한다.** 만약 <u>new 연산자와 함께 생성자 함수를 호출하지 않으면 일반함수로 동작</u>하게 된다.

- ### 🔬 생성자 함수에 인스턴스 생성 과정

생성자 함수의 함수 몸체에서 수행해야 하는것은 **프로퍼티 구조가 동일한 인스턴스를 생성하기 위한 탬플릿 으로 동작하여 인스턴스를 생성하고 생성된 인스턴스를 초기화 하는것이다.**
생성자 함수가 인스턴스를 생성하는 것은 필수이며, 생성된 인스턴스를 초기화 하는것은 옵션이다.

```javascript
// 생성자 함수
function Circle(radius) {
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}

// 인스턴스 생성
const circle1 = new Circle(5); // 반지름이 5인 Circle 객체를 생성
```

생성자 함수 내부의 코드를 살펴보면 this에 프로퍼티를 추가하고 필요에 따라 전달된 인수를 프로퍼티 초기값으로서 할당하여 인스턴스를 초기화한다. 하지만 인스턴스를 생성하고 반환한 코드는 보이지 않는다.

자바스크립트 엔진은 암묵적인 처리를 통해 인스턴스를 생성후 반환한다.** new 연산자와 함께 호출 하면 다음과 같은 과정을 거쳐 인스턴스 생성후 초기화 그리고 인스턴스를 암묵적으로 반환한다.**

- #### 1. 인스턴스 생성과 this 바인딩

  new 연산자와 함께 생성자 함수를 호출하면 암묵적으로 빈객체가 생성되는데 이것이 생성자 함수가 만들어낸 인스턴스(객체)이다. 이렇게 **암묵적으로 생성된 빈객체는 this에 바인딩되며, 런타임 이전에 실행된다.**

  **바인딩(binding)**
  여기서 <u>바인딩이란 식별자와 값을 연결하는 과정을 의미</u>한다.
  변수 선언은 변수이름과 확보된 메모리 공간의 주소를 바인딩 하는것이고, 위에서 살펴본 this 바인딩은 this와 this가 가리킬 객체를 바인딩하는것이다.

  ```javascript
  function Circle(radius) {
    // 1. 암묵적으로 빈 객체가 생성되고 this에 바인딩
    console.log(this);

    this.radius = radius;
    this.getDiameter = function () {
      return 2 * this.radius;
    };
  }
  ```

- #### 2. 인스턴스 초기화

  **생성자 함수에 기술되어 있는 코드가 실행되어 this에 바인딩 되어있는 인스턴스를 초기화한다.**
  개발자가 this에 바인딩 되어있는 인스턴스에 프로퍼티나 메서드를 추가하고 생성자 함수가 인수로 전달 받은 초기값을 인스턴스 프로퍼티에 할당하여 초기화 하거나 고정값을 할당한다.

  ```javascript
  function Circle(radius) {
    // 1. 암묵적으로 빈 객체가 생성되고 this에 바인딩
    console.log(this);

    // 2. this에 바인딩되어있는 인스턴스를 초기화한다.
    this.radius = radius;
    this.getDiameter = function () {
      return 2 * this.radius;
    };
  }
  ```

- #### 3. 인스턴스 반환

  생성자 함수의 내부 처리가 끝나면 완성된 인스턴스(객체)가 바인딩된 this가 암묵적으로 반환한다.

  ```javascript
  function Circle(radius) {
    // 1. 암묵적으로 빈 객체가 생성되고 this에 바인딩
    console.log(this);

    // 2. this에 바인딩되어있는 인스턴스를 초기화한다.
    this.radius = radius;
    this.getDiameter = function () {
      return 2 * this.radius;
    };

    // 3. 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환 된다.
    // 아마두 이처리는 함수내에 있는 암묵적return이 반환해주는것이지 않을까?
  }

  // 인스턴스 생성 Circle 생성자 함수는 함묵적으로 this를 반환한다.
  cosnt circle = new Circle(10);
  console.log(circle); // Circle {radius : 10, getDimeter: f}
  ```

  만약 this가 아닌 다른객체를 <u>명시적으로 반환하면 this가 반환되지 못하고 return 문에 명시된 객체가 반환</u>된다 즉, this가 아닌 다른 값을 반환하는것은 **생성자 함수의 기본동작을 훼손하기에 생성자 함수내부에서는 반드시 return 문을 생략해야한다.**

- ### 🎳 내부 메서드 `[[Call]]` 과 `[[Construct]]`

- ### 🎭 constructor와 non-constructor의 구분

- ### 🔮 new 연산자

- ### 🥏 newtarget
