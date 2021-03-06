# 🔥 알고리즘 문제풀이

## K번째수

배열 array의 i번째 숫자부터 j번째 숫자까지 자르고, 정렬 했을때 k번째에 있는 수를 구하는 문제

### 문제

1. array라는 배열의 2번쨰 수 부터 5번째까지 자르면 [5,2,6,3]
2. 1에서 나온 배열을 정렬하면 [2,3,5,6]입니다.
3. 2에서 나온배열의 3번째 숫자는 5 입니다.

배열 array와 [i,j,k]를 원소로 가진 2차원 배열 commands가 매개 변수로 주어질 때, commands의 모든 원소에 대해 앞서 설명한 연산을 적용했을때 나온결과를 배열에 담아 return 하도록 하는 solution 함수를 작성해주세요.

### EX)

**입출력 예시**
| array | commands | return |
| :-------------: | :---------------------------------: | :-----: |
| [1,5,2,6,3,7,4] | [ `[2,5,3]`, `[4,4,1]` ,`[1,7,3]` ] | [5,6,3] |

### 풀이

```javascript
function solution(array, commands) {
    const answer = [];
    commands.map(x=> {
        let [start, end, target] = x;
        let list = array.slice(start-1, end);
        list.sort((a, b) => a-b);
        answer.push(list[target-1])
    })
    return answer;
  }
}
```

#### 평가

- 먼저 스코프의 개념이 조금 부족하였던거 같다 보완할것!
- 디스트럭쳐링 할당에 있어서 생각은 했지만, 배열과 객체를 햇갈렸던부분.
- sort 알고리즘 (quick정렬) 숫자가 유니코드에 따라 문자열로 바뀌었다가 숫자로 변경되는 부분에 있어서 정확히 알지 못하고있던점
- 원본배열을 건드리지 않는 배열함수와 원본배열을 건드리는 함수에 대해 조금더 공부할것!
