# 컴퓨터 알고리즘 기초 8강 퀵 정렬 (Quick Sort) | T아카데미

---

## 1. 퀵 정렬 (Quicksort)

### 퀵 정렬 이란?

- Divide-and-Conquer paradigm을 사용
- partitioning - pivot 보다 작은값은 왼쪽으로, pivot보다 큰값은 오른쪽으로 정렬하는데 이것을 재귀적으로 지속하는것을 말한다.
  즉, x를 pivot 이라고 했을때 x보다 작은 것들이 모여있는 앞쪽에서 다시 pivot을 설정해서 그 pivot보다 작은것은 왼쪽, 큰것은 오른쪽으로 이동하게 하면된다.

![QuickSort01](https://user-images.githubusercontent.com/66991380/110277081-f2bce180-8017-11eb-85ee-c3abe1b5c984.jpg)

### 파티셔닝 실행 흐름!

pivot인 4와 배열의 첫번째 값인 2를 비교해서, pivot인 4보다 작으면 왼쪽에 위치하며 회색으로, 크다면 4의 오른쪽으로 위치하며 초록색으로 설정한다.

그다음, 4와 8을 비교한다.

그다음, 4와 7을 비교한다.

그다음, 4와 1을 비교했을때 4보다 작은 1은 정렬되어있는 pivot보다 큰값들중 첫번쨰 위치에 있는 8과 자리를 교체한다.

그다음, 4와 3을 비교한후, 정렬되있는 pivot보다 큰값들중 첫번째 위치에 있는 7과 위치를 교체한다.

•••

마지막으로 pivot으로 설정했던 4와 pivot보다 큰값들중 첫번째 위치에 있는 8과 위치를 교체하면 정렬이 완료된다!

![QuickSort02](https://user-images.githubusercontent.com/66991380/110277084-f3ee0e80-8017-11eb-9512-8d32845e5e20.jpg)

## 2. 퀵 정렬 (Quicksort)의 수행시간

### 수행시간 분석

- Partition에 걸리는 시간
- θ(n)

1. pivot을 정한다. (n)
2. n-1의 숫자들을 비교한다.
3. pivot보다 작으면 왼쪽, pivot보다 크면 오른쪽
4. n-1번 비교한다. - 최대 n번

- Partition의 횟수
- 경우에 따라 횟수가 달리진다.
  Balanced partitioning vs. unbalanced partitioning

### 무작위 퀵 정렬

최악의 경우를 피하기 위해 배열에서 Pivot을 무작위로 선택하는 방법이다.

기존에는 배열의 마지막 수를 기준으로 Pivot을 정했다면, 무작위 퀵정렬은 배열안에값들중 무작위로 1개의 Pivot을 정해 최악의 경우인 모두 정렬되어있는 상태를 해결할수있다.

계속 pivot을 정해서 재귀적으로 정렬해야하는데 이미 정렬되어있는 배열에서 마지막 수를 고르게되면, 최악의 경우가 발생한다.

### 정렬 알고리즘 수행시간 비교

![QuickSort03](https://user-images.githubusercontent.com/66991380/110277088-f51f3b80-8017-11eb-95c9-65c31f691b5d.jpg)

가장 빠른것은 Mergesort, Heapsort, Quicksort 3개 이고 각 상황에 따라 사용하면된다 :)

### 학습정리

**퀵 정렬은 Pivot과 partition을 이용해 크기가 작은 숫자는 계속 앞쪽으로, 큰숫자는 계속 뒤쪽으로 이동 시켜 정렬문제를 해결하는 알고리즘 이다.**

시간복잡도는 θnlgn
