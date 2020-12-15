# 20. strict mode

## 1. strict mode란?

아래 예제의 실행 결과는 무엇일지 생각해보자.

```javascript
function foo() {
  x = 10;
}
foo();

console.log(x); // ?
```

foo 함수 내에서 선언하지 않은 변수인 x에 값 10을할당했다. 이경우 자바스크립트 엔진은 x 변수가 어디 선언되었는지 스코프 체인을 통해 검색한다. 하지만 어디서도 선언한 변수 x 를 찾을수 없게된다.

이때, 자바스크립트 엔진은 **암묵적으로 전역 객체에 x 프로퍼티를 동적으로 생성**하고 이때 선언된 x 프로퍼티는 **전역 변수처럼 사용**이 가능하다. 이러한 현상을 **암묵적 전역**이라고 한다.

이렇게 개발자의 의도와 다르게 전역에 선언된 암묵적 전역은 오류를 발생시킬수 있는 원인이 된다. 따라서 반드시 var, let, const 키워드를 사용하여 변수를 선언할수 있도록하자.

하지만 개발자는 기계가 아니라 사람인지라 오타나 문법적 지식의 미비로 인해 실수할수있다. 이러한 실수가 발생했을떄 명시적인 에러를 발생시켜 자바스크립트의 개인행동을 막고자 **ES5부터 strict mode(엄격모드)가 추가** 되었으며, 이는 자바스크립트 엔진에 최적화 작업에 문제를 일으킬수 있는 코드에 대해 명시적으로 에러를 발생시킨다.

**ESLint 같은 린트 도구를 사용하여도 strict mode와 유사한 효과를 얻을수 있다.** 개발을 할때 설치해서 사용하도록하자 :)

## 2. strict mode의 적용

strict mode를 적용하려면 전역의 선두나 함수몸체의 선두에 `'use strict';` 를 추가해준다.

전역의 선두에 추가하면 스크립트 전체에 strict mode가 적용된다.

`use strict` 를 작성하자 아래와같이 엄격모드인 s**trict mode**가 적용되어 선언되지 않은 변수에 대해 ReferenceError를 발생시킨다. 이때 주의할점은 **strict mode**를 **사용하고자 하는 코드의 선두에 작성해주어야한다.**

```javascript
'use strict';

function foo() {
  x = 10; // ReferenceError: x is not defined
}

foo();
```

그렇지 않으면 strict mode가 제대로 동작하지 않는다.

```javascript
function foo() {
  x = 10; // 에러를 발생시키지 않는다.
  ('use strict');
}

foo();
```

## 3. 전역에 strict mode를 적용하는 것은 피하자

전역에 적용한 strict mode는 스크립트 단위로 적용된다.

```javascript
<!DOCTYPE html>
<html lang="ko-KR">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <script>
      'use strict'; // 이곳에 작성한 코드는 strict mode가 적용된다.

    </script>

    <script>
      x = 1; // 에러가 발생하지 않는다.
      console.log(x);
    </script>

    <script>
      'use strict';

      y = 1; // ReferenceError: y is not defined
      console.log(y);
    </script>
  </body>
</html>
```

위 예제와 같이 스크립트 단위로 적용된 strict mode는 다른 스크립트에 영향을 주지 않고 `'use strict'` 라고 명시해준 해당 스크립트에 한정되어 적용된다.

이때 strict mode를 **적용한 script** 와 **적용하지 않은 script** 때문에 오류를 발생할 가능성이 있기에 전역에 strict mode를 적용하는 것은 바람직 하지않다.

이럴경우에는 **즉시 실행함수로 스크립트 전체를 감싸 스코프를 구분**하여 **즉시실행 함수의 선두에 strict mode를 사용**해주자.

```javascript
(function () {
  'use strict';
})();
```

## 4. 함수 단위로 strict mode를 적용하는 것도 피하자

위에서 본것처럼 strict mode를 적용한 스코프와 적용하지 않은 스코프 때문에 오류를 불러들일 가능성이 있으며, 매번 strict mode를 각각의 스코프에 적용해서 사용하는것은 번거로운 일이 아닐수 없다. 또한 strict mode가 적용된 함수가 참조할 외부컨텍스트에, strict mode를 적용하지 않는다면 문제가 발생할수있다.

**strict mode를 사용할때에는 즉시 실행함수로 감싼 스크립트 단위로 적용하자.**

```javascript
(function () {
  var let = 10; // 에러 발생 x - strict mode는 적용할 스코프의 선두에 작성해야한다.

  function foo() {
    'use strict';

    let = 20; // Syntax Error: Unexpected strict mode reserve word
  }

  foo();
})();
```

## 5. strict mode가 발생시키는 에러

strict mode가 발생시키는 에러에 대해 알아보자 즉, strict mode 에서 지원하는 엄격한 문법을 알아보자

### 5.1 암묵적 전역

**선언하지 않은 변수를 참조하면 ReferenceError가 발생**한다.

```javascript
(function () {
  'use strict';

  x = 1;
  console.log(x); // ReferenceError: x is not defined
})();
```

### 5.2 변수, 함수, 매개변수의 삭제

**delete 연산자로 변수, 함수, 매개변수를 삭제**하면 SyntaxError 발생한다.

```javascript
(function () {
	'use strict';

	var x =1;
	delete x;	// SyntaxError: Delete of an unqualified identifier in strict mode
}
```

### 5.3 매개변수 이름의 중복

**중복된 매개변수 이름을 사용**하면 SyntaxError가 발생한다.

```javascript
(function () {
  'use strict';
  // SyntaxError: Duplicate parameter name not allowed in this context
  function foo(x, x) {
    return x + x;
  }
  console.log(foo(1, 2));
})();
```

### 5.4 with 문의 사용

**with 문은 전달된 객체를 스코프 체인에 추가하는 문법**인데 strict mode 안에서 with 문을 사용하면 SyntaxError가 발생한다. with 문은 **동일한 객체의 프로퍼티를 반복해서 사용할떄 객체 이름을 생략할 수 있어 코드가 간단해 지는 효과**가 있지만 성능과 가독성이 좋지 못해 사용하지 않는것이 좋다.

```javascript
(function () {
  'use strict';

  with ({ x: 1 }) {
    console.log(x); // SyntaxError: Strict mode code may not include a with statement
  }
})();
```

## 6. strict mode 적용에 의한 변화

### 6.1 일반 함수의 this

strict mode 에서 함수를 일반 함수로써 호출하면 **this에 undefined가 바인딩**된다. 이는 **생성자 함수가 아닌 일반함수 내부에서는 this의 사용목적을 잃기 때문**이다. 이떄 에러는 발생하지 않는다.

```javascript
(function () {
	'use strict';

	function foo(){
		console.log(this); // undefined
	}
	foo();
}
```

### 6.2 arguments 객체

strict mode 에서는 **매개변수에 전달된 인수를 재할당 하여도 arguments 객체에 반영되지 않는다.**

```javascript
(function (a) {
  'use strict';
  // 매개변수에 전달된 인수에 숫자값 2를 재할당
  a = 2;

  // 변경된 인수가 적용되었다면 {0 : 2, length: 1}
  console.log(arguments); // {0 : 1, length: 1}
})(1);
```
