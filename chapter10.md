# 🎈10. 객체 리터럴 part arrangement

## 🔎 객체란?

자바스크립트는 객체기반의 프로그래밍 언어이면서 이를 구성하는 거의 모든것이 객체이다.
원시값을 제외한 나머지 값들(함수, 배열, 정규표현식등..)이라고 할수있다.

**원시타입의 값은 불변값**(immutable value)이지만 **객체타입의 값은 변경가능한값**(mutable value)이다.

**객체는 0개이상의 프로퍼티로 구성된 집합이며 프로퍼티 키와 값으로 구성된다.**

프로퍼티 값으로는 모든 값이올수 있다.
함수는 일급 객체이므로 값으로 취급할수 있으며, 프로퍼티 값으로 사용할수있다. **프로퍼티값이 함수일경우에는 일반함수와 구분하기위해서 메서드라고 한다.**

**프로퍼티 : 객체의 상태를 나타내는값**
**메서드 : 프로퍼티를 참조하고 조작할수 있는 동작**

## 💡 객체 리터럴에 의한 객체 생성

자바스크립트에서 객체를 만드는 방법은 여러가지가 있다.

- 객체리터럴
- Object 생성자함수
- 생성자 함수
- Object.create 메서드
- 클래스(ES6)

일단 객체리터럴을 이용해서 객체를 생성하는 방법부터 알아보자.
리터럴의 정의를 다시한번 살펴보면, 사람이 이해할 수 있는 문자 또는 약속된 기호를 사용하여 값을 생성하는 표기법을 말하는데.

객체리터럴은 객체를 생성하기위한 방법이다.
`{...}`중괄호 안에 0개이상의 프로퍼티를 정의하면된다.
자바스크립트는 코드의 문맥을 읽기 때문에 `{}`만 입력하게된다면 블록문으로 해석하게된다.
즉, 객체 리터럴은 변수에 할당 함에있어서 객체 리터럴로써 평가된다고 할수있다.

```javascript
{...} // 블록문

var tangerine = {}; //객체리터럴
```

위의 예제 처럼 프로퍼티를 정의하지 않은 객체리터럴을 이용한 객체 생성 방식은 빈객체로 표현되며, 코드블록 뒤에 세미콜론을 붙여준다. 객체리터럴은 코드블록을 의미하는것이아니라, 값으로 평가되는 표현식이기 때문이다.

## 📰 프로퍼티

객체는 프로퍼티들의 집합이며, 키(key)와 값(value)으로 구성된다.
프로퍼티 나열에 있어서는 `,` 로 구분하며 마지막 프로퍼티에는 찍지 않아도 된다.

```javascript
var myPhone = {
  name: 'iphone',
  manuFacturer: 'apple',
};
```

위 예제에서의 프로퍼티키는`name, manuFacturer` 이고 프로퍼티값은 `'iphone11','apple'`이다.
프로퍼티키에는 모든 값이 올수있다고 했는데 **프로퍼티 키에는 빈문자열을 포함하는 <u>모든 문자열</u> 또는 심벌값이 올수있다.**

사실 프로퍼티키는 문자열인데 객체내에서 프로퍼티키는 자바스크립트 엔진이 문자열이나 심벌값이 아닌 다른값을 사용하면 암묵적으로 문자열로 타입변환시켜준다.

또한 여기서의 프로퍼티 키는 값에 접근하도록해주는 식별자 역할을 하기에 식별자 명명 규칙을 따라야 할것 같지만 반드시 그렇지는 않다. 하지만 자유에는 책임이 있듯이 반드시 `' '," "`따옴표를 사용해야한다.

식별자 네이밍 규칙을 따르지 않으면 의도하지 않은 일들이 발생한다.

```javascript
var myPhone = {
  name: 'iphone11',
  manu-Facturer: 'apple',
};
```

위코드에서 자바스크립트 엔진은 manu-Facture를 `-` 연산자가 있는 표현식으로 해석하게된다.

문자열 또는 문자열로 평가되는 표현식을 사용해 프로퍼티키의 동적생성을 이끌어낼수있다. 이때에는 대괄호`[]`를 사용해 묶어주어야한다.

```javascript
var obj = {};
var propertyKey = 'tangerine';

obj[propertyKey] = 'peanut';

consoel.log(obj); // {tangerine : peanut}
```

프로퍼티키에 예약어를 사용해도 오류가 나지않고, 빈문자열을 프로퍼티 키로 사용해도 에러가 발생하지 않는다. 프로퍼티키의 예상치 못한 오류를 발생할수 있고, 프로퍼티키의 의미를 갖지못하기에 사용하지 않는것이 맞다고 생각한다.

이미존재하는 프로퍼티키의 중복선언을 해도 에러가 발생하지 않고, 나중선언된 프로퍼티가 먼저선언된 프로퍼티를 덮어쓴다.

```javascript
var person = {
  name: 'lee',
  name: 'kim',
};

console.log(person); // {name : 'kim'}
```

## 🧮 메서드

자바스크립트에서 프로퍼티값에는 모든값을 사용할수 있다고 했다. 함수는 자바스크립트에서 일급 객체로 평가됨으로 값으로 취급할수 있기에 프로퍼티 값에 올수있다.

**프로퍼티값으로 오는 함수는 일반함수와 구분하기위해 메서드라 부르며 객체에 묶여있는 함수를 의미한다.**

```javascript
var person = {
  name: 'kim',
  address : function(){
    ...
  }
};
```

## 🔐 프로퍼티 접근

프로퍼티 접근 방식은 두가지가 있다.

- 마침표 프로퍼티`.`접근연산자를 사용하는 마침표 표기법
- 대괄호 프로퍼티`[...]`접근연산자를 사용 대괄호 표기법

프로퍼티 키가 식별자 네이밍규칙을 준수하면 마침표접근연산자,대괄호를 둘다 사용할수있다.
그렇다는 것은 식별자네이밍 규칙을 준수하지 않는다면 둘다 사용할수 없다는것이다.

```javascript
var myPhone = {
  name: 'iphone',
};

console.log(myPhone.name); //iphone
console.log(myPhone['name']); //iphone
```

위와 같이 **대괄호 프로퍼티 접근 연산자 내부에 지정하는 프로퍼티 키는 반드시 따옴표로 감싼 문자열이어야한다.**
그렇지 않으면 식별자로 해석한다.

```javascript
var myPhone = {
  name: 'iphone',
};

console.log(myPhone.name);
console.log(myPhone[name]); // ReferenceError: name is not defined;
```

객체에 존재하지 않는 프로퍼티에 접근하면 ReferenceError를 반환하지 않고 undefined를 반환한다.
이는 프로퍼티 동적 생성과 관련이있다.

```javascript
var myPhone = {
  name: 'iphone',
};

console.log(myPhone.manuFacturer); // undefined
```

## 📝 프로퍼티 값 갱신

이미 존재하는 프로퍼티에 값을 할당하게되면 프로퍼티 값이 갱신된다.

```javascript
var myPhone = {
  name: 'iphone',
};

myPhone.name = 'galaxy';

console.log(myPhone.manuFacturer); // {name :'galaxy'}
```

## 🎇 프로퍼티 동적 생성

존재하지 않는 프로퍼티에 값을 할당하면 동적생성이 이루어지고 프로퍼티 값도 할당된다.

```javascript
var myPhone = {
  name: 'iphone',
};

myPhone.name = 'galaxy';
myPhone.manuFacturer = 'samsung';
console.log(myPhone.manuFacturer); // {name :'galaxy' ,manuFacturer:'samsung'}
```

## 🪁 프로퍼티 삭제

delete 연산자는 객체의 프로퍼티를 삭제할수 있다. delete 연산자의 피연산자는 프로퍼티값에 접근할수 있는 표현식이어야 하며, 존재하지 않는 프로퍼티를 삭제하려고 한다면 아무런 에러없이 무시된다.

```javascript
var myPhone = {
  name: 'iphone',
};

myPhone.name = 'galaxy';

myPhone.manuFacturer = 'samsung';

delete myPhone.name; // name이라는 프로퍼티키 삭제
delete myPhone.price; // 존재하지 않는 프로퍼티 키를 삭제 -> 오류출력을 안한다.

console.log(myPhone.manuFacturer); // {manuFacturer: 'samsung'}
```

## 🧱 ES6에서 추가된 객체 리터럴의 확장기능

- ### 📌 프로퍼티 축약 표현

- ### 📗 계산된 프로퍼티 이름

- ### 📘 메서드 축약 표현
