# 🎈8. 제어문 part arrangement

- 제어문 : 코드블록을 실행(조건문), 반복실행(반복문) 할때 사용하는 제어문은 코드의 실행흐름을 인위적으로 제어한다.

## <블록문>

- 0개 이상의 문을 '{}' 로 묶은것
- 코드블록이라 불리운다.
- 제어문이나 함수를 정의할때 사용한다.
- 자체종결성을 가지기에 세미콜론을 붙이지 않는다.

## <조건문>

- 주어진 조건식을 평가 결과에 따라 (true,false) 블록문의 실행을 결정한다.
- 불리언 값으로 평가된다.
- if...else문과 switch문이 있다.

### if..else 문

```JAVASCRIPT
if( 조건식 ){
 //조건식이 true 이면 실행
}🦺else{
  //조건식이 false 이면 실행
}
```

- 추가 적인 조건을 주고 싶다면 🦺에 `if else( 조건식 )`을 추가 하자.

### switch 문

```JAVASCRIPT
switch (표현식) {
  case 표현식1:
    switch 문의 표현식과 표현식1이 일치하면 실행;
    break;
  case 표현식2:
    switch 문의 표현식과 표현식2가 일치하면 실행;
    break;
  default:
    switch 문의 표현식과 일치하는 표현식을 갖는 case 문이 없을 때 실행;
}
```

- 각각의 case에 `break;` 문을 사용하지 않는다면 <u>fall through</u> 현상이 발생한다.
- `default 문` 에는 더이상 밑으로 실행될 문이 없으니 `break;`를 사용하지 않아도 된다.

✨fall through 현상은 이런상황에서 발생한다.

- `break;` 문을 작성하지 않았을때!

🎆 fall through 현상은 조건문에 부합하는 표현식을 찾았을때 일어나는데 각각의 case 문에 `break;` 문이 없을경우에는 switch 문을 탈출하지 않고 default문까지 실행한다

## <반복문>

### for문

```JAVASCRIPT
for (변수 선언문 또는 할당문; 조건식; 증감식) {
  조건식이 참인 경우 반복 실행될 문;
}
```

- 주로 반복횟수가 명확할때 사용한다.

- 변수 선언문에는 일반적으로 반복을 의미하는 iteration의 i를 뜻하는 변수 i를 사용한다.

- 조건식이 참일때 까지 코드블록이 실행된다.

🧨 실행 순서는 이와 같다.

1. 변수선언문실행
2. 조건식평가
3. 참이면 코드블록실행
4. 증감식 실행 - > 다시 조건식 실행

### while문

```
var count = 0;

while (조건식) {
  console.log(count);
  증감식;
}
```

- 반복횟수가 불명확 할 때 주로 사용한다.

- 조건식의 평가 결과가 거짓이면 코드 블록을 실행하지 않고 종료한다.

- 조건식의 평가 결과가 참이면 무한루프가 되는데 그럴경우 if 문을이용해 탈출 조건을 만들고 break; 문으로 코드블록을 탈출하자

### do...while문

```
var count = 0;

do {
  console.log(count);
  증감식;
} while (조건식); // 0 1 2
```

- 거짓이면 코드블록을 실행하지 않는 while문을 보완하기위해 무조건한번은 실행하는 do...while문이 있다!

## <break 문>

- 반복문,레이블문을 탈출하는 용도로 사용한다.

## <countinue 문>

- 반복문의 코드실행을 중단하고 증감식으로 실행 흐름을 바꾼다.

```
var string = 'fastcampus';
var search = 'c';
var count = 0;

for (var i = 0; i < string.length; i++) {
  // 'c'가 아니면 현 지점에서 실행을 중단하고 반복문의 증감식으로 이동한다.
  if (string[i] !== search) continue;
  count++; // continue 문이 실행되면 이 문은 실행되지 않는다.
}
```
