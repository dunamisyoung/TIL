# 🔥 알고리즘 문제풀이

##1. 1 ~ 10000의 숫자중 8이 등장하는 횟수 구하기(Google)

1 부터 10000까지 8이라는 숫자가 총 몇 번 나오는가? 이를 구하는 함수를 완성하라.
단, 8이 포함되어있는 숫자의 갯수를 카운팅 하는것이 아니라 8이라는 숫자를 모두 카운팅 해야한다. 예를들어 8808은 3, 8888은 4로 카운팅 해야된다.
(hint) 문자열중 n 번째에 있는 문자 : Str.charAt(n) or str[n]

```javascript
function getCount8() {
  var maxium = 10000; //최대값
  var str = ''; // 모든 숫자값을 문자열로 바꿀 변수
  var strPlus = ''; // i의 값을 받을 변수
  var conunt8 = ''; // 8을 카운트할 변수

  for (var i = 1; i <= maxium; i++) {
    str = str + i; // i의 변화에 따라 i의 값을 중복으로 더한다.
    strPlus = i + ''; //i가 한번에 가져오는 수를 알기위해
    // i를 다른 변수strPlus에 담으면서 문자열로 변환합니다.

    // strPlus의 문자열길이만큼 즉, i의 문자열 길이만큼 반복횟수를 정해서 strPuls[j] === 8 이면 count8을 1++
    //아니면 다시 조건식으로 가서 j를 증가시켜 n번쨰 문자열로갑니다. (n번째 문자열로이동)
    for (var j = 0; j <= strPlus.length; j++) {
      // strPuls안에 담긴 i의 길이 만큼 반복해서 i 안에 8이 몇번있는지 알기위해
      if (strPlus[j] === '8') conunt8++;
      //결국 i가 가져온 문자열의 j번째가 8인지를 비교 확인하고 카운트를 증가
    }
  }
  console.log(conunt8);
}

getCount8(); //4000
```

##2. 이상한 문자 만들기

toWeirdCase함수는 문자열을 인수로 전달받는다.
문자열 s에 각 단어의 짝수번째 인덱스 문자는 대문자로, 홀수번째 인덱스 문자는 소문자로 바꾼 문자열을 리턴하도록 함수를 완성하라.
예를 들어 s가 ‘hello world’라면 첫 번째 단어는 ‘HeLlO’, 두 번째 단어는 ‘WoRlD’로 바꿔 ‘HeLlO WoRlD’를 리턴한다.
주의) 문자열 전체의 짝/홀수 인덱스가 아니라 단어(공백을 기준)별로 짝/홀수 인덱스를 판단한다.

```javascript
function toWeirdCase(s) {
  var strPlus = ''; // 문자열을 받을 변수
  var emptyStr = 0; // 짝수와 홀수를 구분하여 초기화를 위한 변수 초기값은 인덱스가 0부터 카운트 되니까 0으로 설정

  for (var i = 0; i < s.length; i++) {
    // 받아드린 문자열의 길이만큼 반복
    if (s[i] !== ' ') {
      // 받아들인 문자열의 i번째의 문자가 공백이 아닌지 확인
      if (emptyStr % 2 === 0) {
        strPlus += s[i].toUpperCase();
        // 받아드린 값이 나머지가 0이면 짝수이니 대문자 반환
        emptyStr++; // 공백이 아니면 1증가
      } else if (emptyStr % 2 === 1) {
        strPlus += s[i].toLowerCase();
        // 받아드린 값이 나머지가 1이면 홀수이니 소문자 반환
        emptyStr++; // 공백이 아니면 1증가
      }
    } else {
      strPlus += s[i]; // 공백인 문자열을 그대로 strPlus반환
      emptyStr = 0; // 공백이면 초기화 -> 다시 0으로
    }
  }
  return strPlus; // 마지막 반환값
}

console.log(toWeirdCase('hello world')); // 'HeLlO WoRlD'
console.log(toWeirdCase('my name is lee')); // 'My NaMe Is LeE'
```
