# useState를 통해 컴포넌트에서 바뀌는 값 관리하기

---

지금까지 우리가 리액트 컨포넌트를 만들떄는 동적인 부분이 하나도 없었지만, 컨포넌트에서 보여지는 내용이 사용자 인터렉션에 따라 바뀌어야할때 어떻게 구현할수 있는지에 대해 알아봅시다.

React 16.8v 이전에는 함수형 컨포넌트에서 상태관리가 되지 않았습니다. 하지만 16.8v 이후 **HOOKs** 라는 기능이 도입되면서 **함수형 컨포넌트에서도 상태를 관리할수 있게 되었다.** **useState**라는 함수를 사용해봅시다. 이것은 React의 HOOKs중 하나입니다.

먼저 Counter.js 라는 파일을 만든다. 그리고 아래와 같이 작성한다.

```jsx
//Counter.js
import React from 'react';

function Counter() {
  return (
    <div>
      <h1>0</h1>
      <button>+1</button>
      <button>-1</button>
    </div>
  );
}

export default Counter;
```

기존 App.js에 있던 컨포넌트를 지워준다.

```jsx
//App.js
import React from 'react';
import Counter from './counter.js';

function App() {
  return <Counter />;
}

export default App;
```

Counter 컨포넌트에서 버튼이 클릭되는 이벤트가 발생했을때 특정 함수가 호출되도록 설정해보자.

버튼을 클릭했을때 함수가 실행되게끔 하려면 onClick이벤트를 설정해주어야하고, **이벤트핸들러에 카멜케이스**를 이용해 적어주어야한다.

```jsx
import React from 'react';

function Counter() {
  const onIncrease = () => {
    console.log('+1');
  };

  const onDecrease = () => {
    console.log('-1');
  };

  return (
    <div>
      <h1>0</h1>
      <button onClick={onIncrease}>+1</button>
      <button onClick={onDecrease}>-1</button>
    </div>
  );
}

export default Counter;
```

이벤트를 설정할때 주의할점은, 함수를 넣어주어야하는것이지 함수를호출하게되면 안됩니다. 만약 호출문을 작성하게되면, 리액트 컴포넌트가 렌더링될때 값이 출력이 된다.

### 동적인 상태 추가하기 useState

이제 컴포넌트에 동적인 상태를 추가해보겠습니다. 아래와 같이 useState라는 함수를 리액트에서 가져와줍니다.

```jsx
import React, { useState } from 'react';

function Counter() {
  const [number, setNumber] = useState(0); //number 라는 상태의 값을 0으로 설정
  /*
	위 코드와 동일한 상태입니다.
	const numberState = useState(0);
	const number = numberState[0];
	const setNumber = numberState[1];
*/
  const onIncrease = () => {
    console.log('+1');
  };

  const onDecrease = () => {
    console.log('-1');
  };

  return (
    <div>
      <h1>0</h1>
      <button onClick={onIncrease}>+1</button>
      <button onClick={onDecrease}>-1</button>
    </div>
  );
}

export default Counter;
```

useState함수는 배열을 반환하게 되는데 첫번째 원소로는 number를 두번째 원소로는 setNumber를 추출해줍니다.

setNumber함수를 이용해서 number의 값을 업데이트 해줍시다.

즉, **useState 함수를 이용해서 바뀌는 값을 관리** 할수 있게되고, **기본값은 함수의 파라미터로 전달**하면됩니다. useState 함수는 배열을 반환하는데 **첫번째 요소는 현재상태**, **두번째 요소는 상태를 변경하는 함수**가 있습니다. 이것을 업데이터 함수라고 합니다.

```jsx
import React, { useState } from 'react';

function Counter() {
  const [number, setNumber] = useState(0);
  const onIncrease = () => {
    setNumber(number + 1); // click 하면 1씩 증가
  };

  const onDecrease = () => {
    setNumber(number - 1); // click 하면 1씩 감소
  };

  return (
    <div>
      <h1>{number}</h1>
      <button onClick={onIncrease}>+1</button>
      <button onClick={onDecrease}>-1</button>
    </div>
  );
}

export default Counter;
```

업데이터 함수를 이용해 현재상태를 가져와서 업데이트 하겠다~ 라는 함수를 정의해줄수있습니다.

이것은 리액트 컴포넌트 최적화와 관련이 있습니다. 추후에 더 알아보도록 합시다.

```jsx
import React, { useState } from 'react';

function Counter() {
  const [number, setNumber] = useState(0);
  const onIncrease = () => {
    setNumber((prevNumber) => prevNumber + 1); // click 하면 1씩 증가
  };

  const onDecrease = () => {
    setNumber((prevNumber) => prevNumber - 1); // click 하면 1씩 감소
  };

  return (
    <div>
      <h1>{number}</h1>
      <button onClick={onIncrease}>+1</button>
      <button onClick={onDecrease}>-1</button>
    </div>
  );
}

export default Counter;
```
