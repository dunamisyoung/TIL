# 6. 컴포넌트 반복

이곳은 중요하다고 생각하는 개념들, 흩어진 개념들의 집합소 입니다. :)

---

우리가 웹 애플리케이션을 만들다 보면 다음과 같이 반복되는 코드를 작성할때가 있다.

```jsx
import React from 'react';

const IterationSample = () => {
  return (
    <ul>
      <li>땅콩</li>
      <li>귤</li>
      <li>허브</li>
      <li>우드</li>
      <li>시트러스</li>
    </ul>
  );
};

export default IterationSample;
```

`<li></li>`이런 형태가 계속 반복되는데 지금은 몇개 되지않아서 괜찮게 보이지만 복잡한 코드들이 많이 나온다면 코드양이 늘어남에따라 파일용량도 많이 늘어날것입니다. 그것을 해결할수있도록해봅시다.

---

## 6.1 자바스크립트 배열의 map() 함수

---

배열고차함수인 **map** 함수를 사용해서 반복되는 컴포넌트를 렌더링 할수있습니다. map 메서드는 새로운 배열을 반환한다.

### 문법

**arr.map(currentValue,index,array,[thisArg]) - v,i,arr,thisArg**

이함수의 파라미터는 다음과 같습니다.

- currentValue : 현재 처리요소
- index : 현재 처리요소의 inedx값
- array : 현재 처리하고 있는 원본 배열
- thisArg : callback 함수 내부에서 사용할 this 레퍼런스

map 함수는 기존 배열로 새로운 배열을 만드는 역할을 한다.

```jsx
const numbers = [1, 2, 3, 4, 5];
const result = numbers.map((num) => num * num);
console.log(result);
```

위 명령을 통해 아래와같은 결과를 만들수있다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d750dab7-1d4c-4ec9-be57-2c9f088b34f4/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d750dab7-1d4c-4ec9-be57-2c9f088b34f4/Untitled.png)

---

## 6.2 데이터 배열을 컴포넌트 배열로 변환

---

```jsx
import React from 'react';

const IterationSample = () => {
  const names = ['땅콩', '귤', '허브', '우드', '시트러스'];
  const nameList = names.map((name) => <li>{name}</li>);
  return <ul>{nameList}</ul>;
};

export default IterationSample;
```

App 컴포넌트에서 확인해보면 map함수를 통해 각각의 다른요소들이 들어가있는 <li>태그를 반환할수있다.

---

## 6.3 key

---

리액트에서 key는 컴포넌트 배열을 렌더링 했을때 어떤 원소에 변동이 있었는지 알아내려고 사용한다. key가 없을때는 Virtual DOM을 비교하는 과정에서 리스트를 순차적으로 비교하게된다. 하지만 key가 있다면 key값을 이용해 좀 더빠르게 변화를 알아낼수있다.

### key값을 설정

map 함수 인자로 전달되는 함수 내부에서 컴포넌트 props를 설정하듯이 설정하면된다. key값은 언제나 유일해야한다. 하지만 이렇게 사용할수있는 key값이 없다면 어떻게 해야할까? 바로 inedx 값을 활용하면 된다.

```jsx
import React from 'react';

const IterationSample = () => {
  const names = ['땅콩', '귤', '허브', '우드', '시트러스'];
  const nameList = names.map((name, index) => <li key={index}>{name}</li>);
  return <ul>{nameList}</ul>;
};

export default IterationSample;
```

이렇게 고유한 값이 없을때만 index값을 key로 사용해야 하며 index를 key로 사용하면 배열이 변경될때 효율적으로 리렌더링 하지못한다.

---
