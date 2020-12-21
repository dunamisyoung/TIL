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
