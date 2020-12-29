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

![Untitled6](https://user-images.githubusercontent.com/66991380/103296207-f5f48980-4a38-11eb-815a-b6c928f03ebc.jpg)

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

## 6.4 응용

---

배운개념을 응용해 고정된 배열을 렌더링 하지않고 동적배열을 렌더링해보자.

index값이 아닌 고유값을 만들수 있는 방법에 대해서도 알아보자.

```jsx
import React, { useState } from 'react';

const IterationSample = () => {
  const [names, setNames] = useState([
    { id: 1, text: '땅콩' },
    { id: 2, text: '귤' },
    { id: 3, text: '허브' },
    { id: 4, text: '우드' },
    { id: 5, text: '시트러스' },
  ]);

  const [inputText, setInputText] = useState('');
  const [nextId, setNextId] = useState(5);

  const nameList = names.map((name) => <li key={name.id}>{name.text}</li>);
  return <ul>{nameList}</ul>;
};

export default IterationSample;
```

위 코드처럼 map 함수를 사용할때 key값을 index대신 name.id값으로 지정해 줄수있다.

### 데이터 추가 기능 구현

버튼 클릭시에 호출할 onClick 함수를 함수로 정의해서 onClick 이벤트로 설정해보자.

그리고는 onClick 함수에서는 배열의 내장함수 [concat](https://poiemaweb.com/js-array#55-arrayprototypeconcatitems-arrayt--t-t--es3)을 사용해 새로운 항목을 추가한 배열을 만들어 setNames를 통해 상태를 업데이트 해주자.

```jsx
import React, { useState } from 'react';

const IterationSample = () => {
  const [names, setNames] = useState([
    { id: 1, text: '땅콩' },
    { id: 2, text: '귤' },
    { id: 3, text: '허브' },
    { id: 4, text: '우드' },
    { id: 5, text: '시트러스' },
  ]);

  const [inputText, setInputText] = useState('');
  const [nextId, setNextId] = useState(5);

  const onChange = (e) => setInputText(e.target.value);
  const onClick = () => {
    const nextNames = names.concat({
      id: nextId,
      text: inputText,
    });
    setNextId(nextId + 1);
    setNames(nextNames);
    setInputText('');
  };

  const nameList = names.map((name) => <li key={name.id}>{name.text}</li>);
  return (
    <>
      <input value={inputText} onChange={onChange} />
      <button onClick={onClick}>추가</button>
      <ul>{nameList}</ul>
    </>
  );
};

export default IterationSample;
```

이때 concat은 새로운 배열을 만들어주며, 불변성 유지를 할수있게 도와줍니다. 자세한것은 조금더 배우고 알아보자.

### 데이터 제거기능 구현

이번에는 각 항목을 더블 클릭시 해당 항목이 화면에서 사라지는 기능을 구현해보자. 이것도 불변성을 유지하며 업데이트 해주어야한다. 이때 특정항목을 지울때는 배열고차함수인 [filter](https://poiemaweb.com/js-array-higher-order-function#4-arrayprototypefiltercallback-value-t-index-number-array-array--any-thisarg-any-t--es5)를 사용한다.

```jsx
const numbers = [1, 2, 3, 4, 5, 6];
const biggerThaneThree = numbers.filter((number) => number > 3); // [4, 5, 6]
```

filter함수를 사용하면 특정조건을 만족하는 원소들만 쉽게 분류할 수 있다. 이러한 특성을 바탕으로 이벤트를 등록해봅시다.

```jsx
import React, { useState } from 'react';

const IterationSample = () => {
  const [names, setNames] = useState([
    { id: 1, text: '땅콩' },
    { id: 2, text: '귤' },
    { id: 3, text: '허브' },
    { id: 4, text: '우드' },
    { id: 5, text: '시트러스' },
  ]);

  const [inputText, setInputText] = useState('');
  const [nextId, setNextId] = useState(5);

  const onChange = (e) => setInputText(e.target.value);
  const onClick = () => {
    const nextNames = names.concat({
      id: nextId,
      text: inputText,
    });
    setNextId(nextId + 1);
    setNames(nextNames);
    setInputText('');
  };

  const onRemove = (id) => {
    const nextNames = names.filter((name) => name.id !== id);
    setNames(nextNames);
  };

  const nameList = names.map((name) => (
    <li key={name.id} onDoubleClick={() => onRemove(name.id)}>
      {name.text}
    </li>
  ));
  return (
    <>
      <input value={inputText} onChange={onChange} />
      <button onClick={onClick}>추가</button>
      <ul>{nameList}</ul>
    </>
  );
};

export default IterationSample;
```

### 정리

- 컴포넌트에서 반복적인 요소를 렌더링을 해야할경우에는 map을 사용하자
- key 값을 통해 최적화를 위해 사용되며, 값이 중복되지않도록 조심해야한다. 즉 고유한 값으로 설정해야한다. key값이 별도로 없을 경우에는 index를 이용한다.
- 상태안에서 배열을 변경시에 원본 배열에 직접 접근하는것이아니라. concat, filter등을사용해 원본배열을 건드리지 않는것을 기억하자.
