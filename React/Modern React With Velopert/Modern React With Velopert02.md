# 02. JSX의 기본 규칙 알아보기

---

## JSX란?

얼핏 보기에는 HTML 생겼지만 사실은 자바스크립트이다.

이는 Babel이라는 도구를 사용해서 XML형태 코드가 Javascript 코드로 변환이 되는것이다.

### 리액트에서 사용되는 JSX 규칙

- 첫번째! 태그는 반드시 닫혀있어야 한다. (XML문법) 셀프 클로징 태그를 사용해서 닫아준다!

```jsx
import React from 'react';
import Hello from './Hello.js';

function App() {
  return (
    <div>
      <Hello />
      <Hello />
      <Hello />
      <input></input> /*
      <input />
      */
      <br></br> /*
      <br />
      */
    </div>
  );
}

export default App;
```

- 두번째! 두개 이상의 태그는 꼭 하나의 태그로 감싸져있어야 한다.

단순히 태그가 두개있다고해서 div를 사용해서 감싸는것이 좋은 방안은아니다.

이것을 보완하기위해 **Fragment를 사용**한다. `<></>`

이떄 괄호 `()`는 가독성 측면에서 사용된다.

```jsx
import React from 'react';
import Hello from './Hello.js';

function App() {
  return (
    <>
      <Hello />
      <div>안녕히 계세요</div>
    </>
  );
}

export default App;
```

### JSX내부에서 javascript 값을 사용하는 방법

- JSX내부에서 javascript 값을 사용하는 방법은 `{}` 중괄호를 이용해서 감싸주면된다.

```jsx
import React from 'react';
import Hello from './Hello.js';

function App() {
  const name = 'react';
  return (
    <>
      <Hello />
      <div>{name}</div>
    </>
  );
}

export default App;
```

### style 과 className을 설정하는 방법

HTML에서 인라인스타일을 설정할떄는 문자열을 이용한다.

JSX에서는 조금다르다 객체를 만들어주어야하는데 아래 예시를 확인해보자.

```jsx
import React from 'react';
import Hello from './Hello.js';

function App() {
  const name = 'react';
  const style = {
    backgroundColor: 'black',
    color: 'aqua',
    fontSize: 24,
    padding: '1rem', //기본값은 px로 저장된다. 단위를 따로 설정하고 싶다면 문자열로 단위지정
  };
  return (
    <>
      <Hello />
      <div style={style}>{name}</div>
    </>
  );
}

export default App;
```

위와같이 `-` 로 구분지어 놓았던 이름들은 카멜케이스 스타일로 네이밍을 해주어야합니다.

class이라고 불리었던 CSS selector가 JSX문법에서는 **className**이라는 이름을 사용한다.

```jsx
import React from 'react';
import Hello from './Hello.js';
import './App.css';

function App() {
  const name = 'react';
  const style = {
    backgroundColor: 'black',
    color: 'aqua',
    fontSize: 24,
    padding: '1rem',
  };
  return (
    <>
      <Hello />
      <div style={style}>{name}</div>
      <div className="gray-box"></div>
    </>
  );
}

export default App;
```

위와 같이 작성하면 `./App.css` 에서 만든 css스타일이 작성된다.

### JSX에서 주석처리 하는 방법

javascript 와 다르게 JSX에서는 HTML 주석처리 방법 + {} 로를 해주어야 주석처리가 된다.

```jsx
import React from 'react';
import Hello from './Hello.js';
import './App.css';

function App() {
  const name = 'react';
  const style = {
    backgroundColor: 'black',
    color: 'aqua',
    fontSize: 24,
    padding: '1rem',
  };
  return (
    <>
      {/* 주석 */}
      <Hello
      // 이런식으로도 주석처리가 가능
      />
      <div style={style}>{name}</div>
      <div className="gray-box"></div>
    </>
  );
}

export default App;
```

**오늘의 핵심정리**

![Untitled jpg](https://user-images.githubusercontent.com/66991380/102222845-4fcc5e00-3f27-11eb-9a27-ef537845c93f.png)

![Untitled1](https://user-images.githubusercontent.com/66991380/102222851-50fd8b00-3f27-11eb-8a41-7823afb1118e.jpg)

![Untitled2](https://user-images.githubusercontent.com/66991380/102222854-51962180-3f27-11eb-88a2-673c81fe0044.jpg)

![Untitled3](https://user-images.githubusercontent.com/66991380/102222856-522eb800-3f27-11eb-8e9c-03baa8120477.jpg)
