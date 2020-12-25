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

## 4.2 이벤트 핸들링 익히기

---

아래처럼 코드를 작성해봅시다.

```jsx
//EventPactice
import React, { Component } from 'react';

class EventPractice extends Component {
  render() {
    return (
      <div>
        <h1>이벤트연습</h1>
      </div>
    );
  }
}

export default EventPractice;
```

App.js에서 EventPractice 를 렌더해봅시다.

```jsx
// App.js
import React from 'react';
import EventPractice from './EventPractice';

const App = () => {
  return <EventPractice />;
};

export default App;
```

EventPractice 컴포넌트의 render 메서드안에 input 요소를 작성하고 그안에 JSX 이벤트 핸들러를 적어줍시다. 이전에 공부한것처럼 사용자 정의 컴포넌트에는 이벤트를 등록할수 없다는것을 생각하면서 작성해보자 😉

```jsx
import React, { Component } from 'react';

class EventPractice extends Component {
  render() {
    return (
      <div>
        <h1>이벤트연습</h1>
        <input
          type="text"
          name="messge"
          placeholder="아무거나 입력"
          onChange={(e) => {
            console.log(e);
          }}
        />
      </div>
    );
  }
}

export default EventPractice;
```

개발자 도구에서 값을 적으면 이벤트 객체가 나타난다. 여기서 나타나는 e 객체는 SyntheticEvent로 웹브라우저의 네이티브 이벤트를 감싸는 객체이다. 사용법은 HTML 이벤트를 다룰때와 동일하며, SyntheticEvent는 네이티브 이벤트와다르게 이벤트가 종료시 초기화되므로 값의 참조가 불가하다. 만약 비동기적으로 이벤트 객체를 참조해야할때는 e.persist() 함수를 호출해야한다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7498534b-a81d-4a41-a911-6ca6f3b77755/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7498534b-a81d-4a41-a911-6ca6f3b77755/Untitled.png)

하지만 아래는 리액트 원서를 캡쳐해놓은 사진이다. 보면 v17부터는 지원하지 않는다는 이야기가 나온다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5e436a82-2002-4d78-bb9f-d20c56223b1b/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5e436a82-2002-4d78-bb9f-d20c56223b1b/Untitled.png)

일단은 알아두면 개념의 흐름을 이어나가기에 충분하니 알아두도록하고 자세한 내용은 [합성 이벤트(SyntheticEvent)](https://ko.reactjs.org/docs/events.html#other-events)와 [합성 이벤트와 Event Pooling](https://medium.com/react-native-seoul/react-%EB%A6%AC%EC%95%A1%ED%8A%B8%EB%A5%BC-%EC%B2%98%EC%9D%8C%EB%B6%80%ED%84%B0-%EB%B0%B0%EC%9B%8C%EB%B3%B4%EC%9E%90-06-%ED%95%A9%EC%84%B1-%EC%9D%B4%EB%B2%A4%ED%8A%B8%EC%99%80-event-pooling-6b4a0801c9b9)을 참고하자.

### State에 input값 담기

```jsx
import React, { Component } from 'react';

class EventPractice extends Component {
  state = {
    message: '',
  };

  render() {
    return (
      <div>
        <h1>이벤트연습</h1>
        <input
          type="text"
          name="messge"
          placeholder="아무거나 입력"
          value={this.state.message}
          onChange={(e) => {
            this.setState({
              message: e.target.value,
            });
          }}
        />
      </div>
    );
  }
}

export default EventPractice;
```

위 코드를 작성해서 this.setState메서드를 호출해 내가 입력하는 값으로 state를 업데이트해보자.

이번에는 버튼을 하나만들어 확인버튼을 누르면 경고창을 띄우면서 내가입력한 값을 보여주고, input의 값을 빈칸으로 만들어보자.

```jsx
import React, { Component } from 'react';

class EventPractice extends Component {
  state = {
    message: '',
  };

  render() {
    return (
      <div>
        <h1>이벤트연습</h1>
        <input
          type="text"
          name="messge"
          placeholder="아무거나 입력"
          value={this.state.message}
          onChange={(e) => {
            this.setState({
              message: e.target.value,
            });
          }}
        />
        <button
          onClick={() => {
            alert(this.state.message);
            this.setState({
              message: '',
            });
          }}
        >
          확인
        </button>
      </div>
    );
  }
}

export default EventPractice;
```

### 임의 메서드 만들기

앞에 이벤트 사용시 주의사항에보면 **이벤트에 실행할 자바스크립트 코드가아닌 함수 형태의 값을 전달한다.** 라고 배웠다. 그렇기에 이벤트를 바인딩하면서 함수를 만들어 전달했는데 함수를 따로 만들어 전달할 수 도 있다. 이를통해 가독성을 한층 올려줄수 있다. 위에서 작성한 onChange와 onClick에전달한 함수를 따로 빼서 컴포넌트로 분리해보자.

```jsx
import React, { Component } from 'react';

class EventPractice extends Component {
  state = {
    message: '',
  };

  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.handleClick = this.handleClick.bind(this);
  }

  handleChange(e) {
    this.setState({
      message: e.target.value,
    });
  }

  handleClick(e) {
    alert(this.state.message);
    this.setState({
      message: '',
    });
  }

  render() {
    return (
      <div>
        <h1>이벤트연습</h1>
        <input
          type="text"
          name="messge"
          placeholder="아무거나 입력"
          value={this.state.message}
          onChange={this.handleChange}
        />
        <button onClick={this.handleClick}>확인</button>
      </div>
    );
  }
}

export default EventPractice;
```

여기서 한번더 짚고 넘어가야할점은 , super(props) 선언전까지 constructor에서 this는 사용이 불가하다. 물론 super를 호출한이후에는 가능하다. 더 많은 내용은 [왜 super(props) 를 명시해 줘야 하는가?](https://velog.io/@honeysuckle/%EB%B2%88%EC%97%AD-Dan-Abramov-%EC%99%9C-superprops-%EB%A5%BC-%EC%9E%91%EC%84%B1%ED%95%B4%EC%95%BC-%ED%95%98%EB%8A%94%EA%B0%80) 를 참고하자.

### Property Initializer Syntax 사용하기

바벨의 [transform-class-properties](https://medium.com/@wongni/%EB%A6%AC%EC%95%A1%ED%8A%B8%EC%97%90%EC%84%9C-bind-this-%EB%B9%BC-%EB%B2%84%EB%A6%AC%EA%B8%B0-dfb0bbf7bef0) 문법을 사용해서 화살표 함수 형태로 메서드를 정의해보자. 이렇게 작성하면 훨씬 깔끔하게 정의가 가능하다.

```jsx
import React, { Component } from 'react';

class EventPractice extends Component {
  state = {
    message: '',
  };

  handleChange = (e) => {
    this.setState({
      message: e.target.value,
    });
  };

  handleClick = (e) => {
    alert(this.state.message);
    this.setState({
      message: '',
    });
  };

  render() {
    return (
      <div>
        <h1>이벤트연습</h1>
        <input
          type="text"
          name="messge"
          placeholder="아무거나 입력"
          value={this.state.message}
          onChange={this.handleChange}
        />
        <button onClick={this.handleClick}>확인</button>
      </div>
    );
  }
}

export default EventPractice;
```

### input 여러개 다루기

지금까지 input 값을 state에 넣는 방법을배웠다. input이 여러개일때는 어떻게 작업해야할까? 이때는 `e.target.name` 값을 이용하면된다. 이벤트 핸들러에서 e.target.name은 해당 인풋의 name을 가르킨다. 지금은 message 일것이다. 이 값을 통해 state를 설정하여 쉽게 여러개의 input을 작업할수있다.

```jsx
import React, { Component } from 'react';

class EventPractice extends Component {
  state = {
    username: '',
    message: '',
  };

  handleChange = (e) => {
    this.setState({
      [e.target.name]: e.target.value,
    });
  };

  handleClick = (e) => {
    alert(this.state.username + ':' + this.state.message);
    this.setState({
      username: '',
      message: '',
    });
  };

  render() {
    return (
      <div>
        <h1>이벤트연습</h1>
        <input
          type="text"
          name="messge"
          placeholder="사용자명"
          value={this.state.username}
          onChange={this.handleChange}
        />
        <input
          type="text"
          name="messge"
          placeholder="아무거나 입력"
          value={this.state.message}
          onChange={this.handleChange}
        />
        <button onClick={this.handleClick}>확인</button>
      </div>
    );
  }
}

export default EventPractice;
```

아래 코드를 보면 객체안에서 key를 `[]` 로 감싸면 그 안에 넣은 레퍼런스가 가리키는 실제 값이, key 값으로 사용된다. 아래 문법을 [computed property names](https://ko.javascript.info/object#ref-172) 라고 부른다.

```jsx
handleChange = (e) => {
  this.setState({
    [e.target.name]: e.target.value,
  });
};
```

### onKeyPress 이벤트 핸들링

아래 코드는 handleKeyPress 함수를 만들어 'Enter' 이벤트 발생시 실행흐름을 handleClick으로 옮겼습니다.

```jsx
import React, { Component } from 'react';

class EventPractice extends Component {
  state = {
    username: '',
    message: '',
  };

  handleChange = (e) => {
    this.setState({
      [e.target.name]: e.target.value,
    });
  };

  handleClick = (e) => {
    alert(this.state.username + ':' + this.state.message);
    this.setState({
      username: '',
      message: '',
    });
  };

  render() {
    return (
      <div>
        <h1>이벤트연습</h1>
        <input
          type="text"
          name="messge"
          placeholder="사용자명"
          value={this.state.username}
          onChange={this.handleChange}
        />
        <input
          type="text"
          name="messge"
          placeholder="아무거나 입력"
          value={this.state.message}
          onChange={this.handleChange}
        />
        <button onClick={this.handleClick}>확인</button>
      </div>
    );
  }
}

export default EventPractice;
```

## 4.3 함수형 컴포넌트로 구현하기

이제껏 작성했던 코드들을 함수형 컴포넌트로 작성해봅시다.

```jsx
import React, { useState } from 'react';

const EventPractice = () => {
  const [username, setUsername] = useState('');
  const [message, setMessage] = useState('');
  const onChangeUsername = (e) => setUsername(e.target.value);
  const onChangeMessage = (e) => setMessage(e.target.value);

  const onClick = () => {
    alert(username + ':' + message);
    setUsername('');
    setMessage('');
  };

  const onKeyPress = (e) => {
    if (e.key === 'Enter') {
      onClick();
    }
  };

  return (
    <div>
      <h1>이벤트 연습</h1>
      <input
        type="text"
        name="username"
        placeholder="아무거나 입력하세요"
        value={username}
        onChange={onChangeUsername}
      />
      <input
        type="text"
        name="message"
        placeholder="아무거나 입력하세요"
        value={message}
        onChange={onChangeMessage}
        onKeyPress={onKeyPress}
      />
      <button onClick={onClick}>확인</button>
    </div>
  );
};

export default EventPractice;
```

위 코드는 e.target.name을 활용하지 않고 onChange 관련 함수 두개를 따로 만들었다. 하지만 input의 개수가 많아면 e.target.name을 활용하는것이 더 좋을수 있다.

```jsx
import React, { useState } from 'react';

const EventPractice = () => {
  const [form, setForm] = useState({
    username: '',
    message: '',
  });
  const { username, message } = form;
  const onChange = (e) => {
    const nextFrom = {
      ...form,
      [e.target.name]: e.target.value,
    };
    setForm(nextFrom);
  };

  const onClick = () => {
    alert(username + ':' + message);
    setForm({
      username: '',
      message: '',
    });
  };

  const onKeyPress = (e) => {
    if (e.key === 'Enter') {
      onClick();
    }
  };

  return (
    <div>
      <h1>이벤트 연습</h1>
      <input type="text" name="username" placeholder="아무거나 입력하세요" value={username} onChange={onChange} />
      <input
        type="text"
        name="message"
        placeholder="아무거나 입력하세요"
        value={message}
        onChange={onChange}
        onKeyPress={onKeyPress}
      />
      <button onClick={onClick}>확인</button>
    </div>
  );
};

export default EventPractice;
```

이렇게 [computed property names](https://ko.javascript.info/object#ref-172) 을 활용한 input요소 여러개를 관리할수있는 방법을 배웟다.
