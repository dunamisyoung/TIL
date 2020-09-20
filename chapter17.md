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

함수 선언문 또는 함수 표현식으로 정의한 함수는 일반적인 함수로 호출할수 있으며 또한 생성자 함수로도 호출이 가능하다. 즉, 생성자 함수로 호출한다는것은 new 연산자와 함께 호출하여 객체를 생성한다는 것을 의미한다.

함수는 일급객체이지만 일반객체와 동일하게 동작할 수 있다. 함수객체는 일반 객체가 가지고 있는 내부 슬롯과 내부 메서드를 모두 가지고 있기때문이다.

```javascript
function deo() {}

deo.prop = 10;

deo.method = function () {
  console.log(this.prop);
};

deo.method(); // 10
```

함수는 객체이지만 일반 객체와는 다르다. 일반 객체는 호출할 수없지만 함수는 호출할 수 있다.
따라서 함수객체는 일반 객체가 가지고 있는 내부 슬롯()과 내부메서드, 함수 객체만을 위한 `[[Environment]]`,`[[FormalParameters]]` 등의 내부슬롯과 `[[Call]]`, `[[Construct]]` 같은 내부 메서드를 추가로 가지고 있다.

함수가 **일반 함수로서 호출되면 함수 객체의 내부 메서드 `[[Call]]`이 호출**되고 new 연산자와 함께 함께 생성자 함수로 호출되면 `[[Construct]]`가 호출된다.

```javascript
function deo() {}

// 일반적인 함수로서 호출 : [[Call]]이 호출된다
deo();

// 생성자 함수로서 호출: [[Construct]]가 호출된다.
new deo();
```

내부 메서드 `[[Call]]`을 가지는 함수 객체를 callable 이라고 하며, 내부 메서드 `[[Construct]]`를 갖는 함수 객체를 constructor, `[[Construct]]`를 갖지 않는 함수 객체를 non-consstructor라고 부른다. **callable은 호출할수 있는 객체, 즉 함수**를 말하며, **constructor는 생성자 함수로서 호출할수 있는 함수**, **non-constructor는 객체를 생성자 함수로서 호출할수 없는 함수를 의미**한다.

호출할 수 없는 객체는 함수객체가 아니므로 함수로서 기능하는 객체는 반드시 callable 이어야한다.
모든 함수객체는 내부메서드로 `[[Call]]`을 가지고 있으므로 호출할수 있지만, 모든 함수 객체가`[[Construct]]`를 가지는것은 아니다.

**즉, 모든 함수객체는 호출할수있지만 모든 함수객체를 생성자 함수로서 호출할 수있는것은 아니다.**

- ### 🎭 constructor와 non-constructor의 구분

자바스크립트 엔진의 constructor와 non-constructor 구별은 함수정의를 평가하여 함수객체를 생성할때 함수 정의방식에 따라 나누어진다.

- constructor : 함수 선언문, 함수 표현식, 클래스(클래스도 함수! 나중에 자세히 보자)
- non-constructor : 메서드, 화살표 함수

이때 주의할 것은 ECMAScript 사양에서 메서드로 인정하는 범위가 일반적인 의미의 메서드 보다 좁다는 것이다.

```javascript
//일반 함수에는 - 함수 선언문 , 함수 표현식이있다.
function deo() {} // 함수 선언문

const vi = function () {}; //함수표현식

// 프로퍼티 x값으로 할당된 것은 일반 함수로 정의된 함수이다. 이는 메서드로 인정하지 않는다.
const tangerine = {
  x: function () {},
};

// 일반 함수로 정의된 함수만이 constructor이다.
new deo();
new vi();
new tangerine.x();

const arrow = () => {};
new arrow(); //TypeError : arrow is not a constructor
```

함수를 프로퍼티 값으로 사용하면 일반적으로 메서드로 통칭한다.하지만 Ecmascript 사양에서는 ES6의 메서드 축약표현만을 의미한다고 되어있다.
다시말해 함수가 어디에 할당되어 있는지를 판단하는 것이 아니라 **함수 정의 방식에 따라 constructor와 non-constructor를 구분한다.**

위 예제와 같이 일반함수 즉, **함수 선언문과 함수 표현식으로 정의된 함수만이 constructor**이고 ES6 의 **화살표 함수와 메서드 축약표현으로 정의된 함수는 non-constructor다.**

함수를 일반 함수로서 호출하면 함수 객체의 내부 메서드 `[[Call]]`이 호출되고 new연산자와 함께 생성자 함수로 호출하면 `[[Constructor]]`가 호출된다.

```javascript
function deo() {}

//일반 함수로서 호출
deo();

// 생성자 함수로서 호출
new deo();
```

주의할것은 생성자 함수로서 호출되기를 기대하고 **정의하지 않은 일반함수에 new 연산자를 붙여 호출하면 생성자 함수로 동작할수 있다는것이다.**

- ### 🔮 new 연산자

일반함수와 생성자 함수에 특별한 형식적 차이는 없다. **new 연산자와 함께 함수를 호출하면 해당함수는 생성자 함수로 동작하게된다.**

다시말해 함수 객체내부 메서드`[[Call]]`이 호출되는것이아니라 `[[Constructor]]`가 호출된다. 단, new연산자와 함께 호출하는 함수는 non-constructor가 아닌 constructor 이어야한다.

```javascript
// 생성자 함수가 아닌 일반함수로 정의
function add(x, y) {
  return x + y;
}

// 생성자 함수로써 정의하지않은 일반 함수를 new 연산자와 함께 호출
let inst = new add();
// 함수가 객체를 반환하지 않았으므로 반환문이 무시된다.
console.log(inst); // {}

// 객체를 반환하는 일반 함수
function createUser(name, role) {
  return { name, role };
}

// 생성자 함수로서 정의하지 않은 일반 함수를 new 연산자와 함께 호출
inst = new createUser('Lee', 'admin');

//함수가 생성한 객체를 반환한다.
console.log(inst); // {name : 'Lee', role : 'admin'}
```

반대로 new 연산자 없이 생성자 함수를 호출하면 일반 함수로 호출된다. 다시말해 함수 객체의 내부 메서드`[[Constructor]]`가 호출되는 것이 아니라 `[[Call]]`이 호출된다.

```javascript
// 생성자 함수
function Circle(radius) {
  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}

// new 연산자 없이 생성자 함수를 호출하면 일반 함수로서 호출된다.
const circle = Circle(5);
console.log(circle); // undefined

// 일반 함수 내부의 this는 전역 객체 window를 가르킨다.
console.log(radius); // 5
console.log(getDiameter); // 10

circle.getDiameter();
// TypeError: Cannot read property 'getDiameter' of undefined
```

위에서 보여지는 Circle 함수를 new 연산자와 함께 생성자 함수로써 호출하면 내부의 this는 Circle 생성자 함수가 생성할 인스턴스를 가리킨다. 하지만 **Circle 함수를 일반 함수로 호출하게되면 함수 내부의 this는 전역 객체 window를 가르킨다. 따라서 radius 프로퍼티와 getDiameter 메서드는 전역 객체의 프로퍼티가 된다.**

일반함수와 생성자 함수에는 특별한 형식적 차이느 없지만 생성자 함수를 표기할때는 첫문자를 대문자로 기술하는 파스칼케이스로 명명하여 일반 함수와 구별하도록하자!

- ### 🥏 newtarget

생성자 함수가 new 연산자 없이 호출되는 것을 방지하기 위해서 Es6에서는 new.target을 지원한다.

new.target은 this와 유사하게 constructor인 모든 함수 내부에서 암묵적인 지역변수와 같이 사용되며 메타 프로퍼티라고 불리운다. 익스플로러(IE) 는 new.target을 지원하지 않기에 주의하도록하자.

함수의 내부에서 new.target을 사용하게되면 new 연산자와 함께 생성자 함수로 호출되었는지 확인할수있다.

**new 연산자와 함께 생성자 함수로서 호출되면 함수 내부의 new.target은 함수 자신을 가리킨다. new 연산자 없이 일반함수로 호출된 함수 내부의 new.target은 undedifined이다.**

함수 내부에서 new.target을 사용하여 new연산자와 생성자 함수로서 호출했는지 확인해서 그렇지 않은 경우 재귀 호출을 통해 생성자 함수로서 호출할 수 있다.

```javascript
function Circle(radius) {
  if (!new.target) {
    // 생성자 함수로 호출하지 않았다면 재귀 호출을 통해 생성된 객체(인스턴스)를 반환하도록한다.
    return new Circle(radius);
  }

  this.radius = radius;
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}

const circle = Circle(5);
console.log(circle.getDiameter());
```

**new 연산자와 함께 생성자 함수에 의해 생성된 객체(인스턴스)는 프로토타입에 의해 생성자 함수와 연결된다.** 이를 통해 new 연산자와 함께 호출되어있는지 확인할수 있다.

참고로 대부분의 빌트인 생성자 함수(Object, String, Number, Boolean, Function, Array, Date, RegExp, Promise)는 new 연산자와 함께 호출되었는지 확인후 적절한 값을 반환한다.

**예를 들어 Object와 Function 생성자 함수는 new 연산자 없이 호출시에도 new 연산자와 호출했을때 와 동일하게 동작하게된다.**

```javascript
let obj = new Object();
console.log(obj); // {}

obj = Object();
console.log(obj); // {}

let f = new Function('x' 'return x ** x');
console.log(f); // f anoynmous(x) {return x ** x}

f = Function('x' 'return x ** x');
console.log(f); // f anoynmous(x) {return x ** x}
```
