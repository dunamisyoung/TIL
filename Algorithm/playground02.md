# 🎈 제어문 연습문제

## 1. 변수 x가 10보다 크고 20보다 작을 떄 변수 x를 출력하는 조건식을 완성하라

```javascript
var x = 15;

if (x > 10 && x < 20) {
  console.log(x);
}
```

## 2. for 문을 사용하여 0부터 10 미만의 정수 중에서 짝수만을 작은 수부터 출력하시오.

```javascript
for (var i = 0; i < 10; i++) {
  if (i % 2 === 0) console.log(i);
}
```

## 3. for문을 사용하여 0 부터 10미만의 정수 중에서 짝수만을 작은 수부터 문자열로 출력하시오.

```javascript
var str = '';

for (var i = 0; i < 10; i++) {
  if (i % 2 === 0) str += i;
}
console.log(str);
```

## 4. for문을 사용하여 0부터 10미만의 정수 중에서 홀수만을 큰수부터 출력하시오.

```javascript
for (var i = 10; i > 0; i--) {
  if (i % 2 === 1) console.log(i);
}
```

## 5. while문을 사용하여 0 부터 10 미만의 정수 중에서 짝수만을 작은 수부터 출력하시오.

```javascript
var i = 0;

while (i < 10) {
  if (i % 2 === 0) console.log(i);
  i++;
}
```

## 6. while문을 사용하여 0 부터 10 미만의 정수 중에서 홀수만을 큰수부터 출력하시오.

```javascript
var i = 10;

while (i > 0) {
  if (i % 2 === 1) console.log(i);
  i--;
}
```

## 7. for 문을 사용하여 0부터 10미만의 정수의 합을 출력하시오.

```javascript
var num = 0;

for (var i = 0; i < 10; i++) {
  num = num + i; //num +=i
}
console.log(num);
```

## 8. 1부터 20 미만의 정수 중에서 2 또는 3의 배수가 아닌 수의 총합을 구하시오.

```javascript
var num = 0;

for (var i = 1; i < 20; i++) {
  if (i % 2 !== 0 && i % 3 !== 0) {
    num = num + i;
  }
}
console.log(num);
```

## 9. 1부터 20 미만의 정수 중에서 2 또는 3의 배수인 수의 총합을 구하시오.

```javascript
var num = 0;

for (var i = 1; i < 20; i++) {
  if (i % 2 === 0 || i % 3 === 0) {
    num = num + i;
  }
}
console.log(num);
```

10. ## 두 개의 주사위를 던졌을 때, 눈의 합이 6이 되는 모든 경우의 수를 출력하시오.

```javascript
for (var i = 1; i < 6; i++) {
  for (var j = 5; j > 0; j--) {
    if (i + j === 6) console.log([i, j]);
  }
}
```

11. ## 삼각형 출력하기 - pattern 1

```javascript
var line = 5;
var x = '';
var y = '';

for (var i = 0; i < line; i++) {
  x = x + '*';
  y = y + x + '\n';
}
console.log(y);
```

```javascript
var inLine = 1;
var x = '';
var y = '';

for (var i = 0; i < outLine; i++) {
  for (var j = 0; j < inLine; j++) {
    x = x + '*';
  }
  y = y + x + '\n';
  inLine++;
  x = '';
}
console.log(y);
```

## 12. 삼각형 출력하기 - pattern 2

```javascript
var outLine = 5;
var inLine = 5;

var x = '';
var y = '';
var z = '';

for (var i = 0; i < outLine; i++) {
  for (var j = 0; j < inLine; j++) {
    x = x + '*';
  }
  y = y + ' ';
  z = z + x + '\n' + y;
  x = '';
  inLine--;
}

console.log(z);
```

## 13. 삼각형 출력하기 - pattern 3

```javascript
var outLine = 5;
var inLine = 5;

var x = '';
var y = '';
var z = '';

for (var i = 0; i < outLine; i++) {
  for (var j = 0; j < inLine; j++) {
    x = x + '*';
  }
  y = y + x + '\n';
  x = '';
  inLine--;
}

console.log(y);
```

## 14. 삼각형 출력하기 - pattern 4

```javascript
var outLine = 5;
var inLine = 4;

var x = '';
var y = '';
var z = '';

for (var i = 0; i < outLine; i++) {
  for (var j = 0; j < inLine; j++) {
    x = x + ' ';
  }
  z = z + '*';
  y = y + x + z + '\n';
  x = '';
  inLine--;
}

console.log(y);
```

## 15. 정삼각형 출력하기

```javascript
var outLine = 5;
var inLine = 4;

var x = '';
var y = '';
var z = '';
var q = '';

for (var i = 0; i < outLine; i++) {
  q = q + y;
  for (var j = 0; j < inLine; j++) {
    x = x + ' ';
  }
  y = y + '*';
  z = z + x + y + q + '\n';
  inLine--;
  x = '';
  q = '';
}
console.log(z);
```

## 16. 역정삼각형 출력하기

```javascript
var outLine = 5;
var inLine = 4;

var x = '';
var y = '';
var z = '';
var q = '';

for (var i = 0; i < outLine; i++) {
  for (var j = 0; j < inLine; j++) {
    x = x + '*';
  }
  y = y + ' ';
  z = z + x + '*';
  q = q + x + z + '\n' + y;
  inLine--;
  x = '';
  z = '';
}

console.log(q);
```
