# useRef 로 컴포넌트 안의 변수 만들기

---

컴포넌트 내부에서 let 키워드로 변수를 선언하게되면 다음번 리렌더링 시에는 변수값이 초기화 되게 되는데, 그렇다면 리렌더링시에도 초기화 되지 않게끔 관리 싶다면 useState를 사용해야 되는데 useState를 사용할때 값을 바꾸게 되면 Component가 리렌더링 됩니다.

## 값이 변해도 리렌더링이 안일어나게 하려면?

useRef라는 Hooks를 사용하면된다. 이전에 useRef는 특정 DOM을 선택할때 사용한다고 알고있었다. 컴포넌트가 리렌더링 될때마다 어떠한 값을 관리하고자 할때 사용할수도 있다.

주로 setTimeOut이나 setInterval을 사용했을때 주어지는 id값을 기억할때 사용하기도하며, 외부라이브러리를 사용하여 생성된 인스턴스를 담을때 스크롤위치 기억 등등.. **중요한것은 useRef를 사용하여 관리하는 값은 바뀌어도 컴포넌트가 리렌더링 되지 않는다는 것**이다.

App 컴포넌트에서 useRef를 사용해서 변수를 관리해보자. 배열에 새 항목을 추가할때 새항목에서 사용할 고유 id 값을 관리하기위해 사용해보자.

```jsx
// App.js
import React from 'react';
import UserList from './UserList';

function App() {
  return <UseList />;
}

export default App;
```

UserList에서 users 배열을 props로 받아오자. 그렇게 하기위해서는 부모에서 자식으로 전달되는 props를 구현하기위해 기존에 UserList에 있던 user 배열을 App.js로 옮겨주자.

```jsx
// UserList.js

import React from 'react';

function User({ user }) {
  return (
    <div>
      <b>{users.username}</b> <span>({users.email})</span>
    </div>
  );
}

function UserList({ users }) {
  return <div>{u * sers.m * ap((user, index) => <User user={user} key={user.id} />)}</div>;
}

export default UserList;
```

App.js 에서 아래와 같이 받아와준다. 그리고는 UserList의 Props를 지정하면된다. 그리고는 useRef를 사용해서 nextId 라는 변수를 만들어주자.

```jsx
// App.js

import React from 'react';
import UserList from './UserList';

function App() {
  const users = [
    {
      id: 1,
      username: 'dunamisyoung',
      email: 'public.dunamisyoung@gmail.com',
    },
    {
      id: 2,
      username: 'tangerinePeanut',
      email: 'public.tangerinePeanut@gmail.com',
    },
    {
      id: 3,
      username: 'eiluoso',
      email: 'public.eiluoso@gmail.com',
    },
  ];

  const nextId = useRef(4);

  return <UseList users={users} />;
}

export default App;
```

나중에 새로운 항목을 추가하게 될경우를 생각해서 함수를 하나 만들자. 나중에 nextId의 값을 조회하고 싶다면 `.current` 를 사용해주면된다. 또한, 새롭게 생기는 배열의 경우 id값을 1씩 증가하기위해 아래와 같이 적어주자.

```jsx
// App.js

import React from 'react';
import UserList from './UserList';

function App() {
  const users = [
    {
      id: 1,
      username: 'dunamisyoung',
      email: 'public.dunamisyoung@gmail.com',
    },
    {
      id: 2,
      username: 'tangerinePeanut',
      email: 'public.tangerinePeanut@gmail.com',
    },
    {
      id: 3,
      username: 'eiluoso',
      email: 'public.eiluoso@gmail.com',
    },
  ];

  const nextId = useRef(4);

  const onCreate = () => {
    consle.log(nextId.current);
    nextId.current += 1;
  };

  return <UseList users={users} />;
}

export default App;
```

useRef는 특정 DOM을 선택하고 싶을때 뿐아니라, 컴포넌트의 값이변했을때 리렌더링이 되어도 useRef로 작성한 값은 유지되게 하기 위해서 사용하기도 한다.
