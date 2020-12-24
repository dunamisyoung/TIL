# 3. 컴포넌트

**`이곳은 중요하다고 생각하는 개념들, 흩어진 개념들의 집합소 입니다.` :)**

---

컴포넌트의 선언 방식 클래스형 컴포넌트, 함수형컴포넌트로 두가지 이다.

## 3.1 클래스형 컴포넌트

---

### 클래스형 컴포넌트

```jsx
//App.js
import React, { Component } from 'react';

class App extends Component {
  render() {
    const name = 'react';
    return <div className="react">{name}</div>;
  }
}

export default App;
```

클래스형 컴포넌트의 역할은 이전 함수형 컴포넌트와 같다. 차이점은 **state기능 및 라이프사이클 기능을 사용할수 있다는 점**과, 임의 메서드정의가 가능하다는것이다.

### render의 유무

클래스형 컴포넌트에서는 render 함수가 꼭 있어야하며, UI로 보여주어야할 JSX를 반환해야한다.

### 함수형컴포넌트를 써야하나?

함수형 컴포넌트의 장점

- 클래스형 컴포넌트보다 선언하기 편하다.
- 메모리자원도 덜 사용한다.
- 프로젝트 완성후 빌드하여 배포시에 결과물의 용량이 작다.

함수형 컴포넌트의 단점

- state와 라이프사이클 API의 사용불가

### v16.8 Update → Hooks

함수형 컴포넌트의 단점을 보완해줄 **Hooks라는 기능이 도입**됨으로 함수형 컴포넌트에서도 클래스 컴포넌트의 기능을 사용할수 있게됨.

---

## 3.2 함수형 컴포넌트로 코드작성

---

```jsx
import React from 'react';
```

CRA을할때 같이 다운로드된 모듈 파일 안에 있는 React의 기능을 불러와 사용하겠다 라는뜻.

### 화살표 함수로 함수형 컴포넌트 만들기

```jsx
import React from 'react';

const MyCompoent = () => {
  return <div>나의 새롭고 멋진 컴포넌트</div>;
};

export default MyComponent;
```

화살표 함수를 통한 컴포넌트 작성은 **함수를 파라미터로 전달할때 유용하게 쓰인다.** 또한 일반함수로 호출되는 this의 값은 전역을 가르키게 되는데 이때 화살표 함수를 이용하면, 자신의 상위 스코프의 this값을 가지게 됨으로 this바인딩의 문제를 해결할 수 있게 도와준다.

## default export & named export

### default export

```jsx
export default MyComponent;
```

- default로 선언된 모듈은 하나의 파일에서 **단 한개의 변수 또는 클래스 등을 export 할수 있다.**
- default로 선언된 모듈을 import 할때는 **어떤이름으로든 import가 가능**하다.
- 단 var, let, const 를 바로 export default 할수 없다.

즉 아래와 같다.

```jsx
import Mycomponent from './Mycomponent';
import anything from './Mycomponent';

export default const Mycomponent = 'hello'; // 이건 안되요
```

### named export

```jsx
export class MyFirstClass {}
export class MySecondClass {}
```

- named로 선언된 모듈은 하나의 파일에서 **여러 변수 클래스 등을 export 할수 있다.**
- **다만 import 시 `{}` 안에 export된 이름과 동일하게 설정 해야한다.**
- 다른 이름으로 import 할때에는 `as`를 사용해야한다.

```jsx
import { MyFirstClass as anything } from './Mycomponent';
```

- `*as` 를사용하면 한 파일에 있는 클래스, 변수들을 한번에 import 가능하다. 하지만 import 했을때 Hello.Mycomponent 이런식으로 사용해야한다.

```jsx
import * as Hello from './Mycomponent';
```

**_named export는 여러값을 내보낼때 유용하고, 가져올때는 내보낼때와 동일한 이름을 사용하거나 `import {name as newName} 구문을 사용해야한다. 반면 default export는 어떤이름으로도 가져올수 있다._**

[default export와 named export 차이점](https://medium.com/@_diana_lee/default-export%EC%99%80-named-export-%EC%B0%A8%EC%9D%B4%EC%A0%90-38fa5d7f57d4)

---

## 3.3 Props

---

**props**는 poroperties를 줄인 표현으로 **컴포넌트 속성을 설정할때 사용하는 요소**이며 props 값은 해당 컴포넌트를 불러와 사용하는 부모 컴포넌트에서 설정가능하다.

### JSX 내부에서 props 렌더링

MyComponent를 수정하여 해당 컴포넌트에서 name이라는 props를 렌더링 하도록하자.

```jsx
//MyComponent.js
import React from 'react';

const MyComponent = (props) => {
  return <div>안녕하세요, 제 이름은 {props.name}입니다. </div>;
};

export default MyComponent;
```

App컴포넌트에서 MyComponent의 props 값을 지정해보자.

```jsx
//App.js
import React from 'react';
import MyComponent from './MyComponent';

const App = () => {
  return <MyComponent name="React" />;
};

export default App;
```

이런식으로 React가 **사용자 정의 컴포넌트로 작성한 엘리먼트를 발견하면** JSX 어트리뷰트와 자식을 해당 컴포넌트에 단일 객체로 전달하는데 이것을 **props**라고 한다.

### defaultProps

App.js 에서설정한 name 값을 지우고 MyComponent로 이동해서 defaultProps를 설정해보자.

```jsx
//MyComponent.js
import React from 'react';

const MyComponent = (props) => {
  return <div>안녕하세요, 제 이름은 {props.name}입니다. </div>;
};

MyComponent.defaultProps = {
  name: '기본 값',
};

export default MyComponent;
```

이처럼 defaultProps는 `컴포넌트명.defaultProps`으로 정의할 수 있으며 부모 컴포넌트에서 해당컴포넌트의 JSX 어트리뷰트와 자식을 정의하지 않았을때 기본값을 설정할수 있게 해줍니다.

### children

사용자 정의 컴포넌트를 사용할때 **태그사이의 내용**을 보여주는 props를 **children**이라고 하며, 태그사이의 내용에 접근하려면 props.children을 사용합니다.

```jsx
//App.js
import React from 'react';
import MyComponent from './MyComponent';

const App = () => {
  return <MyComponent>리액트</MyComponent>;
};

export default App;
```

Props는 항상 부모에서 자식으로 전달된다.

사용자정의 컴포넌트의 JSX 어트리뷰트 → 해당컴포넌트의 props 객체로 전달

```jsx
//MyComponent.js
import React from 'react';

const MyComponent = props => {
	return (
		<div>
			안녕하세요, 제 이름은 {props.name}입니다. <br />
			children 값은 {props.children} 입니다.
		</div>;
	);
};

MyComponent.defaultProps = {
	name: '기본 값'
}

export default MyComponent;
```

### 디스트럭쳐링 할당을 통한 props 값 추출

MyComponent에서 props 값을 조회할때 `props.name` , `props.children` 처럼 props.라는 키워드를 붙여주게 되는데 이때 ES6 디스트럭쳐링 할당을 통해 간결하게 사용할수 있다.

```jsx
import React from 'react';

const MyComponent = ({ name, children }) => {
	return (
		<div>
			안녕하세요, 제 이름은 {name}입니다. <br />
			children 값은 {children} 입니다.
		</div>;
	);
};

MyComponent.defaultProps = {
	name: '기본 값'
}
```

### propTypes를 통한 props검증

컴포넌트의 필수 props를 지정하거나. props의 타입을 지정할때 **propTypes**가 사용된다.

컴포넌트의 propTypes를 지정하는 것은 defaultProp을 설정하는것과 비슷하며 propTypes 사용시에는 코드상단에 `import PropTpes from 'prop-types'` 를사용하여 불러와야 한다.

```jsx
//MyComponent.js
import React from 'react';
import PropTypes from 'prop-types';

const MyComponent = ({ name, children }) => {
	return (
		<div>
			안녕하세요, 제 이름은 {name}입니다. <br />
			children 값은 {children} 입니다.
		</div>;
	);
};

MyComponent.defaultProps = {
	name: '기본 값'
}

MyComponent.propTypes = {
	name : PropTypes.string
};

export default MyComponent;
```

이런식으로 설정시 name 값은 무조건 문자열 형태로 전달된다. 즉, 부모컴포넌트에서 사용자 정의 컴포넌트에 props의 값을 숫자로 전달해도 해당컴포넌트에서 props를 조회하면 문자열로 변환되야 하기에 오류가 발생한다.

즉, 해당 컴포넌트에서 설정한 **`PropTypes.데이터타입`** 이 부모에게서 전달된 props 보다 우선순위에 있다고 판단된다. propTypes 설정시 부모요소에서 전달되는 dataType과 **propTypes.데이터타입**을 잘 확인할수 있도록하자.

### isRequired를 사용한 필수 propTypes 설정

propTypes를 지정하지 않았을 경우 경고 메시지를 띄워 주려면, **`propTypes.데이터타입.isRequired`** 이런식으로 설정 해주면 된다.

예를 들어보자 favoriteNumber 라는 숫자를 필수 props로 설정하려면 아래와 같이 작성하면된다.

```jsx
//MyComponent.js
import React from 'react';
import PropTpes from 'prop-types';

const MyComponent = ({ name, children , favoriteNumber }) => {
	return (
		<div>
			안녕하세요, 제 이름은 {name}입니다. <br />
			children 값은 {children} 입니다.
			<br />
			제가 좋아하는 숫자는 {favoriteNumber} 입니다.
		</div>;
	);
};

MyComponent.defaultProps = {
	name: '기본 값'
}

MyComponent.propTypes = {
	name : PropTypes.string,
	favoriteNumber : PropTypes.string.isRequired
};

export default MyComponent;
```

위와 같이 설정했을때 부모 컴포넌트에서 props를 전달하지 않았다면 경고가 나타날 것이다.

### 다양한 PropTypes 종류

- array
- arrayOf
- bool
- func
- number
- object
- string
- symbol
- node
- insanceOf
- oneOf
- oneOfType
- objectOf
- shape
- any

자세한 propTypes 정보는 [https://github.com/facebook/prop-types](https://github.com/facebook/prop-types)서 확인해보자 😉

### 클래스형 컴포넌트에서 props 사용하기

클래스형 컴포넌트에서 props를 사용하게된다면 render 함수 내에서 this.props를 조회해야된다. defaultProps와 propTypes는 함수형 컴포넌트와 동일하게 설정할수 있다.

```jsx
//MyComponent.js
import React { Component } from 'react';
import PropTpes from 'prop-types';

class MyComponent extends Component {
	render() {
		const { name, children , favoriteNumber } = this.props;
		return (
			<div>
				안녕하세요, 제 이름은 {name}입니다. <br />
				children 값은 {children} 입니다.
				<br />
				제가 좋아하는 숫자는 {favoriteNumber} 입니다.
			</div>;
		);
	};
};

MyComponent.defaultProps = {
	name: '기본 값'
}

MyComponent.propTypes = {
	name : PropTypes.string,
	favoriteNumber : PropTypes.string.isRequired
};

export default MyComponent;
```

클래스형 컴포넌트에서 defaultProps와 propTypes를 class내부에서 지정도 가능하다.

```jsx
//MyComponent.js
import React { Component } from 'react';
import PropTpes from 'prop-types';

class MyComponent extends Component {
	static defaultProps = {
	name: '기본 값'
	};

	static.propTypes = {
	name : PropTypes.string,
	favoriteNumber : PropTypes.string.isRequired
	};

	render() {
		const { name, children , favoriteNumber } = this.props;
		return (
			<div>
				안녕하세요, 제 이름은 {name}입니다. <br />
				children 값은 {children} 입니다.
				<br />
				제가 좋아하는 숫자는 {favoriteNumber} 입니다.
			</div>;
		);
	};
};

export default MyComponent;
```

---

## 3.4 State

리액트에서 **state**는 컴포넌트 내부에서 **바뀔수 없는 값을 의미하며** state는 클래스형 컴포넌트의 state가 있고, 함수형 컴포넌트의 useState라는 함수를 통해 사용하는 state 두가지가 존재한다.

### 클래스형 컴포넌트의 state

```jsx
// Counter.js
import React, { Component } from 'react';

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = {
      number: 0,
    };
  }
  render() {
    const { number } = this.state;
    return (
      <div>
        <h1>{number}</h1>
        <button
          onClick={() => {
            this.setState({ number: number + 1 });
          }}
        >
          +1
        </button>
      </div>
    );
  }
}

export default Counter;
```

클래스형 컴포넌트에 state를 설정할때 constructor 메서드를 작성하여 설정했다.

이는 컴포넌트의 생성자 메서드로써 클래스 컴포넌트에서 **constructor를 작성할때는 반드시 super(props)를 호출해야한다**. 이 함수가 호출되면 현재 클래스형 컴포넌트가 상속받는 Component 클래스가 지닌 생성자 함수를 호출해준다.

this.state의 초기값은 객체 형식이어야한다. 또한, this.setState를 이용해 state에 새로운 값을 넣을수 있다.

```jsx
···
 render() {
    const { number } = this.state;
    return (
      <div>
        <h1>{number}</h1>
        <button
          onClick={() => {
            this.setState({ number: number + 1 });
          }}
        >
          +1
        </button>
      </div>
    );
  }
}
export default Counter;
```

render 함수에서 현재 state를 조회하고 싶다면 this.state를 조회하면된다. **이벤트로 설정할 함수**를 넣어줄때 **화살표 함수 문법을 사용**해 넣어주어야한다. [이는 React가 기본적으로 stricmode로 실행되기에 일반함수로 호출된 this는 undefined를 출력한다.](https://blueshw.github.io/2017/07/01/arrow-function/)

### state 객체안에 여러 값이 있을떄

```jsx
// Counter.js
import React, { Component } from 'react';

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = {
      number: 0,
      count: 0,
    };
  }
  render() {
    const { number, count } = this.state;
    return (
      <div>
        <h1>{number}</h1>
        <h2>카운트 : {count}</h2>
        <button
          onClick={() => {
            this.setState({ number: number + 1 });
          }}
        >
          +1
        </button>
      </div>
    );
  }
}

export default Counter;
```

state 객체 안에는 여러값이 있을수 있다. this.setState 함수는 인자로 전달된 객체 안에 들어있는 값만 바꾸어준다. 즉, onClick 이벤트가 발생하여도, this.setState 함수의 인자로 전달된 객체만 바꾸기에 count 값은 변하지 않는다.

### state를 constructor에서 꺼내기

state의 초기값 설정에 있어서 기존에는 constructor 메서드를 선언 해주고, super를 호출했었지만, 다른 방식으로도 state의 초기값을 지정할수 있다.

```jsx
// Counter.js
import React, { Component } from 'react';

class Counter extends Component {
  state = {
    number: 0,
    count: 0,
  };
  render() {
    const { number, count } = this.state;
    return (
      <div>
        <h1>{number}</h1>
        <h2>카운트 : {count}</h2>
        <button
          onClick={() => {
            this.setState({ number: number + 1 });
          }}
        >
          +1
        </button>
      </div>
    );
  }
}

export default Counter;
```

### this.setState에 객체 대신 함수인자 전달하기

this.setState를 사용해 state값을 업데이트 할때 상태는 비동기적으로 업데이트된다. 이때 onClick에 설정한 함수 내부에서 this.setState를 두번 호출하면 어떻게될까?

```jsx
<button
  onClick={() => {
    this.setState({ number: number + 1 });
    this.setState({ number: this.state.number + 1 });
  }}
>
  +1
</button>
```

위에서 말했던것처럼 [this.setState를 사용하여 값을 업데이트할때는 비동기적으로 동작](https://velog.io/@cada/React%EC%9D%98-setState%EA%B0%80-%EC%9E%98%EB%AA%BB%EB%90%9C-%EA%B0%92%EC%9D%84-%EC%A3%BC%EB%8A%94-%EC%9D%B4%EC%9C%A0)하기에 만약 이를 해결하고 싶다면 this.setState를 사용시 함수를 인자로 전달하면된다.

```jsx
import React, { Component } from 'react';

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = {
      number: 0,
    };
  }
  render() {
    const { number } = this.state;
    return (
      <div>
        <h1>{number}</h1>
        <button
          onClick={() => {
            this.setState((prevState, props) => ({ number: prevState.number }));
          }}
        >
          +1
        </button>
      </div>
    );
  }
}

export default Counter;
```

만약 업데이트 하는 과정에서 props가 필요하지 않다면 생략 가능하다.

### this.setState가 끝난후 특정작업 실행

setState를 사용하여 값을 업데이트 하고난후 어떠한 작업을 하고싶다면 setState의 두번째 파라미터로 콜백함수를 전달하면된다.

```jsx
import React, { Component } from 'react';

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = {
      number: 0,
    };
  }
  render() {
    const { number } = this.state;
    return (
      <div>
        <h1>{number}</h1>
        <button
          onClick={() => {
            this.setState({ number: prevState.number }, () => {
              console.log('setState 호출됨');
            });
          }}
        >
          +1
        </button>
      </div>
    );
  }
}

export default Counter;
```

## 함수형 컴포넌트에서의 useState 사용

리액트 v16.8 이후 도입된 useState 함수를 통해 함수형 컴포넌트에서의 state관리가 가능해졌는데 이 useState는 Hooks중 하나이며, 기존 클래스형 컴포넌트의 state 사용법과는 조금 다르다.

```jsx
// Say.js
import { useState } from 'react';

const Say = () => {
  const [message, setMessage] = useState('');

  const onClickEnter = () => setMessage('안녕하세요!');
  const onClickLeave = () => setMessage('안녕히 가세요!');

  return (
    <div>
      <button onClick={onClickEnter}>입장</button>
      <button onClick={onClickLeave}>퇴장</button>
      <h1>{message}</h1>
    </div>
  );
};

export default Say;
```

기존 클래스형 컴포넌트에서 "state 초기값 설정시 객체 형태는 넣어주어야 한다" 라고 배웠지만, 함수형 컴포넌트의 **useState에서는 값의 형태가 자유로울수있다**. useState를 호출하면 **배열이 반환**되고, 이 배열의 <u>첫쨰 원소는 현재상태</u>, <u>두번쨰 원소는 상태변경 함수 혹은 세터함수(setter function)</u> 라고한다.

### 한 컴포넌트에서 useState 여러번 사용하기

```jsx
import { useState } from 'react';

const Say = () => {
  const [message, setMessage] = useState('');

  const onClickEnter = () => setMessage('안녕하세요!');
  const onClickLeave = () => setMessage('안녕히 가세요!');

  const [color, setColor] = useState('black');

  return (
    <div>
      <button onClick={onClickEnter}>입장</button>
      <button onClick={onClickLeave}>퇴장</button>
      <h1 style={{ color }}>{message}</h1>
      <button style={{ color: 'red' }} onClick={() => setColor('red')}>
        빨간색
      </button>
      <button style={{ color: 'green' }} onClick={() => setColor('green')}>
        초록색
      </button>
      <button style={{ color: 'blue' }} onClick={() => setColor('blue')}>
        파란색
      </button>
    </div>
  );
};

export default Say;
```
