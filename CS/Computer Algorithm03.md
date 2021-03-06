# 컴퓨터 알고리즘 개요 (3) - T아카데미

---

## 1. 정렬문제의 정의

### 정렬문제 (Sorting problem)

**입력 (Input)**

- n개의 숫자들의 배열 [ a₁ , a₂, a₃ ]

**출럭 (Output)**

- 입력된 숫자의 배열이 a₁ ≤ a₂ ∙∙∙ ≤ a₉ 조건을 만족 하도록 다시 나열한 결과
- 오름차순 (Increasing Order)
- 내림차순 (Decreasing Order)

```jsx
Input: [5, 2, 4, 6, 1, 3];
Output: [1, 2, 3, 4, 5, 6];
```

## 2. 선택정렬 알고리즘

문제정의는 위에서 했으니 아래의 3가지에 대해 알아보도록 하자.

- 알고리즘 설명
- 정확성 증명
- 성능 분석

### 선택정렬(Selection sort)

**선택**하여 정렬하는 알고리즘

- 최소값 선택 정렬
- 가장 작은 값을 선택 (오름차순)
- 최대값 선택 정렬
- 가장 큰 값을 선택 (내림차순)

### 최소값 선택 정렬

1. 정렬되지 않은 숫자중 가장 작은 숫자선택
2. 선택한 숫자를 정렬되지 않은 숫자들중 첫번째 숫자와 자리를 교체한다
3. 모든 숫자를 옮기게 될때 까지 반복 ( 개선 → n -1 )

![minSort](https://user-images.githubusercontent.com/66991380/106908627-cf65f480-6742-11eb-9166-567dc7a67841.jpg)

### 정확성 증명

- 수학적 귀납법을 이용
- i번째 선택한 숫자가 i번쨰로 작은(혹은 큰) 숫자인지를 증명
  ( 여기서 i 번째 선택한 숫자 = 내가 n개의 숫자중 가장 작은 숫자를 선택했을때의 수를 뜻한다. )

### 성능분석

가장 작은 숫자를 찾기위한 가장 쉬운 방법?

↪ 모든 숫자들을 비교해본다.
첫번째 숫자를 min으로 두고 두번째와 세번째를 하나씩 비교해본다.
즉, 비교함수를 기준 함수로 설정하고 몇번 비교하는지 횟수를 세어본다.

- 최고차항을 Θ로 표현
- 최선/ 최악의 경우 수행시간: Θ(n²)
- 최선/ 최악의 경우 공간 : Θ(n)
- 입력 받은 숫자들의 배열이 어떤 형태이면,
- **최악(**Ω - notation**)**의 경우가 되는가? X
- **최선(**O - notation**)**의 경우가 되는가? X

선택렬에서는 항상 남아있는 숫자를 다 비교해서 그중에서 가장 작은 수를 비교하기에 최선과 최악의 경우가 없다.

### 정렬문제 정의

n개의 숫자를 오름차순이나, 내림차순으로 숫자를 재배열하여 출력하는것

### 선택정렬 알고리즘

최소값을 찾아 최소값을 맨앞으로 보내는것

1. 정렬되지 않은 수중 가장 작은수를 고른다.
2. 선택한 숫자와 정렬되지 않은 숫자들중 첫번째있는 숫자와의 자리를 교체한다.
3. 선택된 숫자가 들어간 자리까지 정렬이 되었다고 판단한다.
4. 모든 숫자를 옮길때까지 반복 ( 개선 : n - 1 까지 )

### 정확성 증명

첫번째(i) 선택하는 숫자는 n개중 가장작은수

두번째(i) 선택하는 숫자는 n-1개중 가장작은수를 선택 n개중 2번쨰로 작은수

세번째(i) 선택하는 숫자는 n-2개중 가장작은수를 선택 n개중 3번째로 작은수

즉, i 번째 선택하는 숫자가 i 번째 작은 수이다.

### 성능 분석

비교함수를 기준 함수로 정하고 n개의 함수를 매번 2개씩 짝을 지어준다.

n 개의 수가 있을때 비교횟수는 n-1

n-1 개의 수가 있을때 비교횟수는 n-2

n-2 개의 수가 있을때 비교횟수는 n-3

비교횟수의 합은? n(n-1)/2 이며 최고차항이 n² 이 되므로 시간복잡도는 (n²) 이된다.

항상 모든 수에 대해 비교를 해야 가장 작은 수를 찾을수 있기때문에

최선의 경우와 최악의 경우가 나오지 않기 떄문에 최선이나 최악의 경우를 뜻하는

O - notation, Ω - notation , 두개 모두 만족하기에 θ(n²) 라고 할수있다.
