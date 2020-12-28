# 5. ref : DOM에 이름달기

이곳은 중요하다고 생각하는 개념들, 흩어진 개념들의 집합소 입니다. :)

---

## 5.1. ref는 어떤 상황에서 사용해야 할까?

---

### 리액트 컴포넌트에서는 id를 사용하면 안되는것인가?

기존에 DOM 요소에 이름을 달아줄떄 id, class를 사용했다. 하지만 리액트 컴포넌트에서는 **id**에 대한 언급이 없다. 그렇다고해서 id를 사용하면 안되는건가?

리액트 컴포넌트안에서 id를 사용할 수 있다. JSX 코드에서 DOM에 id를 달면 렌더링시 그대로 전달된다. 하지만 특수한 경우가 아니라면 권장하지 않는다. 사용하지않는이유는 id는 고유한값인데, 같은 id값을 가진 컴포넌트가 여러번 사용될수 있기에, 사용하지 않는다.

**ref는 전역적으로 작동하지 않고 컴포넌트 내부에서만 작동하기에 이런 문제가 생기지 않는다.**

### ref는 특정 DOM 안에 작업을해야할때 사용한다.

ref는 DOM을 꼭 직접 건드려야할때 사용된다. 예를 들어 input에 특정 값이 맞는지 확인할떄는 아래와같이 작성하게된다.

```jsx
<!DOCTYPE html>
<html lang="ko-KR">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Example</title>
    <style>
      .success {
        background-color: green;
      }
      .failure {
        background-color: red;
      }
    </style>
    <script>
      function validate() {
        var input = document.getElementDyId('password');
        input.className = '';
        if (input.value === '0000') {
          input.className = 'success';
        } else {
          input.className = 'failure';
        }
      }
    </script>
  </head>
  <body>
    <input type='password' id='password'></input>
    <input onclick='validate()'>Validate</input>
  </body>
</html>
```

리액트에서는 이런 작업은 DOM에 접근하지 않고 state로 구현할 수 있다. 앞으로 좀더 공부하면서 알아보자.

### 클래스형 컴포넌트에서 state를 통한 DOM변경

```jsx
import { Component } from 'react';
import './ValidationSample.css';

class ValidationSample extends Component {
  state = {
    password: '',
    clicked: false,
    validated: false,
  };

  handleChange = (e) => {
    this.setState({
      password: e.target.value,
    });
  };

  handleButtonClick = () => {
    this.setState({
      clicked: true,
      validated: this.state.password === '0000',
    });
  };

  render() {
    return (
      <div>
        <input
          type="password"
          value={this.state.password}
          onChange={this.handleChange}
          className={this.state.clicked ? (this.state.validated ? 'success' : 'failure') : ''}
        />
        <button onClick={this.handleButtonClick}>검증하기</button>
      </div>
    );
  }
}

export default ValidationSample;
```

input에서는 onChange 이벤트 발생시 handleChange를 호출해서 state의 password 값을 업데이트 하게 했다. button에서는 onClick 이벤트가 발생하면 handledButtonClick을 클릭해서 clicked 값을 참으로 설정했고, validated값을 검증 결과로 설정했다.

위에서 설정한 조건에 따라 `import './ValidationSample.css';` 안에 있는 css 파일에의해 input 색상이 초록색 또는 빨간색으로 나타나게된다.

그리고 나서 App 컴포넌트에서 ValidationSample을 import 해서 return 안에 넣어주면된다.

---

### DOM을 꼭 사용해야 하는 상황

위에서는 state를 통해 필요한 기능을 구현했지만, **state 만으로 해결할수 없는 기능**들이있다.

- 특정 input에 포커스주기
- 스크롤 박스 조작하기
- Canvas 요소에 그림그리기

이때는 어쩔수 없이 **DOM에 직접접근해야한다.** [이때 **ref**를 사용](https://ko.reactjs.org/docs/refs-and-the-dom.html)하게된다.

---

## 5.2 ref 사용

---

### 콜백함수를 통한 ref 설정

**ref를 만드는 가장 기본적인 방법은 콜백함수를 사용하는것**이다.

- ref(reference - 참조)를 달고자 하는 요소에 **ref 콜백함수를 props로 전달한다.**
- 이 콜백 함수는 ref 값을 파라미터로 전달받는다.
- 함수 내부에서 파라미터로 받은 ref를 컴포넌트의 멤버 변수로 설정한다.

```jsx
<input
  ref={(ref) => {
    this.input = ref;
  }}
/>
```

이렇게되면 this.input은 input요소의 DOM을 가르키게된다. 또한 ref의 이름은 DOM 타입관계없이 `this.tangerine = ref` 처럼 원하는 것으로 자유롭게 지정도할수있다.

### createRef를 통한 ref 설정

ref를 만드는 또 다른 방법은 리액트 v16.3 이후에 추가된 **createRef**라는 함수를 사용하는 것이다.

```jsx
import React, { Component } from 'react';

class RefSample extends Component {
  input = React.createRef();

  handleFocus = () => {
    this.input.current.focus();
  };

  render() {
    return (
      <div>
        <input type="text" ref={this.input} />
      </div>
    );
  }
}
ref;
```

위에서 작성한것처럼 ref를 사용하고자 하는 DOM에 ref라는 props를 콜백함수로 전달하는것이아닌 React.createRef() 를 멤버 변수안에 담아주고, 멤버 변수를 ref를 달고자 하는 요소에 props로 넣어주면 ref 설정이된다. 앞서 말한것처럼 **ref는 직접 DOM에 접근할때 사용한다는것을 기억하자.**

이렇게 ref를 설정한후 DOM에 접근하려면 this.input.current를 조회하면된다. 콜백함수를 사용했을때와 다른점은 [.current](https://ko.reactjs.org/docs/refs-and-the-dom.html#accessing-refs)를 넣어주어야한다는 것이다.

---

## 5.3 컴포넌트에 ref 달기

---

리액트에서는 사용자 정의 컴포넌트에도 ref를 달수있다. 주로 컴포넌트 내부에 있는 DOM을 컴포넌트 외부에서 사용할때 쓴다.

### 사용법

```jsx
<MyComponent
  ref={(ref) => {
    this.MyComponent = ref;
  }}
/>
```

이렇게 작성하면 **MyComponent 내부의 메서드 및 멤버 변수에 접근이 가능**하다. 즉, 내부의 ref에도 접근이 가능하다.

### 컴포넌트 초기설정

이번에는 스크롤 박스가 있는 컴포넌트를 만들어 스크롤바를 아래로 내리는 작업을 부모컴포넌트에서 실행해보자. 먼저 ScollBox.js 라는 컴포넌트 파일을 만들자.

```jsx
ScollBox.js;
import React, { Component } from 'react';

class ScrollBox extends Component {
  render() {
    const style = {
      border: '1px solid black',
      height: '300px',
      width: '300px',
      overflow: 'auto',
      position: 'relative',
    };

    const innerStyle = {
      width: '100%',
      height: '650',
      background: 'linear-gradient(white, black)',
    };

    return (
      <div>
        style={style}
        ref=
        {(ref) => {
          this.box = ref;
        }}
        <div style={innerStyle}></div>
      </div>
    );
  }
}

export default ScrollBox;
```

그리고는 App.js에서 import 하고 render 함수내에 넣어줍니다.

그리고는 컴포넌트에 스크롤바를 맨 아래로 내리는 메서드를 만들어보자. scrollHeight 에서 clientHeight 높이를 빼서 scrollTop에 넣어주었다.

```jsx
import React, { Component } from 'react';

class ScrollBox extends Component {
  // 스크롤을 내리는 메서드
  scrollToBottom = () => {
    const { scrollHeight, clientHeight } = this.box;
    // const scrollHeight = this.box.scrollHeight;
    // const clientHeight = this.box.clientHeight
    this.box.scrollTop = scrollHeight - clientHeight;
  };

  render() {
    const style = {
      border: '1px solid black',
      height: '300px',
      width: '300px',
      overflow: 'auto',
      position: 'relative',
    };

    const innerStyle = {
      width: '100%',
      height: '650',
      background: 'linear-gradient(white, black)',
    };

    return (
      <div>
        style={style}
        ref=
        {(ref) => {
          this.box = ref;
        }}
        <div style={innerStyle}></div>
      </div>
    );
  }
}

export default ScrollBox;
```

이렇게 만든 메서드를 App 컴포넌트의 ScrollBox에 ref를 달아주면 사용할수있다.

### 컴포넌트에 ref를 적용하고 내부 메서드 사용하기

```jsx
import { Component } from 'react';
import ScrollBox from './ScrollBox';

class App extends Component {
  render() {
    return (
      <div>
        <ScrollBox ref={(ref) => (this.scrollBox = ref)} />
        <button onClick={() => this.scrollBox.scrollToBottom()}>맨 밑으로</button>
      </div>
    );
  }
}

export default App;
```

여기서 주의할 점은 문법상 `onClick = {this.scrollBox.scollBottom}` 같은 형식도 맞지만 컴포넌트가 **처음 렌더링 될때는 값이 undefined** 이므로 새로운 함수를 통해 **함수내부에서 이미 렌더링을 해서 this.scroll을 설정한 시점의 값을 읽어**와서 실행하기에 오류를 막을수 있다는 점이다.

---

## 5.4 정리

---

- 리액트에서 id를 사용하지 않는 이유는 id자체는 고유한 값이고 그값이 다른 컴포넌트에서 여러번 사용된다면 고유한 값의 역할을 하지 못하기 떄문이다.
- **ref**를 사용하는 경우는 state를 통해 문제를 해결할수 없음으로 DOM에 꼭 접근해야만 할때이다.보통 [이때 **ref**를 사용](https://ko.reactjs.org/docs/refs-and-the-dom.html)한다.
- **콜백함수를 사용해서 ref를 만들때의 방법**

1. ref를 사용하고자 하는 요소에 ref 콜백함수를 props로 전달한다.
2. 콜백 함수는 ref 값을 파라미터로 전달받는다.
3. 함수 내부에서 파라미터로 받은 ref를 컴포넌트의 멤버 변수로 설정한다.

- `<input ref={(ref) => {this.input=ref}} />`
- **createRef를 통해 ref를 사용할때 1.** React.createRef() 를 멤버 변수안에 담아주고,

2. 멤버 변수를 ref를 달고자 하는 요소에 props로 넣어주면 ref 설정이된다.
3. 값에 접근할때는 [.current](https://ko.reactjs.org/docs/refs-and-the-dom.html#accessing-refs)를 넣어주어야한다.

- **사용자 정의 컴포넌트에서 ref사용**
  사용법은 콜백함수를 사용해서 ref를 만들때와 동일하다.
  이를통해 부모 컴포넌트에서 ref 컴포넌트를 사용한 컴포넌트에 접근이 가능하다.
- 컴포넌트 내부에서 DOM에 직접 접을할때는 ref를 사용한다.하지만 [ref를 사용할때는 신중하게 사용](https://ko.reactjs.org/docs/refs-and-the-dom.html#dont-overuse-refs)하자.
- 서로다른 컴포넌트끼리 데이터를 교류할때 ref를 사용하는것은 옳지 못하다. 그러므로 **언제나 데이터 교류는 부모 ↔ 자식 흐름으로 교류**해야한다.
