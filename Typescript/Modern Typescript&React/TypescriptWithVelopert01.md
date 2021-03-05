## Typescript ?

타입스크립트는 자바스크립트의 수퍼셋으로 자바스크립트가 동작하는 어느곳에서든지 동작한다.

환경설정부터 알아보자.

### 초기 설정값

```tsx
// package.json 파일 생성 및 ts-node 설치
npm init -y
npm i typescript ts-node

// 프로젝트의 typescript 설정파일생성 -> tsconfig.json
npx tsc --init

// ts -> js
npx tsc
```

### TypeSciprt의 타입

```tsx
// Typescript
const message: string = 'hello world';
console.log(message);

// Javascript
('use strict');
var message = 'hello world';
console.log(message);
```

위에서보면 message 변수 옆에 **:string** 이라는 type이 붙어있다. 이것은 typeScript가 말하고 있는 type의 일부분인 string 타입이며, type을 표기할때는 변수 오른쪽에 ex) `:string` 이런식으로 표기하게된다.하지만 무조건적으로 타입을 명시하지는 않아도 된다.

### tsconfing.json

```tsx
"compilerOptions": {
    /* Visit https://aka.ms/tsconfig.json to read more about this file */

    /* Basic Options */
    // "incremental": true,                         /* Enable incremental compilation */
    "target": "es5",                                /* Specify ECMAScript target version: 'ES3' (default), 'ES5', 'ES2015', 'ES2016', 'ES2017', 'ES2018', 'ES2019', 'ES2020', or 'ESNEXT'. */
    "module": "commonjs",

// 컴파일 옵션을 설정할 수 있다.
target : -> es5 or es6 ...

// "outDir": "./",                              /* Redirect output structure to the directory. */
"outDir": "./dist"
아래로 내리다보면 outDir가 있는데 컴파일된 코드를 어디에 저장할 것인지 설정하는것이다.
```

### package.json - ts-node

tsnode - compile 하지 않고도 파일을 실행 시킬수 있게 해준다.

사용법은 termenal에 `$ npx ts-node ./src/practice.ts` (npx ts-node 실행파일경로) 를 입력해준다.

```tsx
{
  "name": "ts-practice",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {
    "ts-node": "^9.1.1",
    "typescript": "^4.2.3"
  }
}
```

### practice.ts

```tsx
let count = 0;
count += 1;
count = '문자열'; //이미 number type을 할당한 변수에 string type을 재할당 할 수 없기에 오류

// StringType
const message: string = 'hello world';
// BooleanType
const done: boolean = false | true;

// numbersArrayType
const nubmers: number[] = [1, 2, 3, 4];
// StringsArrayType
const messages: string[] = ['hello', 'world'];

messages.push(1); //messages 배열을 type이 string인데 number type인 1을 넣는다면 오류

// string or undefined
let mightBeUndefined: string | undefined = undefined;
// number or null
let nullableNumber: number | null = null;

// type을 'red' | 'orange' | 'yellow' 3개중 1개로 지정할수있음
let color: 'red' | 'orange' | 'yellow' = 'red';
color = 'yellow';
color = 'green'; // green은 위에서 정의한 type에서 존재하지 않기에 오류
```

### Typescript → Javascript

컴파일시 type에 관한 정보는 다 사라진다.

```tsx
'use strict';
var count = 0;
count += 1;
/* count = '문자열'; //이미 number type을 할당한 변수에 string type을 재할당 할 수 없기에 오류 */
// StringType
var message = 'hello world';
// BooleanType
var done = false;
// numbersArrayType
var nubmers = [1, 2, 3, 4];
// StringsArrayType
var messages = ['hello', 'world'];
/* messages.push(1); //messages 배열을 type이 string인데 number type인 1을 넣는다면 오류 */
// string or undefined
var mightBeUndefined = undefined;
// number or null
var nullableNumber = null;
// type을 'red' | 'orange' | 'yellow' 3개중 1개로 지정할수있음
var color = 'red';
color = 'yellow';
/* color = 'green'; // green은 위에서 정의한 type에서 존재하지 않기에 오류 */
```

### Fn-practice01.ts

```tsx
function sum(x: number, y: number): number {
  return x + y;
}

const result = sum(1, 2);
```

만약 어떤 값이든 받아오고 싶다면 매개변수의 `x:any` 라고 명시할수 있겠지만, 현재는 인수로 받아온 것들을 numberType으로 받을것이기에 위와같이 명시한다. 그리고는 반환될 값도 매개변수 오른쪽에 미리 명시할수있다.

만약 위에서 명시한 값이아닌 다른 값을 반환하려고 한다면 오류가 나게된다.

```tsx
function sum(x: number, y: number): number {
  return '명시된 값과는 다른 값!';
}
```

### Fn-practice02.ts

```tsx
function sumArray(numbers: number[]): number {
  return numbers.reduce((acc, current) => acc + current, 0);
}

const total = sumArray([1, 2, 3, 4, 5]);
```

위 sumArray함수는 numbers 라는 매개 변수의 타입을 numberArray로 설정하고 반환값은 number로 명시했다. sumArray 함수를 실행하게되면 인수로 전달된 배열안의 모든숫자들이 반환되어 total이라는 변수에 담기게된다.

### Fn-practice03.ts

```tsx
function returnNothing(): void {
  return console.log('어쩌고저쩌고');
}
```

함수작성시 return 타입을 명시하지 않게되면 void('공백')라는 타입이 들어간다.

```tsx
function returnStringOrNumber(): string | number {
  return 4;
}
```

위처럼 return 값을 string type or number type 이라고 명시할 수 도있다.
