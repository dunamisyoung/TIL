# 🎈16. 프로퍼티와 어트리뷰트 part arrangement

## 🔎 내부 슬롯과 내부 메서드

**내부슬롯**과 **내부메서드**는 이중대괄호로 이루어져있으며,`[[...]]` 자바스크립트 엔진의 구현 알고리즘을 설명하기 위해 사용하는 의사프로퍼티(pesudo property),메서드(pesudo method)이다.

이는 자바스크립트 엔진에서 실제로 동작하지만 개발자가 직접 접근할수 없는 객체의 프로퍼티이다.
자바스크립트 엔진의 내부 구조이기 떄문에 접근할수 없지만 일부 내부 슬롯과 메서드를 통해 간접적을 접근 할 수 있다.

모든 객체는 `[[Prototype]]`이라는 내부 슬롯을 가지는데 이 `[[Prototype]]` 내부슬롯의 경우 `__proto__`를 통해 간접적을 접근할수 있다.

```javascript
const o = {};

o.__proto__; // Object.prototype
```

## 🔗 프로퍼티 어트리뷰트와 프로퍼티 디스크립터 객체

자바스크립트 엔진은 **객체의 프로퍼티를 생성**하면 **<u>프로퍼티의 상태</u>를 나타내는 프로퍼티 어트리뷰트를 기본값으로 자동 정의**한다.

프로퍼티 상태에는 4가지가 있다. 프로퍼티값(value), 값의 갱신가능 여부(writable), 열거 가능여부(enumerable), 재정의 가능 여부(configurable)를 말한다.

프로퍼티 어트리뷰트는 자바스크립트 엔진이 관리하는 내부 상태값인 내부 슬롯이다.

프로퍼티 어트리뷰트에 간접적인 접근을 할수 있게 도와주는 **Object.getOwnProertyDescriptor** 메서드를 이용하면 된다.

```javascript
const person = {
  name: 'Lee',
};

console.log(Object.getOwnPropertyDescriptor(person, 'name'));
// {value: "Lee", writable: true, enumerable: true, configurable: true}
```

Object.getOwnPropertyDescriptor 메서드 호출시 첫번쨰 매개변수에는 객체의 참조를 전달, 두번쨰에는 프로퍼티 키를 문자열로 전달하면된다. 이렇게하면 <u>프로퍼티 어트리뷰트 정보를 제공</u>하는 **프로퍼티 디스크립터 객체를 반환**한다.

만역 존재하지 않는 프로퍼티나 상속 받은 프로퍼티에대한 디스크립터를 요구하면 **undefined**를 반환한다.

**Object.getOwnPropertyDescriptor** 메서드가 하나의 프로퍼티에 디스크립터 객체를 반환 받았다면,
Object.getOwnPropertyDescriptor**s** 메서드는 모든 프로퍼티의 디스크립터 객체를 반환한다.

**즉, 동적으로 생성된 프로퍼티의 어트리뷰트 정보를 제공하는 프로퍼티 디스크립터 객체도 반환한다.**

```javascript
const person = {
  name: 'Lee',
};

person.age = 20;

console.log(Object.getOwnPropertyDescriptors(person));
//age: {value: 20, writable: true, enumerable: true, configurable: true}
//name: {value: "Lee", writable: true, enumerable: true, configurable: true}
```

## ⛓ 데이터 프로퍼티와 접근자 프로퍼티

프로퍼티는 구분하자면 **데이터 프로퍼티**와 **접근자 프로퍼티**로 나눌수있다.

- ### 🧬 데이터 프로퍼티

  - 키와 값으로 구성된 일반적인 프로퍼티이다.

  - 데이터 프로퍼티는 어트리뷰트를 가진다. 이는 자바스크립트 엔진이 프로퍼티를 생성할때 기본값으로 자동 정의된다.

| 프로퍼티 어트리뷰트 | 프로퍼티 디스크립터 객체의 프로퍼티 | 설명                                                                                                                                                                                                                                               |
| ------------------- | ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `[[Value]]`         | value                               | 프로퍼티 키를 통해 값에 접근하면 반환되는 값입니다.프로퍼티키를 통해 재할당이 이루어진 값을 `[[Value]]`에 재할당 한다. 프로퍼티값이 없으면 프로퍼티를 동적 생성하고 `[[Value]]`에 값을 저장한다.                                                   |
| `[[Writable]]`      | writable                            | 프로퍼티 **값의 변경 여부**를 나타내며 불리언 값을 가집니다. false일때 프로퍼티 `[[Value]]`값이 읽기전용이됩니다.                                                                                                                                  |
| `[[Enumerable]]`    | enumerable                          | 프로퍼티의 **열거 가능여부**를 나타내며 불리언 값을 가집니다. false이면 for....in문 같은 메서드로 열거할 수 없다.                                                                                                                                  |
| `[[configurable]]`  | configurable                        | 프로퍼티의 **재정의 가능 여부**를 나타내며 불리언 값을 가집니다. false 이면 프로퍼티 삭제, 어트리뷰트 값의 변경이 금지 되며, `[[Writable]]` 의 값이 true인 경우에는 `[[Value]]` 의 변경과 `[[Writable]]` 에 한해서 false로 변하는 것은 허용됩니다. |

```javascript
const person = {
  name: 'Lee',
};

person.age = 20;

console.log(Object.getOwnPropertyDescriptor(person, 'name'));
//age: {value: 20, writable: true, enumerable: true, configurable: true}
```

프로퍼티 생성시 `[[Value]]`의 값은 프로퍼티 값으로 초기화 되며 `[[Writable]]`, `[[Enumerable]]`,`[[Configurable]]`의 값은 true로 초기화된다. 프로퍼티 동적추가시에도 동일하다.

- ### 🔬 접근자 프로퍼티

접근자 프로퍼티는 자체적으로 값을 가지지 않고 다른 데이터 프로퍼티 값을 읽거나 저장할때 사용하는 접근자 함수로 구성된 프로퍼티다.

| 프로퍼티 어트리뷰트 | 프로퍼티 디스크립터 객체의 프로퍼티 | 설명                                                                                                                                                           |
| ------------------- | ----------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `[[Get]]`           | get                                 | 접근자 프로퍼티를 통해 **프로퍼티의 값을 읽을떄 호출**되는 접근자 함수다. `[[Get]]`의 값, 즉 getter 함수가 호출되고 그 결과가 프로퍼티 값으로 반환된다.        |
| `[[Set]]`           | set                                 | 접근자 프로퍼티를 통해 데이터 **프로퍼티 값을 저장할때 호출**되는 접근자 함수다. `[[Set]]`의 값, 즉 setter 함수가 호출되고 그 결과가 프로퍼티 값으로 저장된다. |
| `[[Enumerable]]`    | Enumerable                          | 데이터 프로퍼티의 `[[Enumerable]] `과 같다.                                                                                                                    |
| `[[Configurable]]`  | Configurable                        | 데이터 프로퍼티의 `[[Configurable]] `과 같다                                                                                                                   |

접근자함수는 getter/setter 함수라고도 부른다. 접근자 프로퍼티는 getter와 setter 함수를 모두 정의할수 있고, 하나만 정의할 수도있다.

```javascript
const person = {
  //데이터 프로퍼티
  firstName: 'Deo',
  lastName: 'Vi',

  //fullName은 접근자 함수로 구성된 접근자 프로퍼티이다.
  //getter 함수
  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  },
  //setter함수
  set fullName(name) {
    [this.firstName, this.lastName] = name.split('');
  },
};

// 데이터 프로퍼티를 통한 프로퍼티 값의 참조.
console.log(person.fistName + ' ' + person.lastname); // Ungmo Lee

person.fullName = 'Heegun Lee';
console.log(person); // {firstName : 'Heegun', lastName : 'Lee'}
```

person 객체의 firstName과 lastName프로퍼티는 일반적 데이터 프로퍼티이다.
메서드 앞에 get, set이 붙은 메서드들이 getter/setter 함수이고, 함수이름fullName이 접근자 프로퍼티다.

접근자 프로퍼티 값에 접근하면 내부적으로 `[[Get]]` 내부 메서드가 호출되고 다음과 같이 동작한다.

1. 프로퍼티 키가 유요한지 확인한다. 프로퍼티 키는 문자열 또는 심벌이어야한다.
2. <u>프로토타입 체인에서 프로퍼티를 검색</u>한다.
3. 검색된 프로퍼티가 **데이터 프로퍼티인지 접근자프로퍼티인지 확인**한다.
4. 접근자 프로퍼티의 어트리뷰트`[[Get]]`의값, 즉 getter 함수를 호출하여 그 결과를 반환한다.
   프로퍼티 어트리뷰트 `[[Get]]`의 값은 Object.getOwnPropertyDescriptor 메서드가 반환하는 프로퍼티 디스크립터 객체의 get 프로퍼티 값과 같다.

<u>**프로토타입(prototype)**</u>

프로토타입은 어떤 개체의 상위(부모) 객체의 역할을 하는 객체다.
프로토 타입은 **하위(자식) 객체에게 자신의 프로퍼티와 메서드를 상속한다.**
프로토타입 객체의 프로퍼티나 메서드를 상속받은 하위 객체는 **자신의 프로퍼티 또는 메서드인것처럼 자유롭게 사용이 가능**하다.

**프로토 타입체인은 프로토타입이 단방향 링크드 리스트 형태로 연결되어있는 상속 구조를 말한다.** 객체의 프로퍼티나 메서드에 접근하려고 할 때 해당 객체에 접근하려는 프로퍼티 또는 메서드가 없다면 프로토 타입 체인을 따라 프로토타입의 프로퍼티나 메서드를 차례대로 검색한다.

_*나중에 자세하게 배우자!*_

## 📢 프로퍼티 정의

프로퍼티 정의란 새로운 프로퍼티를 추가하면서 **프로퍼티 어트리뷰트를 명시적 정의하거나 기존 프로퍼티의 프로퍼티 어트리뷰트를 재정의하는것을 말한다.**
예를들의 프로퍼티 값의 갱신여부, 열거여부, 재정의여부 등 이것을 명시적으로 나타낼때 사용한다.

**Object.defineProperty** 메서드를 사용하면 프로퍼티의 어트리뷰트를 정의할 수 있으며 **인수로는 객체의 참조 데이터 프로퍼티의 키인 문자열, 프로퍼티 디스크립터 객체를 전달하게된다.**

```javascript
const person = {};

Object.defineProperty(person, 'firstName', {
  value: 'Deo',
  writable: true,
  enumerable: true,
  configurable: true,
});

Object.defineProperty(person, 'lastName', {
  value: 'Vi',
});
```

Object.definedProperty 메서드로 프로퍼티를 정의할때 프로퍼티 디스크립터 객체의 프로퍼티를 일부 생략할 수 있다. 프로퍼티 디스크립터 객체에서 생략된 어트리뷰트는 다음과 같이 기본값이 적용된다.

| 프로퍼티 디스크립터 객체의 프로퍼티 | 대응하는 프로퍼티 어트리뷰트 | 생략했을떄의 기본값 |
| ----------------------------------- | ---------------------------- | ------------------- |
| value                               | `[[Value]]`                  | undefined           |
| get                                 | `[[Get]]`                    | undefined           |
| set                                 | `[[set]]`                    | undefined           |
| writable                            | `[[Writable]]`               | false               |
| enumerable                          | `[[Enumerable]]`             | false               |
| configurable                        | `[[Configurable]]`           | false               |

Object.defineProperty 메서드는 하나의 프로퍼티만 정의할 수 있다.
Object.definePropert**ies** 메서드를 사용하면 여러 개의 프로퍼티를 한 번에 정의할 수 있다.

```javascript
const person = {};

Object.definedProperties(person, {
  firstName: {
    value: 'Deo',
    writable: true,
    enmerable: true,
    configurable: true,
  },
  lastName: {
    value: 'Vi',
    writable: true,
    enmerable: true,
    configurable: true,
  },

  fullName: {
    get() {
      return `${this.firstName} ${this.lastName}`;
    },
    set(name) {
      [this.firstName, this.lastName] = name.split(' ');
    },
    enmerable: true,
    configurable: true,
  },
});

person.fullName = 'tangerine Peanut';
console.log(person); // {firstName : 'tangerine' lastName : 'Peanut'}
```

## 🔒 객체 변경 방지

- ### 🚧객체 확장 금지

- ### 📦객체 밀봉

- ### ❄객체 동결

- ### 💎불변 객체
