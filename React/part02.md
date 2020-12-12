# 엘리먼트 렌더링

엘리먼트는 React앱의 가장 작은 단위입니다.

엘리먼트에는 화면에 표시할 내용을 기술합니다.

```javascript
const element = <h1>Hello, world</h1>;
```

[브라우저 DOM 엘리먼트](https://velog.io/@godori/DOM%EC%9D%B4%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80)와 달리 React 엘리먼트는 일반 객체이며 쉽게 생성가능하다.

**ReactDOM**은 React 엘리먼트와 일치하도록 DOM을 업데이트합니다.

### DOM에 엘리먼트 렌더링하기

HTML 파일 어딘가에 <div>가 있다고 가정했을때

```javascript
<div id="root"></div>
```

root라는 DOM안에 들어가는 모든 엘리먼트를 React DOM에서 관리 하며 이것을 **루트DOM** 이라고 하며 React로 구현된 애플리케이션은 보통 하나의 DOM노드가 있습니다.

React엘리먼트를 루트DOM 노드에 렌더링 하려면 둘 다 ReactDOM.render()로 전달하면됩니다.

```javascript
const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```

### 렌더링 된 엘리먼트 업데이트하기

React 엘리먼트는 불변객체입니다.

엘리먼트를 생성한 이후에는 해당 엘리먼트의 자식이나 속성을 변경할수없습니다.

### 변경된 부분만 업데이트하기

React DOM은 해당 엘리먼트와 그 자식 엘리먼트를 이전의 엘리먼트와 비교하고 DOM을 원하는 상태로 만드는데 변경사항이 있는 경우에만 DOM을 업데이트 합니다.

즉, 과거와 현재를 비교해서 과거를 기준으로 변한 값이 있다면, 바뀐 부분만 새롭게 업데이트합니다.

만약, 부모엘리먼트가 변경되었다면, 자식엘리먼트도 같이 렌더링 됩니다.
