# 4. 이벤트 핸들링

**`이곳은 중요하다고 생각하는 개념들, 흩어진 개념들의 집합소 입니다.` :)**

---

## 4.1 리액트의 이벤트 시스템

---

리액트의 이벤트 시스템은 HTML과 비슷하다. 하지만 일반 HTML에서 이벤트 작성과 약간 다르게 주의 사항 몇가지가 있다.

```jsx
import React, { useState } from 'react';

const Sat = () => {
  const [message, setMessage] = useState('');
  const onClickEnter = () => setMessage('안녕하세요!');
  const onClickLeave = () => setMessage('안녕히 가세요!');

  const [color, setColor] = useState('black');

  return (
    <div>
      <button onClick={onClickEnter}>입장</button>
      <button onClick={onClickEnter}>퇴장</button>
    </div>
  );
};

export default Say;
```

### 이벤트 사용시 주의사항

1. **이벤트 이름은 카멜케이스로 작성한다.**
   HTML의 onclick 이벤트를 onClick으로 작성해야하며 onKeyUp같은 형식도 동일하다.
2. **이벤트에 실행할 자바스크립트 코드가아닌 함수 형태의 값을 전달한다.**
   HTML에서 이벤트를 설정할때는 큰따옴표롤 감싸 코드를 넣어주었지만, 리액트에서는 함수형태의 값을 전달한다.
3. **DOM 요소에만 이벤트를 설정할 수 있다.**
   div, button, input 등의 DOM 요소에는 이벤트 설정이 가능하지만, **사용자 컴포넌트에는 이벤트를 자체적으로 설정할 수 없다**. 만약 Mycomponent에 onClick값을 설정해준다면, **함수 실행이 아닌 onClick이라는 이름을 가진 props를 해당컴포넌트에 전달할 뿐**이다. 따라서 컴포넌트에 자체적으로 이벤트를 설정할수는 없으나 **전달받은 props를 해당 컴포넌트 내부의 DOM 이벤트로설정은 가능**하다.

### 리액트 이벤트 종류

- Clipboard
- Composition
- Keyboard
- Focus
- Form
- Mouse
- Selection
- Touch
- UI
- Wheel
- Media
- Image
- Animation
- Transition

자세한 사항은 [https://ko.reactjs.org/docs/events.html#gatsby-focus-wrapper](https://ko.reactjs.org/docs/events.html#gatsby-focus-wrapper)에서 확인해보자.

---
