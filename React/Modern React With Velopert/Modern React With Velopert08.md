# useRef 로 특정 DOM 선택하기

---

HTML과 javascript를 사용할 때 특정 DOM 을 선택할 경우네는 getElementById 혹은 querySelctor 과같은 DOM selector함수를 사용해서 DOM 을 선택하게 된다.

## React에서 DOM 선택하기

특정 element의 크기나 위치를 가져와야할 경우, 스크롤바 위치를 설정해야할 경우 등등..

또한 video관련 라이브러리나, 그래프관련 라이브러리를 사용하고자 할떄도 사용하게 된다.

이럴경우 React에서는 **ref** 라는것을 사용한다.

**함수형 컴포넌트**에서 useRef 를 사용할경우에는 **useRef** ,

**클래스형 컴포넌트**에서는 useRef 를 사용할경우에는 **React.createRef()** 를 사용하게된다.

### 함수형 컴포넌트에서 ref 사용하기

기존에 만들어 놓았던 input창에서 text를 추가한 이후 focus 위치를 옮기고 싶다면?

React에서는 딱히 할수 있는것이 없다. 이럴 경우에는 DOM에 직접 접근을 해야한다.

먼저 useRef 를 리액트에서 불러와준다.

그리고는 nameInput 이라는 변수에 useRef 함수의 반환값을 넣어준다.

nameInput 객체를 선택하고 싶은 DOM에 넣어준다.

```jsx
//InputSample.js

import React, { useState, useRef } from 'react'; // 먼저 useRef 를 리액트에서 불러와준다.

function InputSample() {
  const [inputs, setInputs] = useState({
    name: '',
    nickname: '',
  });

  const nameInput = useRef(); // nameInput 이라는 변수에 useRef 함수의 반환값을 넣어준다.
  const { name, nickname } = inputs;

  const onChange = (e) => {
    const { name, value } = e.target;

    setInputs({
      ...inputs,
      [name]: value,
    });

    nameInput.current.focus(); // 이때 **current는** DOM을 가르킨다.
  };

  const onReset = () => {
    setInputs({
      name: '',
      nickname: '',
    });
  };

  return (
    <div>
      <input
        name="name"
        placeholder="이름"
        onChange={onChange}
        value={name}
        ref={nameInput} /* nameInput 객체를 선택하고 싶은 DOM에 넣어준다. */
      />
      <input name="nickname" placeholder="닉네임" onChange={onChange} value={nickname} />
      <button onClick={onReset}>초기화</button>
      <div></div>
      <b>값 :</b>
      {name} ({nickname})
    </div>
  );
}

export default InputSample;
```

그리고는 onReset 함수에서 **nameInput.current.focus**를 써준다. 이때 **current는** DOM을 가르킨다.

이렇게하면 focus가 이동된다.

즉, useRef를 불러와서, 호출한 이후에 그 반환값을 변수에 담아준다.

그리고 그 변수식별자를 **ref** 라는 값으로 내가 원하는 DOM에 작성해주고 해당 DOM을 선택하고 싶을경우에는 .current 를 이용해서 작업해주면 된다.
