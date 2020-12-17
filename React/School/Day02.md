## 리액트란?

리액트는 Rendering 과 Update를 다루는 라이브러리이다.

리액트에서 모든 view는 컴포넌트이다.

모든 작업의 단위도 컴포넌트이다.

즉 페이지 하나 하나가 컨포넌트 이다.

## 컨포넌트란?

컴포넌트는 HTML, CSS , javascript를 하나로 합쳐서 딱넣으면 동작하게끔하는것.

컴포넌트는 사람들이 매번 같은 코드를 작성해야 하는 불편함과, 그리고 재사용성을 위해서 컴포넌트화 한다 즉, 중복된 표현들을 쉽고 간단하게 표현하고 싶어졌기에 사용.

기존 HTML에서 element요소 뒤에 붙는 것을 어트리뷰트라고 칭했는데 JSX에서는 props 라고 칭한다. 물론 하나일경우에는 prop 이라고도 부르며 이는 프로퍼티의 약자이다.

```jsx
<img src="이미지 주소" />
<button class="클래스 이름">버튼</button>
<내가지은이름1 name="Mark" />
<내가지은이름 prop={false}>내용</내가지은이름>
```

태그 사이에 존재하는것을 children이라고 부른다.

```jsx
<내가지은이름 prop={false}>내용</내가지은이름>
```

위 코드를 해석해보면 {prop : false, children : 내용} 을 가진 객체이며, 이러한 객체의 이름을 props 라고 한다.

```jsx
<내가지은이름1 name="Mark" />
```

위 코드는 자식요소가 없기 떄문에 {name: Mark} 를 가진 객체이며 prop이다.

**즉, 우리가 해야하는일은, 사용자 정의 컴포넌트의 동작을 구현하는일이다.**

우리가 코드의 반복을 볼때 컴포넌트화를 하려는 생각이 들어야한다.

컴포넌트 트리는 돔트리와 똑같이 생겼다고 할 수 있다. 다른 점이라고는 html 요소 덩어리를 컴포넌트화 시킨것 뿐이다.

## Virtual DOM

가짜돔을 의미한다. 진짜 돔은 개발자 도구에서 클릭했을때의 보여지는것이 진짜 돔이다.

우리는 가짜 돔을 만들고 가짜돔을 이용해 우리가 명시한 부분과 달라진 부분을 체크해서 리액트가 진짜돔을 만들어준다. 이제는 개발자가 브라우저안에 있는 돔을 직접적으로 건들지 않겠다 라는 패러다임을 가져야한다.

진짜 돔을 우리가 제어하려고하면 매번 바뀐 부분에 대해 정확하게 파악해서 관리해주어야한다. 하지만 virtualDOM을 이용하면 우리가 일일히 바꾸어야 하는 부분을 대신 해주기에 우리는 바꾸려고 하는 부분에 대해 명시만 해주면 비교해서 자동으로 구현해준다.

## State

State는 우리가 만드려고 하는 웹사이트의 상태를 이야기한다. 상태는 쉽게 바뀔수 있다. 여기서 diff 라는것을 알아야 하는데 이는 가상DOM과 진짜DOM 에서의 차이점 이라고 할수 있다. 부모요소의 상태값이 변경되었을때 자식이 같이 렌더링될 가능성이 있고 그에따라 리액트는 가상DOM과 진짜DOM을 비교하기 시작한다. 이때 우리는 자식요소의 변화가 없을경우에는 렌더 되지 않도록 구현 해주어야한다. VirtualDOM 이 아니었다면 처음부터 끝까지 render 했어야 겠지만 VirtualDOM을 이용하면 위와 같은 기능을 구현할수 있다.

# JSX

HTML 같이 생긴 아이가 JSX 이다. 탬플릿 언어이기도하다. JSX를 제외하고는 전부다 템플릿 언어이다?

템플릿 언어와 JSX의 차이는?

JSX는 자바스크립트로 변환되는 코드이며 Javascript의 확장이다. 또한 XML의 문법규칙을 따르는것으로 알고있다. 그에 비해 탬플릿 언어는 HTML로 변환이 된다.

# transpile

JSX는 Babel과 TypeScript를 통해 브라우저가 이해할수 있는 쉬운 문법으로 변환된다.

# CSR과 SSR

## CSR

- JS가 전부 다운로드 되어 리액트 애플리케이션이 정상 실행되기 전까지는 화면이 보이지 않는다.
- JS가 전부 다운로드 되어 리액트 애플리케이션이 정상 실행된 후 화면이 보이면서 유저가 인터렉션 가능

## SSR

- JS가 전부 다운로드 되지 않아도, 일단 화면은 보이지만 유저가 사용할 수 없음.
- JS가 전부 다운로드 되어 리액트 애플리케이션이 정상 실행된 후 유저가 사용가능.

# 클라이언트와 서버와의 관계

## DNS

우리가 인터넷에 접속해서 URL을 입력하면 서버에 index.html 파일을 요청을 하게되는데 그전에 거치게 되는공간이 DNS 라는 공간이다. 이것은 도메인과 IP의 짝을 가지고 있다.

DNS는 네트워크 사업자인 KT,SKT 등등이 클라이언트에게 준다. 그럼 DNS 서버가 클라이언트에게 준 IP 주소를 받고 그 다음 그 IP에 따른 서버로 HTTPS를 요청한다. HTTPS 를 사용하면 우리가 보낸 요청을 암호화 시켜서 전달한다. 이때 명시적으로 라우터를 지정하지 않는다면, `/` 로 서버에 요청하는데 이떄 이것이 index.html로 바뀐다. 이렇게 index.html을 받은 서버는 사용자에게 index.html을 내려준다. 만약 사용자가 로그인 이후에 mail로 접속하게 된다면 그때는 사용자 로그인에 따른 토큰 이라는 것을 가지고 사용자에게 줄파일을 서버에서 만들어서 준다. 이러한 방식이 **서버사이드 렌더링(SSR)**이다. 즉, 서버안에서 템플릿 언어를 통해 문자열을 덩어리로된 페이지를 만들어서 클라이언트에게 보내주는것이다.

## CSR

클라이언트들이 가지고 있는 기기의 성능이 좋아졌기에 **CSR** 방식을 사용한다. CSR도 SSR과 동일하게 웹브라우저 접속후에 페이지를 요청한다. 이때 서버는 index.html 파일을 전달하는데 이때 빈껍데기를 전달하고, 그안에는 script 태그로 감싸진 리액트가 전달된다. 리액트를 전달 받은 브라우저는 내용물을 해석한다. 아무 문제가 없으면 render 함수를 호출하면서 사용자 화면을 렌더링한다.

만약 사용자가 다른 Router로 이동하고자 할때는 SCR과 같이 서버에 다녀오는것이아니라. 자체적으로 정해놓은 Router와 맞는 페이지로 바꾸어 끼워준다. 그렇다고 온전히 서버에 다녀오지 않는것은 아니다. 만약 사용자가 mail이라는 라우터를 서버에 요청하면 서버는 사용자와 맞는 DB를 가져다가 클라이언트에게 전달한다. SSR은 각 페이지에 맞는 문자열을 서버에서 그려서 전달했지만, 이제는 그렇지 않다. 즉, 서버는 APISever의 역할만 하는것이다.

서버는 요청에따라 JSON 파일을 내려준다. 물론 요청시에도 JSON을 요청한다.

## REST

WebAPI와 RESTAPI의 가장 결정적 차이점은 무엇이냐면 API를 보면 어떤일을 하는지 다 알수 있다는 것이고, WebAPI는 어떤일을 하는지 알수 없는것 이부분은 천천히 알아보도록하자.

[그런 REST API로 괜찮은가](https://www.youtube.com/watch?v=RP_f5dMoHFc) 를 통해 알아보자 :)

이런 어려운 RESTAPI 떄문에 나온것이 GraphQL 이다.

## GraphQL

이것을 통해서 서버와 클라이언트가 통신을 하기 시작한다. 이것도 일단은 나중에 알아보자.

RESTAPI 는 정해진 형식을 요청하고 받아야 하는 형태이지만, GraphQL은 클라이언트에서 원하는 데이터를 가져와야할때 서버에 Query을 날릴수 있는 형태라고한다. 즉, 자유롭게 서버에게 데이터를 요청하고 RESTAPI보다 좀 더 유연하다고 할수있다.

# React Client Side Rendering

- 서버에서 받은 빈껍데기 HTML
- 브라우저가 서버에서 JS링크에 해당하는 주소로 부터 다운로드
- 브라우저가 다운로드 받은 JS를 실행
- 브라우저가 React 실행 → 리액트가 실행 직후 해당 경로에 해당하는 페이지를 렌더
- 렌더링이 끝나면 화면이 보이고 그때부터 실행가능

렌더링 전까지는 안보인다.!

# Cashing

- 처음으로 사이트에 접속했을 때 다운로드 받을것을 로컬 캐싱화 한다 → 사용자가 처음 페이지를 열지 않았다면 렌더 중간에 행동들을 생략해준다.

# React Server Side Rendering

- 서버에서 렌더링된 받은 문자열로 만들어진 HTML
- 브라우저가 JS 링크를 받자마자 페이지가 화면에서 보여진다. → 화면에는 보이지만 동작할수 없는상태
- 브라우저가 리액트실행 → 동작안됨
- 실행 이후 페이지에 맞는 리액트 컴포넌트가 나타났을떄 동작 및 diff 확인후 랜더링

처음은 SCR방식 → 렌더직전에 CSR로 동작하게 한다.

# React 라이브러리

## 리액트가 하는일

핵심묘듈 2개로 리액트가 하는일은 크게 두가지

- **'react' - 리액트를 가지고 컴포넌트 만들기**
- **'react-dom' - 페이지를 그리는 역할을 하는 라이브러리**

즉, 컨포넌트 만들기는 'react' 이고 만든 컴포넌트를 실제 DOM 에 그릴떄는 'react-dom' 이라는 라이브러리를 React 에서 import 해서 사용한다.

**'react-dom' 은 render라는 메서드를 사용한다. 사용방법은 아래와 같다.**

```jsx
ReactDOM.render(
	<Hello name="Video" />,
	document.getElemnetById('Hello')
);
---

class Hello extends React.Component(
	render(){
		return (
			<div>
				Hello {this.props.name}
			</div>
		)
	}
)

ReactDOM.render(
	<Hello name="Video" />,
	document.getElemnetById('Hello')
);
```

위 코드를 통해 Hello라는 컴포넌트를 Hello가 위치한 DOM에 ReactDOM이 그려준다.

# { React 컴포넌트 } - JS, JSX

만들어진 리액트 컴포넌트를 실제 HTMLElement에 연결할 때 ReactDOM 라이브러리를 이용합니다.

- render
- hydrate
- unmountComponentAtNode()
- findDOMNode()
- createPortal()

위 메서드중 render랑 createPortal정도만을 사용하며 render는 필수적으로 한번은 사용해주어야합니다.

# { React 컴포넌트 } 만들기

제일 큰범위를 차지하고있는 두부분만 말하자면 Hooks 와 LifeCycle 이라고할 수 있겠다.

## CDN - content Delivery Network

컨텐츠를 제공하기 위해 만들어 놓은 네트워크이다. 이것을 통해 컴퓨터에 Library를 설치하지 않고 React 개발을 할수있다. 하지만 제한적인 부분이 있다.

CDN은 개발용과 , 프로덕션 용으로 나뉘며 프로덕션용은 경량화를 위해 minify 처리되어있다.

# Use React, ReactDOM with Library CDN

폴더를 하나만들고 `npm init -y` 를 통해 Node.js를 통해 프로젝트를 관리하겠다고 명시해준다.

`npm i serve -D` 를 통해 개발용으로 사용하겠다고 지정해준다.

만든 폴더로 들어가서 `npx serve` 를 사용해준다.

여기서의 npx는 node_module 안에있는 `.bin/serve` 라는 파일을 찾아 실행시켜주는 역할이다.

`npx serve`를 실행하면 localhost:5000이 열린다.

src 폴더를 하나 만들어보자.

index.html을 만들고 아래와 같이 코드를 작성해준다.

```jsx
<!DOCTYPE html>
<html lang="ko-KR">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <h1>Hello</h1>
  </body>
</html>
```

그리고 `npx serve src` 를 작성해준다. localhost:5000이 열리는지 확인한다.

새로고침을하면 Hello가 적힌 페이지가 보여진다.

그리고는 body 밑에 CDN 을 붙여 넣어준다.

```jsx
<!DOCTYPE html>
<html lang="ko-KR">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <h1>Hello</h1>
			<script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
			<script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
			<script>
				console.log(ReactDOM);
				console.log(React);

				ReactDOM.render(
					document.querySelector('#root');
				);
			</script>
  </body>
</html>
```

개발자 도구를 들어가보니 Object 2개가 들어가있고 ReactDOM 을 통해 render를 해보자.

아래와 같은 코드를 적어보니 안녕하세요가 출력된다.

```jsx
<!DOCTYPE html>
<html lang="ko-KR">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <h1>Hello</h1>
    <script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
    <script>
      console.log(ReactDOM);
      console.log(React);

      const Component = () => React.createElement('p', null, '안녕하세요');

      ReactDOM.render(React.createElement(Component, null, null), document.querySelector('#root'));
    </script>
  </body>
</html>
```

위코드는 ReactDOM이 컴포넌트를 가져와서 render하는 코드이다. 고작 안녕하세요 라는 글씨를 웹페이지에 나타내는데 이정도의 코드를 적어야한다.

JSX & Babel이 이러한 번거로움을 덜어준다.

즉, HTML처럼보이는 코드를 작성했을떄 위에서 풀어서 적은 코드처럼 변환후 DOM에 랜더링 시켜주는 역할을한다.

# Babel

```jsx
<!DOCTYPE html>
<html lang="ko-KR">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <h1>Hello</h1>
    <script crossorigin src="https://unpkg.com/react@17/umd/react.development.js"></script>
    <script crossorigin src="https://unpkg.com/react-dom@17/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
    <script type="text/babel">
      console.log(ReactDOM);
      console.log(React);

      const Component = () => {
        <div>
          <h1>목록</h1>
          <ul>
            <li>
              <span>자바</span>스크립트
            </li>
            <li>타입스크립트</li>
          </ul>
        </div>;
      };

      const Component = () => React.createElement('p', null, '안녕하세요');

      ReactDOM.render(<Component />, document.querySelector('#root'));
    </script>
  </body>
</html>
```

위 와같이 작성해보자 이렇게 하면 script 안에 있던 파일을 바벨이 컴파일 하여 실행시켜준다.

다시 localhost를 보면 자바스크립트 타입스크립트가 추가된 화면을 볼수있다.

JSX가 HTML과 다른결정적인 것은 JSX는 **XML규칙**을 따른다.

## JSX 문법

- 최상위 요소가 하나여야 합니다.
- 최상위 요소를 리턴하는 경우, ()로 감싸야합니다.
- 자식들을 바로 랜더링하고 싶다면, <> </> 를 사용합니다. ⇒ 이름은 Fragment
- 자바스크립트 표현식을 사용하려면, {표현식}를 이용합니다.
- if 문은 사용할 수 없습니다. - 삼항조건 연산자 혹은 && 연산자를 사용합니다.
- style을 이용해 인라인 스타일링이 가능하게 합니다. - 카멜 케이스를 이용한다.
- class 대신 className 을 사용해 class를 적용할 수 있습니다.
- 자식요소가 있으면, 꼭 닫아야 하고, 자식요소가 없으면 열면서 닫아야 합니다.

```jsx
<p>어쩌구<p>
<br/>
```
