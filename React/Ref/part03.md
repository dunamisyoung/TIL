# Components and Props

React에서는 컨포넌트를 통해 UI를 재사용 가능한 개별적인 여러 조각으로 나눕니다.

개념적으로 컨포넌트는 Javascript의 함수와 유사합니다.

"props"라고 하는 임의의 입력을 받은후, 화면어 어떻게 표시되는지를 기술하는 **React엘리먼트를 반환**합니다.

### 함수 컨포넌트와 클래스 컴포넌트

컴포넌트를 정의하는 가장 간단한 방법은 Javascript 함수를 작성하는 것입니다.

```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

위 함수는 "props"라는 객체 인자를 받은후에 React엘리먼트를 반환함으로 유효한 React 컨포넌트 입니다. 위와 같은 형식을 **함수 컨포넌트**라고 호칭합니다.

**컨포넌트의 이름은 항상 대문자로 시작**해야한다. 그렇지 않으면 DOM 태그로 처리합니다.

### 컴포넌트 렌더링

이전까지는 React 엘리먼트를 DOM으로 나타냈습니다.

```javascript
const element = <div />;
```

React 엘리먼트는 사용자 정의 컴포넌트로도 나타낼 수 있습니다.

```javascript
const element = <Welcome name="Lee" />;
```

React가 사용자 정의 컴포넌트로 작성한 엘리먼트를 발견하면 JSX어트리뷰트와 자식을 해당 컴포넌트에 단일 객체로 전달 합니다. 이것을 "props"라고 합니다.

```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Lee" />;
ReactDOM.render(element, document.getElementById('root'));
```

위 코드는 사용자 정의 컴포넌트로 작성한 엘리먼트로 React.render()를 호출합니다.

React는 props객체 안에 있는 값을 가지고 사용자 정의 컨포넌트를 호출하며 값을 인자로 받아 처리후 엘리먼트를 반환 합니다.

### 컨포넌트 합성

컨포넌트는 자신의 출력에 다른 컴포넌트를 참조할 수 있다.

이는 모든 세부 단계에서 동일한 추상 컴포넌트를 사용할 수 있음을 의미하며

React 앱에서는 버튼, 폼, 다이얼 로그, 화면 등의 모든 것들이 흔히 컴포넌트로 표현됩니다.

예를 들어 Welcome을 여러번 렌더하는 App 컴포넌트를 만들 수 있습니다.

```javascript
function Welcome(props) {
	return <h1>Hello, {props.name}</h1>;
}

function App() {
	return (
	<div>
		<Welcome name="Lee">
		<Welcome name="Kim">
		<Welcome name="Park">
	</div>
	)
}

ReactDOM.render(
	<App />,
	document.getElementById('root')
);
```

일반적으로 새 React 앱은 최상위에 단일 App 컨포넌트를 가지고 있고, 이를 기존 앱에 통합하는 경우에는 Button과 같은 작은 컴포넌트 부터 시작해서 뷰 계층의 상단으로 올라가면서 점진적으로 작업해야합니다.

### 컴포넌트 추출

다음 Commet 컴포넌트를 살펴봅시다.

```javascript
function Comment(props) {
	return (
		<div className="Comment">
			<div className="UserInfo">
				<img className="Avatar" src={props.author.avatarUrl} alt={props.author.name}/>
				<div className="UserInfo-name">{props.author.name}>
				<div className="Comment-text">{props.text}</div>
				<div className="comment-date">{formatDate(props.date)}</div>
			</div>
		</div>
	);
}
```

위 컴포는트는 중첩구조로 이루어져 있어서 변경하기 어려울 수 있으며, 각 구성요소를 개별적으로 재사용하기도 힘듭니다. 그렇기에 몇가지 **컴포넌트를 추출**합니다.

```javascript
function Avatar(props) {
  return <img className="Avatar" src={props.user.avatarUrl} alt={props.user.name} />;
}
```

props의 이름은 사용된 context가 아닌 컴포넌트 자체의 관점에서 짓는것을 권장합니다.

이렇게 컴포넌트를 추출하는 작업을통해 재사용성을 높여 줄수있습니다.

### props는 읽기 전용입니다.

함수 컨포넌트나 클래스 컴포넌트 모두 컴포넌트 자체props를 수정해서는 안됩니다.

**모든 React 컴포넌트는 자신의 props를 다룰때 반드시 순수 함수 처럼 동작해야합니다.**
