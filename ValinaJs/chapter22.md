# 🎈22. This part arrangement

## 🔎 1. this 키워드

this는 자기참조 변수로써 자신이 속한 객체나 자신이 생성할 인스턴스를 가리키는 식별자를 가리킨다.

this는 자바스크립트 엔진에 의해 암묵적으로 생성되며 코드 어디서든 참조할 있다.

ES6 이전에 함수를 호출하면 암묵적으로 arguments 객체와 this가 함수 내부에 전달된다.

함수 내부에서 arguments 객체를 지역 변수처럼 사용할 수 있는 것처럼 this도 지역 변수처럼 사용할 수 있다. 단, this가 가리키는 값, 즉 this 바인딩은 **함수 호출방식에 의해 동적으로 결정**된다.

바인딩은 식별자와 값을 연결하는 과정을 의미하며 예를 들어 변수 선언은 변수이름과 확보된 메모리 공간의 주소를 바인딩 하는것이다.

### 👪 2. 함수 호출 방식과 this 바인딩

렉시컬 스코프는 함수 정의가 평가되어 함수 객체가 생성되는 시점에 상위 스코프를 결정하지만, this 바인딩은 함수 호출시점에 결정된다.

함수 호출방식

1. 일반 함수 호출
2. 메서드 호출
3. 생성자 함수 호출
4. Function.prototype.apply/call/bind 메서드에 의한 간접호출

```javascript
const foo = function () {
  console.log(this);
};
foo(); // window - 일반함수 호출의 this는 전역객체를 가르킨다.

const obj = { foo };
obj.foo(); // obj - 메서드 호출의 this는 메서드를 호출한 객체를 가리킨다.

new foo(); // foo {} - foo 함수 내부의 this는 함수가 생성한 인스턴스를 가리킨다.

const bar = { name: 'bar' }; // call | apply | bind 메서드에 의한 간접호출에 this는 내부로 전달한 인수에 의해서 결정된다.

foo.call(bar); // bar - 호출과 함께 this 바인딩 까지 전달
foo.apply(bar); // bar - 호출과 함께 this 바인딩 까지 전달
foo.bind(bar)(); // bar - this바인딩만 해주기에 호출은 따로 한번더 명시적으로 해줘야함
```

### 🎨 2.1 일반 함수 호출

기본적으로 this에는 전역객체가 바인딩된다.

전역함수는 물론, 중첩 함수에서도 일반함수로 호출하면 함수 내부의 this에는 전역객체가 바인딩된다. 다만 strict mode가 적용된 일반 함수 내부의 this 에는 undefined가 바인딩된다.

**콜백 함수가 일반 함수로 호출된다면 콜백함수 내부의 this애도 전역 객체가 바인딩된다.**

**어떠한 함수라도 일반 함수로 호출되면 this에 전역 객체가 바인딩된다.**

메서드 내에서 정의한 중첩함수 또는 메서드에게 전달한 콜백 함수(보조 함수)가 일반 함수로 호출될때 메서드 내의 중첩 함수 또는 콜백 함수의 this가 전역 객체를 바인딩 하는 것은 문제가 있다.

메서드 내부에 콜백 함수의 this 바인딩을 메서드의 this 바인딩과 일치 시키기위한 방법은 다음과 같다.

```javascript
var value = 1;

const obj = {
  value: 100,
  foo() {
    const that = this;

    setTimeout(function () {
      console.log(that.value);
    }, 100);
  },
};

obj.foo();
```

위 방법 이외에 자바스크립트는 this를 명시적으로 바인딩 할 수 있는 **Function.prototype.apply, Function.prototype.call, Function.prototype.bind** 메서드를 제공한다.

```javascript
var value = 1;

const obj = {
  value: 100,
  foo() {
    setTimeout(
      function () {
        console.log(this.value);
      }.bind(this),
      100
    );
  },
};

obj.foo();
```

위 보다 간결하게 화살표 함수를 사용해서 this 바인딩을 일치시킬 수도 있다.

```javascript
var value = 1;

const obj = {
  value: 100,
  foo() {
    setTimeout(() => console.log(this.value), 100);
  },
};

obj.foo();
```

### 👞 2.2 메서드 호출

메서드 내부의 this에는 마침표 앞에 기술한 객체가 바인딩된다.

메서드 내부의 this는 메서드를 소유한 객체가 아닌 메서드를 호출한 객체에 바인딩된다.

### 👟 2.3 생성자 함수 호출

**생성자 함수 내부의 this에는 생성자 함수가 (미래에) 생성할 인스턴스가 바인딩된다.**

```javascript
function Circle(radius) {
  this.radius = radius; // this는 자신을 호출한 객체 Circle을 가리킨다.
  this.getDiameter = function () {
    return 2 * this.radius;
  };
}

const circle1 = new Circle(5);
const circle2 = new Circle(10);

console.log(circle1.getDimeter()); // 10
console.log(circle2.getDimeter()); // 20
```

### 🥾 2.4 Function.prototype.apply/call/bind 메서드에 의한 간접 호출

apply, call, bind 메서드는 Function.prototype의 메서드로 모든함수가 상속받아 사용할수 있다.

this로 사용할 객체와 인수 리스트를 인수로 전달받아 함수를 호출한다.

- Function.prototype.apply(thisArg[, argsArray]);

  apply 메서드는 호출할 함수의 인수를 배열로 묶어전달.

- Function.prototype.call(thisArg[, arg1[,arg2[, ...]]])

  call 메서드는 호출할 함수의 인수를 쉼표로 구분한 리스트 형식으로 전달

**apply**와 **call** 메서드의 용도는 유사배열 객체에 배열메서드를 사용하는 경우이다.

- **bind** 메서드는 메서드의 this와 메서드 내부의 중첩 함수 또는 콜백 함수의 this가 불일치 하는 문제를 해결하기 위해 사용한다.

```javascript
const person = {
	name : 'Lee',
	foo(callback) {
		setTimeout(callback.bind(this), 100);
	}
};

person.foo(function(){
	console.log(`Hi! my name is ${this.name}.`); // Hi! my name is Lee.
}
```
