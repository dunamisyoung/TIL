# 04. 조건부 렌더링

---

조건부 렌더링이란 특정조건을 설정하고, 참인지 거짓인지를 확인해서 다른 결과물을 보여주는것을 의미합니다.

Hello 컨포넌트에게 isSpecial이라는 Props를 설정하고 값을 true로 설정했습니다.

```jsx
// App.js
import React from 'react';
import Hello from './Hello.js';
import Hello from './Wrapper.js';

function App() {
  return (
    <Wrapper>
      <Hello name="react" color="red" isSpecial={true} />
      <Hello color="pink" />
    </Wrapper>
  );
}

export default App;
```

Hello.js에서 App.js 에서 받아온 props인 isSpecial 이라는 Props값을 가져옵니다.

이렇게 받아온 값을 삼항조건연산자를 이용해 조건을 만들어 봅니다.

```jsx
// Hello.js
import React from 'react';

function Hello({ color, name, isSpecial }) {
  return (
    <div
      style={{
        color,
      }}
    >
      {isSpecial ? <b>*</b> : null} /*isSpecial 값이 true면 Hello컨포넌트에 * 렌더링*/ 안녕하세요 {name}
    </div>
  );
}

Hello.defaultProps = {
  name: '이름없음',
};

export default Hello;
```

추가적으로 **JSX에서 null, false, undefined 를 렌더링 한다던지 하면 아무것도 나타나지 않습니다.**

즉, **falsy한 값은 아무것도 나타나지 않지만 숫자 0은 예외적으로 화면에 출력**됩니다.

보통의 삼항조건연산자를 사용하는 이유는 내용이 달라질때 예를들어

`<b>{isSpecial? '스페셜' : '낫스페셜' }</b>` 이렇게 조건에 따라 다른내용이 보여져야할때 사용하게 되는데 지금 상황은 숨기거나 보여주거나를 하고있습니다. 이런 상황에서는 `&&` 연산자를 넣어주는것이 더 좋습니다.

```jsx
// Hello.js
import React from 'react';

function Hello({ color, name, isSpecial }) {
  return (
    <div
      style={{
        color,
      }}
    >
      {isSpecial && <b>*</b>} /*isSpecial 값이 true면 Hello컨포넌트에 * 렌더링*/ 안녕하세요 {name}
    </div>
  );
}

Hello.defaultProps = {
  name: '이름없음',
};

export default Hello;
```

즉, 단순히 보여주거나 숨기거나 할경우에는 `&&` 연산자를 사용하는것이 조금더 유용하고, 조건에 따라 내용이 다르게 보여야 하는경우에는 삼항조건연산자를 사용하는것이 좋습니다.

또한, 아래의 Hello 컨포넌트를 보면 `isSpecial={true}` 가 아닌 isSpecial 이라고썻는데 이경우 `isSpecial={true}` 와 동일한 효과를 가져옵니다. 불리언 값을 설정할때 유용하게 사용할수있도록 합시다.

```jsx
// App.js
import React from 'react';
import Hello from './Hello.js';
import Hello from './Wrapper.js';

function App() {
  return (
    <Wrapper>
      <Hello name="react" color="red" isSpecial />
      <Hello color="pink" />
    </Wrapper>
  );
}

export default App;
```
