# 배열에 항목 추가하기

---

배열에 새로운 항목을 추가하는 방법에 대해 알아보자.

일단 CreateUser.js 라는 파일을 하나만들어주자. 이파일에는 인풋 2개랑 버튼 한개를 만들것이다.

이파일에서 4개의 props를 가져올것이다.

```jsx
import React from 'react';

function CreateUser({ username, email, onChange, onCreate }) {
  return (
    <div>
      <input name="username" placeholder="계정명" onChange={onChange} value={username} />
      <input name="email" placeholder="이메일" onChange={onChange} value={email} />
      <button onClick={onCreate}>등록</button>
    </div>
  );
}

export default CreateUser;
```

onChange는 input 값이 바뀌게 될때 호출할 이벤트 처리함수, onCreate는 버튼을 눌렀을떄 새로운 항목을 등록해주는 함수이다. 위와 같이 입력해보자.

그리고는 App.js에 CreateUser 컴포넌트를 가져와서 렌더링 해주자. 이떄 Fragment로 CreateUser와 UserList를 감싸주어야 한다.

```jsx
import React, { useRef } from 'react';
import UserList from './UserList';
import CreateUser from './CreateUser';

function App() {
  const users = [
    {
      id: 1,
      username: 'velopert',
      email: 'public.velopert@gmail.com',
    },
    {
      id: 2,
      username: 'tester',
      email: 'tester@example.com',
    },
    {
      id: 3,
      username: 'liz',
      email: 'liz@example.com',
    },
  ];

  const nextId = useRef(4);
  const onCreate = () => {
    console.log(nextId.current);
    nextId.current += 1;
  };
  return (
    <>
      <CreateUser />
      <UserList users={users} />
    </>
  );
}

export default App;
```

여러개의 Input값을 관리할때는 useState를 사용하면되는데 useState를 두번사용하지말고 객체형태로 상태를 만들어주자. 먼저 useState를 불러와주고, inputs 라는 상태를 만들어주자. 그리고는 username, email 이라는 프로퍼티키를 지정해주자.

또한 inputs에서 username과 email을 가져와 디스트럭쳐링 할당을 해주자.

```jsx
import React, { useRef, useState } from 'react';
import UserList from './UserList';
import CreateUser from './CreateUser';

function App() {
  const [inputs, setInputs] = useState({
    username: '',
    email: '',
  });
  const { username, email } = inputs;

  const users = [
    {
      id: 1,
      username: 'velopert',
      email: 'public.velopert@gmail.com',
    },
    {
      id: 2,
      username: 'tester',
      email: 'tester@example.com',
    },
    {
      id: 3,
      username: 'liz',
      email: 'liz@example.com',
    },
  ];

  const nextId = useRef(4);
  const onCreate = () => {
    console.log(nextId.current);
    nextId.current += 1;
  };
  return (
    <>
      <CreateUser />
      <UserList users={users} />
    </>
  );
}

export default App;
```

그리고는 onChange 함수를 만들어주는데 e.target에서 name과 value를 가져와 디스트럭쳐링 해주고 아래와 같이 작성해보자.

```jsx
import React, { useRef, useState } from 'react';
import UserList from './UserList';
import CreateUser from './CreateUser';

function App() {
  const [inputs, setInputs] = useState({
    username: '',
    email: '',
  });
  const { username, email } = inputs;
  const onChange = (e) => {
    const { name, value } = e.target;
    setInputs({
      ...inputs,
      [name]: value,
    });
  };

  const users = [
    {
      id: 1,
      username: 'velopert',
      email: 'public.velopert@gmail.com',
    },
    {
      id: 2,
      username: 'tester',
      email: 'tester@example.com',
    },
    {
      id: 3,
      username: 'liz',
      email: 'liz@example.com',
    },
  ];

  const nextId = useRef(4);
  const onCreate = () => {
    console.log(nextId.current);
    nextId.current += 1;
  };
  return (
    <>
      <CreateUser username={username} email={email} onChange={onChange} onCreate={onCreate} />
      <UserList users={users} />
    </>
  );
}

export default App;
```

그리고 onCreate 함수에서 등록버튼을 누르면 값이 input에 적힌 값이 사라질수 있게끔 작성해보자.

```jsx
import React, { useRef, useState } from 'react';
import UserList from './UserList';
import CreateUser from './CreateUser';

function App() {
  const [inputs, setInputs] = useState({
    username: '',
    email: '',
  });

  const { username, email } = inputs;
  const onChange = (e) => {
    const { name, value } = e.target;
    setInputs({
      ...inputs,
      [name]: value,
    });
  };

  const users = [
    {
      id: 1,
      username: 'velopert',
      email: 'public.velopert@gmail.com',
    },
    {
      id: 2,
      username: 'tester',
      email: 'tester@example.com',
    },
    {
      id: 3,
      username: 'liz',
      email: 'liz@example.com',
    },
  ];

  const nextId = useRef(4);
  const onCreate = () => {
    setInputs({
      username: '',
      email: '',
    });
    console.log(nextId.current);
    nextId.current += 1;
  };
  return (
    <>
      <CreateUser username={username} email={email} onChange={onChange} onCreate={onCreate} />
      <UserList users={users} />
    </>
  );
}

export default App;
```

users 배열을 컴포넌트의 상태로써 관리하기위해 useState로 감싸주자.

```jsx
import React, { useRef, useState } from 'react';
import UserList from './UserList';
import CreateUser from './CreateUser';

function App() {
  const [inputs, setInputs] = useState({
    username: '',
    email: '',
  });

  const { username, email } = inputs;
  const onChange = (e) => {
    const { name, value } = e.target;
    setInputs({
      ...inputs,
      [name]: value,
    });
  };

  const [users, setUsers] = useState([
    {
      id: 1,
      username: 'velopert',
      email: 'public.velopert@gmail.com',
    },
    {
      id: 2,
      username: 'tester',
      email: 'tester@example.com',
    },
    {
      id: 3,
      username: 'liz',
      email: 'liz@example.com',
    },
  ]);

  const nextId = useRef(4);
  const onCreate = () => {
    setInputs({
      username: '',
      email: '',
    });
    console.log(nextId.current);
    nextId.current += 1;
  };
  return (
    <>
      <CreateUser username={username} email={email} onChange={onChange} onCreate={onCreate} />
      <UserList users={users} />
    </>
  );
}

export default App;
```

## 배열에 불변성을 지키면서 새로운 항목을 추가하는 방법

새로운배열을 만들어서 새로만든 배열을 변화시켜 관리하는 방식을 사용하자. push, splice, sort 같은 원본값을 변화시키는 배열 메서드를 사용할 경우에는 복사해서 사용해주자.

### 스프레드 연산자 사용하기

가장쉬운방법은 스프레드 문법을 사용하는것이다. onCreate애서 새로운 user객체를 만들어주자.

```jsx
import React, { useRef, useState } from 'react';
import UserList from './UserList';
import CreateUser from './CreateUser';

function App() {
  const [inputs, setInputs] = useState({
    username: '',
    email: '',
  });

  const { username, email } = inputs;
  const onChange = (e) => {
    const { name, value } = e.target;
    setInputs({
      ...inputs,
      [name]: value,
    });
  };

  const [users, setUsers] = useState([
    {
      id: 1,
      username: 'velopert',
      email: 'public.velopert@gmail.com',
    },
    {
      id: 2,
      username: 'tester',
      email: 'tester@example.com',
    },
    {
      id: 3,
      username: 'liz',
      email: 'liz@example.com',
    },
  ]);

  const nextId = useRef(4);
  const onCreate = () => {
    const user = {
      id: nextId.current,
      username,
      email,
    };
    setInputs({
      username: '',
      email: '',
    });
    console.log(nextId.current);
    nextId.current += 1;
  };
  return (
    <>
      <CreateUser username={username} email={email} onChange={onChange} onCreate={onCreate} />
      <UserList users={users} />
    </>
  );
}

export default App;
```

그리고는 setUsers 함수를 호출하면서 인수로 ...users, user를 전달하자.

```jsx
import React, { useRef, useState } from 'react';
import UserList from './UserList';
import CreateUser from './CreateUser';

function App() {
  const [inputs, setInputs] = useState({
    username: '',
    email: '',
  });

  const { username, email } = inputs;
  const onChange = (e) => {
    const { name, value } = e.target;
    setInputs({
      ...inputs,
      [name]: value,
    });
  };

  const [users, setUsers] = useState([
    {
      id: 1,
      username: 'velopert',
      email: 'public.velopert@gmail.com',
    },
    {
      id: 2,
      username: 'tester',
      email: 'tester@example.com',
    },
    {
      id: 3,
      username: 'liz',
      email: 'liz@example.com',
    },
  ]);

  const nextId = useRef(4);
  const onCreate = () => {
    const user = {
      id: nextId.current,
      username,
      email,
    };
    setUsers([...users, user]);
    setInputs({
      username: '',
      email: '',
    });
    console.log(nextId.current);
    nextId.current += 1;
  };
  return (
    <>
      <CreateUser username={username} email={email} onChange={onChange} onCreate={onCreate} />
      <UserList users={users} />
    </>
  );
}

export default App;
```

### concat 함수 사용하기

스프레드문법을 이용하지않고 아래와 같이 사용할수도 있다.

```jsx
import React, { useRef, useState } from 'react';
import UserList from './UserList';
import CreateUser from './CreateUser';

function App() {
  const [inputs, setInputs] = useState({
    username: '',
    email: '',
  });

  const { username, email } = inputs;
  const onChange = (e) => {
    const { name, value } = e.target;
    setInputs({
      ...inputs,
      [name]: value,
    });
  };

  const [users, setUsers] = useState([
    {
      id: 1,
      username: 'velopert',
      email: 'public.velopert@gmail.com',
    },
    {
      id: 2,
      username: 'tester',
      email: 'tester@example.com',
    },
    {
      id: 3,
      username: 'liz',
      email: 'liz@example.com',
    },
  ]);

  const nextId = useRef(4);
  const onCreate = () => {
    const user = {
      id: nextId.current,
      username,
      email,
    };
    setUsers(users.concat(user));
    setInputs({
      username: '',
      email: '',
    });
    console.log(nextId.current);
    nextId.current += 1;
  };
  return (
    <>
      <CreateUser username={username} email={email} onChange={onChange} onCreate={onCreate} />
      <UserList users={users} />
    </>
  );
}

export default App;
```
