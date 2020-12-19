# 배열 렌더링하기

---

## 리액트에서 배열 렌더링하기

예를 들어 아래와 같은 배열이 있다고 가정해보자

```jsx
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
```

우선 UserList 컴포넌트를 만들어준다.

그리고 아래와 같이 작성해보자. 아래의 코드는 배열의 하나하나의 요소들을 랜더링 해주는 JSX 코드이다.

```jsx
import React from 'react';

function UserList() {
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
  return (
    <div>
      <div>
        <b>{users[0].username}</b> <span>({users[0].email})</span>
      </div>
      <div>
        <b>{users[1].username}</b> <span>({users[1].email})</span>
      </div>
      <div>
        <b>{users[2].username}</b> <span>({users[1].email})</span>
      </div>
    </div>
  );
}

export default UserList;
```

컴포넌트를 `export default UserList;` 로 내보내 주고, App 컴포넌트에서 랜더링 해보자.

기존에 InputSample import를 지우고 UserList를 불러와준다.

```jsx
// App.js

import Reactfrom 'react';
import UserList from './UserList';

function App() {
  return (
    <UserList />
  );
}

export default App;
```

그리고는 render 안에 있는 겹치는 JSX 문법을 User 라는 컴포넌트로 만들어주자. 그리고는 user를 props 로 받아와준다.

```jsx
// UserList.js

import React from 'react';

function User({ user }) {
  return (
    <div>
      <b>{users[0].username}</b> <span>({users[0].email})</span>
    </div>
  );
}

function UserList() {
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
  return (
    <div>
      <div>
        <b>{users[0].username}</b> <span>({users[0].email})</span>
      </div>
      <div>
        <b>{users[1].username}</b> <span>({users[1].email})</span>
      </div>
      <div>
        <b>{users[2].username}</b> <span>({users[1].email})</span>
      </div>
    </div>
  );
}

export default UserList;
```

그리고는 디스트럭쳐링 할당으로 user[0]이라고 젹혀있던 부분을 user 로 바꾸어준다.

그리고 는 User 컴포넌트를 return 문 안에서 사용해준다.

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

function UserList() {
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
  return (
    <div>
      <User user={users[0]} />
      <User user={users[1]} />
      <User user={users[2]} />
    </div>
  );
}

export default UserList;
```

이런식으로 배열이 고정적이라면 위와같이 사용해도 문제가 없겠지만, 배열의 값이 매번 변하게 된다면, **map 배열고차함수를 사용해주면된다. 즉, map 함수를 사용해서 객체형태로 있던 배열을 컴포넌트 엘리먼트 형태의 배열로 변환해보자.**

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

function UserList() {
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
  return (
    <div>
      {users.map((user) => (
        <User user={user} />
      ))}
    </div>
  );
}

export default UserList;
```

위와 같이 작성하면 users 라는 식별자를 참조해서 각각에 배열의 갯수만큼 배열 하나하나를 돌면서 컴포넌트를 반환하게된다. 하지만 위와 같이 작성했을때 개발자도구의 console창을 확인해보면 Each child in a list should have a unique "key" prop. 라는 경고를 볼수있다. 이는 key라는 props 를 통해 원소마다 고유값을 주어 나중에 최적화를 도와주게된다.

현재 배열에서 key로 사용할 고유한 값은 id 값이므로 기존 코드를 아래와 같이 수정해보자.

```jsx
---

return (
    <div>
	     {
					users.map(
						user => (<User user={user} key={user.id}/>)
					)
				}
    </div>
  );
}

export default UserList;
```

만약, id와 같은 고유값이 없을 경우에는 **map배열 고차함수의 두번째 파라미터로 index 값을 전달**해주면된다.

그렇다면 key가 없다면 어떻게될까 key 역할에 대해 잠시 알아보면?

### key의 존재유무에 따른 업데이트 방식의 차이점

아래와 같은 배열이 있다.

```jsx
const array = ['a', 'b', 'c', 'd'];
```

위와 같은 배열을 렌더링 한다고 했을떄 아래와 같은 코드를 return 문안에 전달하게 될것이다.

```jsx
array.map(item => <div>{item}</div>;
```

위 array 배열에 다른 요소값이 추가된다고 했을때 즉, b와 c 사이에 z라는값이 추가된다고 한다면 자바스크립트 엔진의 동작은 a부터 다시 리렌더링 하게될텐데 c의 값이 z로 d의 값이 c로 그리고 d 뒤에 요소하나를 추가하고 d라는 문자열을 삽입하게 된다. 이처럼 key 값이 정해져 있지 않다면 리렌더링을 통해 성능저하를 가져올수있다.

고유한값이 있는 객체가 있다면 그 객체를 찾아서 내가 설정한 값을 변화시키게된다. 이렇게 key는 성능과 연관이 있다. 즉, 자주업데이트 되지 않거나, 데이터의 갯수가 조금일 경우에는 key 값을 index로 적어도 관계는 없지만 그렇지 않다면 key값을 설정해주자.
