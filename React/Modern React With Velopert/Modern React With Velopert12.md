# 배열에 항목 제거하기

---

배열에 있는 항목을 제거하는 방법을 알아보자. UserList 컴포넌트에서 onRemove 라는 props를 받아와준다. 그리고는 User 컴포넌트에게 전달해준다. 그리고 User 컴포넌트에서 받아와준다. 그리고는 버튼도 하나 만들어준다.

```jsx
// UserList.js
import React from 'react';

function User({ user, onRemove }) {
  return (
    <div>
      <b>{user.username}</b> <span>({user.email})</span>
      <button>삭제</button>
    </div>
  );
}

function UserList({ users, onRemove }) {
  return (
    <div>
      {users.map((user) => (
        <User user={user} key={user.id} onRemove={onRemove} />
      ))}
    </div>
  );
}

export default UserList;
```

삭제 버튼을 눌렀을때 onRemove가 호출될때 user.id를 받아와서 사용하고 싶다면 아래와 같이 작성해주자.

```jsx
// UserList.js
import React from 'react';

function User({ user, onRemove }) {
  return (
    <div>
      <b>{user.username}</b> <span>({user.email})</span>
      <button onClick={() => onRemove(user.id)}>삭제</button>
    </div>
  );
}

function UserList({ users, onRemove }) {
  return (
    <div>
      {users.map((user) => (
        <User user={user} key={user.id} onRemove={onRemove} />
      ))}
    </div>
  );
}

export default UserList;
```

디스트럭쳐링 할당을 통해 좀더 간결하게 나타낼수도있다.

```jsx
// UserList.js
import React from 'react';

function User({ user, onRemove }) {
  const { username, email, id } = user;
  return (
    <div>
      <b>{username}</b> <span>({email})</span>
      <button onClick={() => onRemove(id)}>삭제</button>
    </div>
  );
}

function UserList({ users, onRemove }) {
  return (
    <div>
      {users.map((user) => (
        <User user={user} key={user.id} onRemove={onRemove} />
      ))}
    </div>
  );
}

export default UserList;
```

이때 조심해야할 부분은 onClick 이벤트를 작성해줄때 **함수가 아닌 함수 호출문을 작성하게되면 랜더링 될때 삭제하는 상황이 연출될것이다.** 그러니 조심하자. 다시 App.js 를 열어보자

배열에서 특정항목을 삭제할때는 불변성을 지켜가면서 업데이트를 해주어야한다. 이때 filter함수를 사용하는것이 좋다. 아래와 같이 작성해보자.

```jsx
// App.js

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
    nextId.current += 1;
  };

  const onRemove = (id) => {
    setUsers(users.filter((user) => user.id !== id));
  };
  return (
    <>
      <CreateUser username={username} email={email} onChange={onChange} onCreate={onCreate} />
      <UserList users={users} onRemove={onRemove} />
    </>
  );
}

export default App;
```
