# JSX 소개

```javascript
const element = <h1>Hello, world!</h1>;
```

위 문법을 JSX라고 하며 Javascript를 확장한 문법입니다.

UI가 어떻게 생겨야 하는지 설명하기위해 JSX는 React와 함께 사용할것을 권장합니다.

**JSX는 React 엘리먼트를 생성**합니다.

## JSX란?

React에서는 이벤트가 처리되는 방식, 시간에 따라 state가 변하는 방식등 렌더링 로직이 본질적으로 다른 UI 로직과 연결된다.

React는 마크업과 로직을 넣어 기술을 인위적으로 분리하는 대신, 둘 다 포함하는 "컨포넌트" 라고 불리우는 느슨하게 연결된 유닛으로 관심사를 분리한다.

React에서 JSX 사용이 필수는 아니지만 대부분의 사람은 UI관련 작업을 할때 가독성이 좋다고 생각된다.

### JSX에 표현식 포함하기

아래 예시에는 name이라는 변수를 선언한후 중괄호로 감싸 JSX안에 사용하였습니다.

```javascript
const name = 'Lee';
const element = <h1>Hello, {name}</h1>;

ReactDOM.render(element, document.getElementById('root'));
```

**JSX의 중괄호 안에는 유효한 모든 Javascript 표현식을 넣을수 있습니다.**

### JSX도 표현식입니다

1. 컴파일이 끝나면,
2. JSX 표현식이 정규 Javascript 함수 호출
3. Javascript 객체로 인식됩니다.

결국 JSX는 ReactElement를 만들고. JSX 표현식을 Babel이 컴파일해 Javascript객체로 읽어 실행한다.

### JSX 속성 정의

속성에 따옴표를 이용해 문자열 리터럴을 정의할수 있다.

```javascript
const element = <div tabIndex="0"></div>;
```

HTML 어트리뷰트에 자바스크립트 표현식을 삽입하는것처럼 보여진다.

```javascript
const element = <img src={user.avatarUrl}></img>;
```

어트리뷰트에 Javascript 표현식을 삽일할때는 중괄호주변에 따옴표를 입력하면 안된다.

민약 사용한다고 했을때 중괄호 혹은 따옴표 한가지만 사용해야한다.

JSX에서 class는 **className**가 되고 tabindex는 **tabIndex**가 됩니다.

즉 카멜케이스를 이용한다.

### JSX로 자식정의

JSX 태그가 비어있다면 XML처럼 `/>` 를 이용해 바로 닫아주어야 합니다.

```javascript
const element = <img src={user.avatarUrl} />;
```

JSX 태그는 자식을 포함할수 있습니다.

```javascript
const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
```

### JSX는 주입 공격을 방지합니다.

ReactDOM은 JSX에 삽입된 모든 값을 렌더링하기전에 이스케이프처리하여 명시적으로 작성되지 않은 내용은 주입되지 않습니다.

모든항목은 렌더링되기전 문자열로 변환됩니다. 이특성을 통해 XSS(cross-site-scripting) 공격을 방지 할 수있습니다.

이것은 JSX 문법을 reactElement로 컴파일하는 작업과 관련이있는것일까? [이유](https://chaewonkong.github.io/posts/xss.html)

### JSX는 객체를 표현합니다.

Babel은 JSX를 React.createElement()호출로 컴파일 합니다.

다음 두 예시는 동일합니다.

```javascript
const element = <h1 className="greeting">Hello, world!</h1>;
```

```javascript
const element = React.createElement('h1', { className: 'greeting' }, 'Hello, world!');
```

React.createElement()는 버그가 없는 코드를 작성하는것에 도움이되며, 다음과 같은 객체를 생성하는데 이것이 **ReactElement**라고 합니다.

```javascript
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world!',
  },
};
```

이 객체는 **React가 DOM을 구성**하고 **최신으로 유지하는것에 사용**됩니다.
