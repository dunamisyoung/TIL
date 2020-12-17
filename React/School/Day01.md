## 리액트를 하면서 필요한 Javascript 개념

- const let
- template string
- arrow function
- .bind(this)
- const {children} = this.props;
- ...props
- Promis
- async await
- Generator

### Generator 객체

제너레이터 객체 만드는법

function\* 함수를 호출하면 그 호출의 결과문이 제너레이터 객체이다.

yeild 는 제너레이터 객체에 next를 호출하면 다음 객체까지 간다.

이것을 이용하면 비동기적인 처이가 수월해진다.

제너레이터를 사용할때

let handle = null; 이라는 제너레이터 변수를 선언해주고 baz 라는 함수를 호출한 결과를 handle 변수에 넣어준다. 그리고 baz 라는 함수 안에있는 yield라는 것을통해 bar라는 함수가 호출되고 그안에서 handle.next('hello')라는 setTimeout 함수가 호출되는데 이러한 것은 리덕스 사가가 해주는 일이다. 리덕스 사가의 동작원리를 이해하기위해 제너레이터를 배워두는것도 좋은 방법이다.

# 개발환경 체크

지금이시대 개발자들에게 가장 중요해진것은 무엇일까 Node.js 라고 말씀하신다.

Node.js

- Installer
- nvm

Browser(Chrome)

Git

VSCode

**Uglify -** 코드가 못생기게 바뀌는것 → 즉, 알아볼수없게 바뀌는것을 **Uglify**(어글리파이)[난독화]되엇다고 말한다.

**minify -** 예를들어 **IT** 는 정보통신기술인 Information Technology를 줄여쓴말인데 정의된것이 minify → 즉, 코드를 줄여 작성하여 경량화 시키는것이다.

이런일들을 Node.js에서 도와 줄 것이다.
