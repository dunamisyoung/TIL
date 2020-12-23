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

export default const Mycomponent = 'hello';
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

이런식으로 React가 **사용자 정의 컴포넌트로 작성한 엘리먼트 발견하면** JSX 어트리뷰트와 자식을 해당 컴포넌트에 단일 객체로 전달하는데 이것을 **props**라고 한다.

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
