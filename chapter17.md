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

- ### 💡 생성자 함수에 의한 객체 생성 방식의 장점

- ### 🔬 생성자 함수에 인스턴스 생성 과정

- ### 🎳 내부 메서드 `[[Call]]` 과 `[[Construct]]`

- ### 🎭 constructor와 non-constructor의 구분

- ### 🔮 new 연산자

- ### 🥏 newtarget
