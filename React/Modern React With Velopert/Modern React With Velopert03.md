# 03. Props 를 통해 컴포넌트에게 값 전달하기

---

### Props의 기본적인 사용법

**Props**는 Properties의 줄임말입니다. Props는 컨포넌트를 사용하면서 **특정값을 전달하게될때 사용**하게됩니다.

예를들어 Hello 컴포넌트만 render 한다고 하면

```jsx
// App.js
import React from 'react';
import Hello from './Hello.js';

function App() {
  return <Hello />;
}

export default App;
```

Hello 컴포넌트에는 이런식으로 작성이 되어있을것이고,

```jsx
// Hello.js
import React from 'react';

function Hello() {
  return (
	   </div>안녕하세요</div>
  );
}

export default Hello;
```

이에따라 화면에는 **안녕하세요** 라는 글씨가 랜더링 될것입니다.

App.js에서 Hello 컴포넌트에게 `name:'react'` 라는 값을 전달하였다고 했을떄 이는 객체형태로 props라는 매개변수로 전달됩니다.

```jsx
// Hello.js
import React from 'react';

function Hello(props) {
	console.log(props) // name:'react'
  return (
	   </div>안녕하세요</div>
  );
}

export default Hello;
```

여기서 `react` 라는 값을 Hello라는 컴포넌트에 보여주고 싶다면 아래와 같이 중괄호로 감싸 JSX 문법으로 표현해줍니다.

```jsx
// Hello.js
import React from 'react';

function Hello(props) {
  return (
	   </div>안녕하세요{props.name}</div>
  );
}

export default Hello;
```

또다른 값을 Hello.js에게 전달하고싶다면 App.js에서 아래와같이 설정하고

```jsx
// App.js
import React from 'react';
import Hello from './Hello.js';

function App() {
  return <Hello name="react" color="red" />;
}

export default App;
```

Hello.js 에서 아래와 같이 설정해줍니다. 이때 style 태그 뒤에보이는 중괄호가 2개인 이유는 하나는 **JSX 문법의 중괄호**, 그리고 하나는 **javascript 에서의 객체를 뜻하는 중괄호**이니 햇갈리지 않게 조심해야합니다.

```jsx
// Hello.js
import React from 'react';

function Hello(props) {
  return (
    <div
      style={{
        color: props.color,
      }}
    >
      안녕하세요{props.name}
    </div>
  );
}

export default Hello;
```

이렇게해주면 빨간 글씨로 `안녕하세요 react` 라고 나오게됩니다.

이때 `props.` 이 중복되니 객체 디스트럭쳐링 할당을통해 깔끔하게 만들어줍니다.

```jsx
// Hello.js
import React from 'react';

function Hello({color , name}) {
  return (
	  </div style={{
			color // 객체 디스트럭쳐링 + 프로퍼티키 축약표현
		}}>안녕하세요{name}</div>
  );
}

export default Hello;
```

### props의 기본값 설정

만약 props의 기본값을 주고싶다면 Hello.js에서 아래와같이

**컨포넌트명.defaultProps**를 입력해 기본값을 설정할수 있습니다.

```jsx
// Hello.js
import React from 'react';

function Hello({color , name}) {
  return (
	  </div style={{
			color // 객체 디스트럭쳐링 + 프로퍼티키 축약표현
		}}>안녕하세요{name}</div>
  );
}

Hello.defaultProps ={
	name: '이름없음'
}

export default Hello;
```

이런식으로 작성해 준다면, **Hello.js 컨포넌트를 import 하고있는 App.js 에서 기본값이 설정되어 나타나게됩니다.**

### Props.children이란?

일반적으로 우리는 `</div>안녕하세요</div>` 이런식으로 코드를 작성하는데 이것이 만약 div가 아닌 **사용자 정의 컴포넌트 였을경우**에 안녕하세요 라는 text가 위치한곳에 접근하기 위해서 **props.children을 사용**합니다.

새롭게 Wrapper.js라는 컨포넌트를 만들어줍니다.

```jsx
//Wrapper.js
import React from 'react';

function Wrapper () {
	const style = {
		border : '2px solid black'
		padding : 16
	}

	return <div style={style}></div>
};

export default Wrpper;
```

이때 App.js에서 import 받았을때 화면에 아무것도 보이지 않는데, 이럴때 Wrpper.js 에서 children을 사용하면됩니다.

```jsx
//Wrapper.js
import React from 'react';

function Wrapper ({children}) {
	const style = {
		border : '2px solid black'
		padding : 16
	}

	return <div style={style}>{children}</div>
};

export default Wrpper;
```

즉 App.js에 `<Wrapper></Wrapper>` 안에있던 JSX 문법을 가져와서 render 시킨것입니다.

지금까지 배운것을 정리해보자면,

- **사용자 정의 컨포넌트에 어트리뷰트형태로 정의되어있는 값들이 Props**이고 각 컨포넌트들이 매개변수를 통해 props를 가져와 사용할수 있습니다.
- **컨포넌트명.defaultProps** 를통해 Props의 기본값을 설정할수있습니다.
- children 이라는 것은 사용자 정의 컨포넌트 사이에 위치하는 내용을 의미한다고 할수있습니다.
