# 🎈if...else문을 삼항조건 연산자로 변경하기

## BEFORE

```javascript
var x = 11;
var res;
if (x === 0) {
  res = '영';
} else if (x % 2 === 0) {
  res = '짝수';
} else {
  res = '홀수';
}

console.log(res);
```

## AFTER

```javascript
var x = 11;
var res = x === 0 ? '영' : x % 2 === 0 ? '짝수' : '홀수';

console.log(res);
```
