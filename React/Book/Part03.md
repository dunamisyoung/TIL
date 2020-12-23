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
