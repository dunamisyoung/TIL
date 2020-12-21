# 2. JSX

**`이곳은 중요하다고 생각하는 개념들, 흩어진 개념들의 집합소 입니다.` :)**

---

## 2.1 코드 이해하기

---

### import React from 'react';

이 코드는 리액트를 불러와서 사용할수 있게 해준다.

리액트 프로젝트 생성시 node_modules라는 디렉터리도 함께생성된다. 그 디렉터리 안에있는 react 모듈을 가져와 import 해서 사용할수 있다.

모듈을 불러와서 사용하는것은 원래 브라우저에는 없던 기능으로 Node.js에서 지원하는 기능이다.이러한 기능을 사용하기위해 번들러(bundler)를 사용하는대 대표적으로 webpack이 있다.

- 번들러 → 파일을 묶는다는 뜻이다. 즉, 파일을 묶듯이 연결한다.

### 웹팩을 사용하는 이유?

편의성과 확장성이 다른 도구보다 뛰어나다. 번들러 도구를 사용하면 import를 이용해 모듈을 불어왔을때 불러온 파일을 모두 합쳐서 하나의 파일을 생성하게된다. 최적화 과정에서 여러개의 파일로 분류되기도 한다.

파일을 불러올때는 웹팩의 로더라는 기능을 통해 불러온다. 웹팩의 로더에는 여러가지 종류가 있다.

- **css-loader** : CSS 파일을 불러올 수 있게 해준다.
- **file-loader** : 웹폰트나 미디어 파일등을 불러올 수 있게 해준다.
- **balbel-loader** : 자바스크립트 파일들을 불러와 최신 문법을 ES5문법으로 변환해준다.

### App 컴포넌트

```jsx
// App.js

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a className="App-link" href="https://reactjs.org" target="_blank" rel="noopener noreferrer">
          Learn React
        </a>
      </header>
    </div>
  );
}
```

위코드를 보면 **function 키워드**를 사용해 컴포넌트를 만들었다.

위와 같은 컴포넌트를 **함수형 컴포넌트**라고한다. 컴포넌트를 렌더링 하면 함수에서 반환하고 있는 내용을 나타내게 되는데, 함수에서 반환하고있는것이 마치 HTML 같이 보인다. 이는 사실 HTML 이 아닌 **JSX**다.

---

## 2.2 JSX란?

---

### JSX

JSX는 자바스크립트의 확장 문법으로 XML과 매우 비슷하게 생겼다.

이런형식으로 작성한코드는 브라우저에서 실행전 바벨에 의해 일반 자바스크립트 형태의 코드로 변환된다. 아래의 코드는 어떻게 변환될까 ?

```jsx
// App.js

function App() {
  return (
    <div>
      Hello <b>React</b>
    </div>
  );
}
```

위 코드는 아래와 같이 변환된다.

```jsx
function App(){
	retrun React.createElement('div', null, 'Hello', React.createElement('b', null, 'react'));
}
```

컴포넌트 랜더링을 위해 위와같이 코드를 작성한다면 매우 불편할것이다. 그렇기에 JSX를 사용한다.

---

## 2.3 JSX의 장점

---

### 보기쉽고 익숙하다

일반 자바스크립트를 사용한코드와 JSX로 작성한 코드를 비교했을때 몇 초만 보아도 JSX를 사용하는것이 가독성 높고 작성하기도 쉽게 느껴진다.

### 높은활용도

JSX에서는 HTML 태그 뿐만아니라 앞으로 만들 컴포넌트도 JSX 안에서 작성이 가능하다. 아래의 코드를 보면 컴포넌트를 HTML 태그 쓰듯이 작성한다.

```jsx
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
```

### ReactDOM.render란?

**컴포넌트를 페이지에 렌더링 하는 역할**을 하며, react-dom 모듈을 불러와 사용할수 있다. 이 함수의 **첫번째 파라미터에는 페이지에 JSX 형태로 렌더링할내용을 적어주고, 두번째파라미터에는 JSX를 렌더링할 document 내부요소를 설정**한다.

### React.StrictMode

**리액트 프로젝트에서 리액트의 예전기능들을 사용하지 못하게 하는 기능**이다. 이전문법을 사용하면 경고를 출력한다.

---

## 2.4 JSX 문법

---

### 요소감싸기

**컴포넌트에 여러 요소가 있다면 반드시 부모요소로 감싸야한다.** 아래와 같은 코드는 제대로 작동하지 않는다.

```jsx
import React from 'react';

function App() {
	return(
		<h1>리액트 안녕~</h1>
		<h2>잘 동작하니?</h2>
	)
}

export default App;
```

그렇기에 아래와 같이 하나의 부모요소로 감싸주어야한다.

이렇게 작성해야하는 이유는 **VirtualDOM**에서 컴포넌트 변화를 감지해 낼때 효율적으로 비교할 수있도록 컴포넌트 내부는 **하나의 DOM 트리구조로 이루어져야한다는 규칙**이 있기 떄문이다.

```jsx
import React from 'react';

function App() {
  return (
    <div>
      <h1>리액트 안녕~</h1>
      <h2>잘 동작하니?</h2>
    </div>
  );
}

export default App;
```

리액트 v16 이상부터는 div 대신 **Fragment**를 사용하면된다. 주석과 같이 작성해도 잘동작한다.

```jsx
import React from 'react';
/* import React, {Fragment} from 'react'; */

function App() {
	return(
		<> {/* <Fragment> */}
			<h1>리액트 안녕~</h1>
			<h2>잘 동작하니?</h2>
		</> {/* </Fragment> */}
	)
}

export default App;
```

### 자바스크립트 표현

JSX는 DOM 요소를 렌더링 하는 기능말고도 JSX 안에서 자바스크립트 표현식을 사용할수 있는데 이는 `{}` 안에 작성 하면된다.

```jsx
import React from 'react';

function App() {
  const name = '리액트';
  return (
    <>
      <h1>{name} 안녕~</h1>
      <h2>잘 동작하니?</h2>
    </>
  );
}

export default App;
```

### if 문 대신 조건부 연산자

JSX 내부의 자바스크립트 표현식에서 if문을 사용할 수 없다. 이러한 이유로 조건에 따라 다른 내용을 렌더링시에 JSX 밖에서 if문을 사용하여 사전에 값을 설정하거나, `{}` 안에 삼항조건 연산자를 사용한다.

```jsx
import React from 'react';

function App() {
  const name = '리액트';
  return <div>{name === '리액트' ? <h1>리액트입니다.</h1> : <h2>리액트가 아닙니다.</h2>}</div>;
}

export default App;
```

### AND 연산자(&&)를 사용한 조건부 렌더링

특정 조건을 만족할때 내용을 보여주고, 만족하지 않을 때는 아무것도 렌더링 하지않아야 하는 상황이 온다. 이럴때 사용할수 있는것이 AND 연산자(&&)이다. 이렇게 하면 삼항조건 연산자보다 조금더 간결한 코드가 작성이 가능하다.

```jsx
import React from 'react';

function App() {
  const name = '리왝트';
  return <div>{name === '리액트' ? <h1>리액트입니다.</h1> : null}</div>;
}

export default App;
```

### undefined를 렌더링 하지않기

리액트 컴포넌트에서는 함수에서 undefined만 반환하여 렌더링 하게되면 오류를 발생 시킵니다.

그렇기에 **어떤값이 undefined 일수 있다면 OR(||) 연산자를 사용**하여 undefined 일떄 사용할 값을 지정하여 오류를 방지할 수 있습니다.

```jsx
import React from 'react';
import './App.css';

function App() {
  const name = undefined;
  return name || '값이 undefined입니다.';
}

export default App;
```

반면 JSX 내부에서 undefined를 반환하는 것은 가능하다.

### 인라인 스타일링

리액트에서 DOM 요소에 스타일을 적용할때는 **문자열 형태로 넣지 않고 객체형태로 넣어준다.** 스타일 이름중 `-` 가 포함 되어있는 이름은 카멜케이스 표기법으로 작성해야한다.

```jsx
import React from 'react';
import './App.css';

function App() {
  const name = '리액트';
  const style = {
    backgroundColor: 'black',
    color: 'aqua',
    fontSize: '48px',
    fontWeight: 'bold',
    padding: 16, // 단위 생략시 px로 지정된다.
  };
  return <div style={style}>{name}</div>;
}

export default App;
```

지금은 스타일 객체를 만들어서 div의 style 어트리뷰트로 전달했다. 미리 선언하지 않고도 div 안에서 값을 지정할수도있다.

```jsx
import React from 'react';
import './App.css';

function App() {
  const name = '리액트';
  return (
    <div
      style={{
        backgroundColor: 'black',
        color: 'aqua',
        fontSize: '48px',
        fontWeight: 'bold',
        padding: 16, // 단위 생략시 px로 지정된다.
      }}
    >
      {name}
    </div>
  );
}

export default App;
```

### class 대신 className

JSX에서는 HTML에서 클래스 정의방식과는 다르게 **class가 아닌 className으로 설정**해주어야한다.

```jsx
//App.css
.react{
	background: aqua;
	color: black;
	fontSize : 48px;
	fontWeight : bold;
	padding : 16px;
}

---
// App.js
import React from 'react';
import './App.css'

function App() {
		const name = '리액트';
	return <h2 className='react'>{name}</h2>
}

export default App;
```

### 꼭 닫아야하는 태그

HTMl 코드 작성시 가끔 태그를 닫지 않은 상태로 코드를 작성해도 동작한다. 하지만 JSX에서는 허용하지 않는다. 그렇기에 자식요소가 없다면, `</>` 를 이용해 꼭 태그를 닫아주어야한다. 이러한 태그를 self-closing 태그라고 부른다.

### 주석

JSX 안에서 주석을 작성하는 방법은 아래와 같다.

```jsx
import React from 'react';

function App() {
  const name = '리액트';
  return (
    <>
      {/* 주석은 이렇게 작성합니다. */}
      <div
        className="react" // 시작 태그를 여러줄로 작성한다면 이러한 주석도 가능하다.
      >
        {name} 안녕~
      </h1>
      // 이곳에서는 그대로 나타난다. /* 이곳에서는 그대로 나타난다.*/
    </>
  );
}

export default App;
```
