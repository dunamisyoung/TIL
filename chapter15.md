# 🎈15. let, const와 블록 레벨 스코프 part arrangement

## 🔎 var키워드로 선언한 변수의 문제점

ES5 까지 변수를 선언할수 있는 방법은 단 하나 var 뿐이었다. 하지만 ES6 부터는 var의 특징을 보완한 let, const가 나왔다. 그부분을 공부해보자

- ### 🔗 변수의 중복 선언 허용

  var 키워드로 선언한 변수는 중복 선언이 가능하다.

  ```javascript
  var year = '2020년';
  var month = '9월';

  var year = '2021년';
  var month; // 초기화문이 없는 변수 선언문은 무시된다.

  console.log(year); // 2021년
  console.log(month); // 9월
  ```

  위와 같이 동일한 이름의 변수가 이미 선언되어있는것을 모르고 변수를 중복선언 하면 **나중에 선언한 변수에 할당된 값으로 이전에 선언된 변수 값이 변경된다.**

- ### ⛓ 함수 레벨 스코프

  var키워드로 선언한 변수는 오로지 **함수의 코드 블록만을 지역 스코프로 인정한다.**

  ```javascript
  var color = 'red';

  if (true) {
    var color = 'green';
  }

  console.log(color); // green
  ```

  **for문의 변수 선언문 에서 var 키워드로 선언한 변수도 전역 변수가 된다.**

  ```javascript
  var i = 'iterate';

  for (var i = 0; i < 5; i++) {
    console.log(i); // 0 1 2 3 4
  }

  console.log(i); //5
  ```

- ### 🎢 변수 호이스팅

  var키워드로 변수를 선언하게 되면, 변수 호이스팅에 의해 변수 선언문이 선두로 끌어 올려진 것처럼 동작한다.
  즉, 변수 선언문 이전에 변수를 참조할 수 있음을 의미한다. 단 할당문 이전에 변수를 참조하면, undefined를 반환한다.

  ```javascript
  console.log(tangerine); // undefined

  tangerine = 'peanut';

  console.log(tangerine); // peanut

  var tangerine;
  ```

## 🎭 let 키워드

let 키워드는 var 키워드의 단점을 보안하기 위해서 ES6에서 만든 새로운 변수 선언 키워드이다. var과 무엇이 다른지 잘살펴보자.

- ### 🧬변수 중복 선언 금지

  **var 키워드로 동일한 이름의 변수를 중복 선언하게되면 아무런 에러가 발생하지 않는다.** 이때 변수를 중복선언하면서 **값까지 할당하게되면 의도치 않게 먼저 선언된 변수 값이 재할당 되어 변경되는 부작용이 발생**하게된다.

  하지만 let 키워드로 같은 변수를 중복 선언하면 문법 에러가 발생한다.

  ```javascript
  var tangerine = '귤';
  var tangerine = '작은오렌지';
  // var 키워드를 사용한 변수선언에서는 같은 스코프내에서 중복선언을 허용한다.

  let peanut = '땅콩';
  let peanut = '적은액수'; // SyntaxError: Identifier 'peanut' has already been declared
  ```

- ### 🧱블록 레벨 스코프

  **var로 선언한 변수**는 함수의 코드 블록만을 지역 스코프로 인정하는 **함수 레벨 스코프**를 따른다. 하지만 **let키워드로 선언한 변수**는 모든 코드 블록을 지역 스코프로 인정하는 **블록 레벨 스코프**를 따른다.

  ```javascript
  let global = 100; //전역 변수

  {
    let global = 200;
    let local = 300;
  }

  console.log(global); // 100
  console.log(local); // ReferenceError: bar is not defined
  ```

  let으로 선언한 변수는 블록레벨 스코프를 가지기에 코드블록안에서 실행된 변수 식별자 global,local을 참조할수 없다.

- ### 📤변수 호이스팅

  var키워드로 선언한 변수와는 다르게 let키워드로 선언한변수는 호이스팅이 발생하지 않는것 처럼 보여진다.

  ```javascript
  console.log(tangerine); //ReferenceError: tangerine is not defined
  var tangerine;
  ```

  let 키워드로 선언한 변수를 변수 선언문 이전에 참조하면 참조 에러가 발생한다.

  **var 키워드로 선언한 변수같은경우 런타임이전에 선언과 초기화가 한번에 진행된다.**
  즉, 스코프(실행컨텍스트 렉시컬환경)에 식별자를 등록해 자바스크립트 엔진에 변수의 존재를 알린다. 그리고 **즉시 초기화 단계를 실행해서 undefined를 할당해 변수를 초기화한다.**

  그리하여 변수 선언문 이전에 변수에 접근해도 스코프에 변수가 존재하기 때문에 에러가 발생하지않는다.

  ```javascript
  console.log(tangerine);

  var tangerine;
  console.log(tangerine);

  tangerine = 'peanut';
  console.log(tangerine);
  ```

  하지만 **let 키워드는 선언단계와 초기화 단계가 분리되어 진행**된다.
  즉, 런타임 이전에 스코프(실행컨텍스트 렉시컬환경)에 변수 식별자 네이밍을 기억하게끔하고, **이후에 초기화단계는 변수선언문에 도달하게되면 비로서 실행**된다.

  만약 초기화 단계가 실행되기 이전 즉, 변수 선언문이전에 값에 접근하려고 하면 에러가 발생한다.
  let 키워드로 선언한 변수는 스코프 시작지점부터 변수선언문 지점까지 변수를 참조할 수 없다.
  이 구간을 일시적 사각지대 TDZ(Temporal Dead Zone; TDZ)라고 부른다.

  ```javascript
  console.log(tangerine); // ReferenceError : tangerine is not defined

  let tangerine; // 변수 선언문에서 초기화 단계가 실행된다.
  console.log(tangerine); // undefined

  tangerine = 'peanut';
  console.log(tangerine); // peanut
  ```

  이렇게 보면 let키워드를 사용한 변수선언은 호이스팅이 발생하지 않는것처럼 보이지만 그렇지 않다.

  ```javascript
  let today = 'tangerine'; // 전역 변수

  {
    console.log(today); //  ReferenceError: Cannot access 'today' before initialization => 이미 today 라는 변수가 선언되었고 그값에 접근할수 없다.
    let today = 'peanut'; // 지역 변수
  }
  ```

- ### 📜전역 객체와 let

## 🔒const 키워드

- ### 🎰 선언과 초기화

- ### 🧩 재할당 금지

- ### 🔐 상수

- ### 📌 const 키워드와 객체

## 📍 var vs. let vs. const
