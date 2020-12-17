# 여러개의 input 상태 관리하기

---

인풋요소 여러개를 관리하는 방법을 알아봅시다.

기존의 InputSample.js 파일을 아래와 같이 수정해줍니다.

```jsx
//InputSample.js
import React, { useState } from 'react';

function InputSample() {
  const onChange = (e) => {};

  const onReset = () => {};

  return (
    <div>
      <input placeholder="이름" />
      <input placeholder="닉네임" />
      <button onClick={onReset}>초기화</button>
      <div></div>
      <b>값 :</b>
      이름 (닉네임)
    </div>
  );
}

export default InputSample;
```

인풋이 여러개 있을때는 아까와 같이 useState값을 여러번사용하고 onChange도 여러개만들고 할수있겠지만 input에 name이라는 값을 설정하고 이벤트 발생시 그값을 참조하는 방식으로 구현하는것이 조금더 좋은 방법이라고 할수있다.

useState에서는 기존에는 문자열 값을 관리했지만 이제는 여러개의 값을 가지고있는 객체형태의 값을 관리해 주어야한다.

```jsx
import React, { useState } from 'react';

function InputSample() {
  const [input, setInputs] = useState({
    name: '',
    nickname: '',
  });

  const onChange = (e) => {};

  const onReset = () => {};

  return (
    <div>
      <input placeholder="이름" />
      <input placeholder="닉네임" />
      <button onClick={onReset}>초기화</button>
      <div></div>
      <b>값 :</b>
      이름 (닉네임)
    </div>
  );
}

export default InputSample;
```

객체형태로 상태값을 관리하기위해 배열 디스트럭쳐링 할당을 통해 기본값을 설정했다면, 그리고 inputs의 안에있는 name과 nickname 값을 쉽게 사용할수있도록 다시한번 디스트럭쳐링 할당을 해줍니다. 그리고는 각 input요소에 맞게 어트리뷰트를 적어줍니다.

```jsx
import React, { useState } from 'react';

function InputSample() {
  const [inputs, setInputs] = useState({
    name: '',
    nickname: '',
  });
  const { name, nickname } = inputs;

  const onChange = (e) => {};

  const onReset = () => {};

  return (
    <div>
      <input name="name" placeholder="이름" />
      <input name="nickname" placeholder="닉네임" />
      <button onClick={onReset}>초기화</button>
      <div></div>
      <b>값 :</b>
      이름 (닉네임)
    </div>
  );
}

export default InputSample;
```

이벤트 핸들러도 등록해줍니다. 그리고 onChange함수에 작동이 잘되는지 확인하기위해서 console.log(e.target.value) 값도 설정해줍니다.

```jsx
import React, { useState } from 'react';

function InputSample() {
  const [inputs, setInputs] = useState({
    name: '',
    nickname: '',
  });
  const { name, nickname } = inputs;

  const onChange = (e) => {
    const { name, value } = e.target;

    console.log(e.target.name);
    console.log(e.target.value);
  };

  const onReset = () => {};

  return (
    <div>
      <input name="name" placeholder="이름" onChange={onChange} />
      <input name="nickname" placeholder="닉네임" onChange={onChange} />
      <button onClick={onReset}>초기화</button>
      <div></div>
      <b>값 :</b>
      이름 (닉네임)
    </div>
  );
}

export default InputSample;
```

잘되는지 확인한했다면, 다음으로 리액트에서는 객체를 업데이트를 할때는 기존객체를 복사해야합니다. 그래서 스프레드 문법을이용해 새로만든 nextInputs 라는 객체에 inputs의 값을 풀어가져오고, 덮어씌워 줍니다. setInputs에 인수로 onchage이벤트가 발생했을때의 value 값을 인수로 전달합니다.

const nextInputs = {...inputs,name: value,}; 이렇게 작성했을경우 name에 문자열 name이 들어가게됩니다. 그때 `[]` 대괄호 표기법을 이용해 [name]을 감싸주면 됩니다.

```jsx
import React, { useState } from 'react';

function InputSample() {
  const [inputs, setInputs] = useState({
    name: '',
    nickname: '',
  });

  const { name, nickname } = inputs; // 객체 디스트럭쳐링 할당

  const onChange = (e) => {
    const { name, value } = e.target;

    const nextInputs = {
      ...inputs,
      [name]: value,
    };

    setInputs(nextInputs);
  };

  const onReset = () => {};

  return (
    <div>
      <input name="name" placeholder="이름" onChange={onChange} />
      <input name="nickname" placeholder="닉네임" onChange={onChange} />
      <button onClick={onReset}>초기화</button>
      <div></div>
      <b>값 :</b>
      이름 (닉네임)
    </div>
  );
}

export default InputSample;
```

사실 nextInputs 라는 함수를 작성할 필요없이 아래와 같이 작성해주면됩니다.

```jsx
import React, { useState } from 'react';

function InputSample() {
  const [inputs, setInputs] = useState({
    name: '',
    nickname: '',
  });

  const { name, nickname } = inputs; // 객체 디스트럭쳐링 할당

  const onChange = (e) => {
    const { name, value } = e.target; // e.target에서 name프로퍼티, value프로퍼티추출

    setInputs({
      ...inputs,
      [name]: value,
    });
  };

  const onReset = () => {};

  return (
    <div>
      <input name="name" placeholder="이름" onChange={onChange} />
      <input name="nickname" placeholder="닉네임" onChange={onChange} />
      <button onClick={onReset}>초기화</button>
      <div></div>
      <b>값 :</b>
      이름 (닉네임)
    </div>
  );
}

export default InputSample;
```

사전에 추출해놓은 input과 nickname을 각어트리뷰트에 넣어줍니다. 그리고 `이름 (닉네임)` 이 적혀있던위치에 {name} {nickname} 도 넣어줍니다.

```jsx
import React, { useState } from 'react';

function InputSample() {
  const [inputs, setInputs] = useState({
    name: '',
    nickname: '',
  });

  const { name, nickname } = inputs;

  const onChange = (e) => {
    const { name, value } = e.target;

    setInputs({
      ...inputs,
      [name]: value,
    });
  };

  const onReset = () => {
    setInputs({
      name: '',
      nickname: '',
    });
  };

  return (
    <div>
      <input name="name" placeholder="이름" onChange={onChange} value={name} />
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

객체 상태를 업데이트할때는 꼭 기존 상태를 복사하고 나서 특정값을 덮어씌우고 새로운상태로 업데이트 해주어야한다.

이것을 불변성을 지켜준다고하는것인데, 이렇게해야 리액트컴포넌트가 상태가 업데이트가 됫음을 감지됫다는것을 인지할수있다.
