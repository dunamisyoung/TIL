# input 상태 관리하기

---

리액트에서 input 상태 관리하기

새롭게 InputSamle.js 파일을 만들어주고 아래와 같이 파일을 만들어 줍니다.

```jsx
// InputSample.js
import React from 'react';

function InputSample() {
  return (
    <div>
      <input />
      <button>초기화</button>
      <div></div>
      <b>값 :</b>
      어쩌고 저쩌고..
    </div>
  );
}

export default InputSample;
```

기존 App.js에서 Counter 컨포넌트 import 명령을 지워주고 InputSample을 가져와줍니다.

```jsx
// App.js
import React from 'react';
import InputSample from './InputSample';

function App() {
  return <InputSample />;
}

export default App;
```

input에 입력한 값이 HTML 파일에 실시간으로 랜더링되고, 초기화버튼을 누르면 text값이 사라지는 설정을 구현 해봅시다.

먼저 onChange라는 이름으로 함수를 만들어줍니다. 그리고는 input에 onChange이벤트가 발생했을떄 함수가 호출되도록 입력해줍니다.

```jsx
// InputSample.js
import React from 'react';

function inputSample() {
  const onChange = (e) => {
    console.log(e.target);
  }; // e.target은 현재 이벤트가 발생한 DOM에대한 정보를 가지고 있습니다.

  return (
    <div>
      <input onChange={onChange} />
      <button>초기화</button>
      <div></div>
      <b>값 :</b>
      어쩌고 저쩌고..
    </div>
  );
}

export default inputSample;
```

우리가해야하는 작업은 useState함수를 이용해 input 값을 관리할 상태를 만들어줍니다.

그리고 useState 함수를 이용해 배열디스트럭쳐링 할당으로 text, setText라는 변수에 빈문자열로 초기값을 설정해줍니다.

```jsx
// InputSample.js
import React, { useState } from 'react';

function InputSample() {
  const [text, setText] = useState('');

  const onChange = (e) => {
    console.log(e.target.value);
  };

  return (
    <div>
      <input onChange={onChange} />
      <button>초기화</button>
      <div></div>
      <b>값 :</b>
      어쩌고 저쩌고..
    </div>
  );
}

export default InputSample;
```

그리고는 console.log 대신에 setText안에 onChange이벤트가 발생하면 useState의 첫번쨰인수인 text의 값을 변경할수 있게 e.target.value를 전달합니다. 그리고 어쩌고 저쩌고 라고 써있던 문자를 `{text}` 로 바꿔줍니다.

```jsx
// InputSample.js
import React, { useState } from 'react';

function InputSample() {
  const [text, setText] = useState('');

  const onChange = (e) => {
    setText(e.target.value);
  };

  return (
    <div>
      <input onChange={onChange} value={text} />
      <button>초기화</button>
      <div></div>
      <b>값 :</b>
      {text}
    </div>
  );
}

export default InputSample;
```

이때 새로고침후에 빈문자열이 나오게끔 하려면 <input value={text} /> 라고 적어주어야합니다. 이것은 다른 곳에서 setText를 이용해 값의 변경이 일어났을때 input 요소에 text 값도 변경되게끔 하기 위해서입니다.

새롭게 초기화 버튼을 구현하기 위해서 onReset이라는 함수를 만들어줍니다. 그리고 버튼의 onClick 이벤트에 연결해줍니다.

```jsx
import React, { useState } from 'react';

function InputSample() {
  const [text, setText] = useState('');

  const onChange = (e) => {
    setText(e.target.value);
  };

  const onReset = () => {
    setText('');
  };

  return (
    <div>
      <input onChange={onChange} />
      <button onClick={onReset}>초기화</button>
      <div></div>
      <b>값 :</b>
      {text}
    </div>
  );
}

export default InputSample;
```
