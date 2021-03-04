# 컴퓨터 알고리즘 기초 7강 힙정렬 (2) | T아카데미

---

## 1. 힙 구조 만들기 (Building a heap)

### BUILD-MAX-HEAP

```jsx
PseudoCode
BUILD-MAX-HEAP(A)
A.heap-size = A.length
for i = ( A.length /2 ) downto 1
MAX-HEAPIFY(A,i)
```

- 배열의 길이에 절반부터 시작하는지?

i 라는 node가 있을때 부모는 i/2 왼쪽자식은 2i 오른쪽 자식은 2i + 1 로 나타낼 수있다.

자식을 가지는 첫번쨰 node가 n/2 위치에 존재한다. 그렇기에 n/2 보다 큰 위치에 있는 node들은 HEAPIFY를 할 필요성이 없다.

- 왜 거꾸로 leaf node부터 1로 가는지? - Root node → serve tree까지 조건이 만족하는지 매번 비교해야하는 번거로움이 있기에 serve tree → Root node로 조건을 비교하면 효과적으로 비교가 가능하다.

![Building01](https://user-images.githubusercontent.com/66991380/109964492-1b4f8d80-7d31-11eb-9b6c-1cd3854b2afd.jpg)

자식을 가지는 마지막 노드부터 힙정렬을 시작한다면 위 그림에서는 마지막 node인 10 그 부모인 10/2 인 5부터 정렬을 시작한다.

### MaxHeap 으로 만들기

![Building02](https://user-images.githubusercontent.com/66991380/109964502-1d195100-7d31-11eb-9697-0ab8ab4d28aa.jpg)

### 힙 구조 만들기 (Building a heap)

- 수행시간 분석

MAX-HEAPIFY를 한번 호출 할 때 마다 O(lgn)

MAX-HEAPIFY의 호출 횟수는 O(n)

따라서 전체 수행시간은 O(nlgn)

## 2. 최대값 추출 (Extract-Max)

### 최대값 추출

- Heap에서 가장 큰 값을 제거하고 Max-heap 구조를 복원하는 연산

![Building03](https://user-images.githubusercontent.com/66991380/109964505-1d195100-7d31-11eb-8d76-ad41c8a228f5.jpg)

최대값 추출을 하기전에 **Max-heap의 정의**를 되짚어보자.

- 완전 이진트리
- 부모노드가 자식노드보다 큰값을 가진다.

**Max-heap은** Root node가 전체중 가장 큰값이다.

1. 최대값 추출에 있어서 Root node와 Last node를 서로교체 한다.
   ( 배열의 첫번째 인덱스 값과 마지막 인덱스 값의 위치를 교체한다.)
   그리고나서 Last node에 위치하게된 Root node는 제외하고 ,
   ( 가장 큰 값을 뽑았다면, 배열을 하나씩 줄여 줘야한다. 그렇지 않는다면 매번 다시 원래의 값으로 돌아온다. )
2. Root node의 위치에서 MAX-HEAPIFY를 한번 실행하면된다.

### 힙 소트 (Heap Sort)

```jsx
PseudoCode
HEAPSORT(A)
BUILD-MAX-HEAP(A)
for i = (A.length /2) downto 2
exchange A[1] with A[i]
A.heap-size = A.heap-size - 1
MAX-HEAPIFY(A,i)
```

### 힙소트 실행 흐름 ⬇

![Building04 jpg](https://user-images.githubusercontent.com/66991380/109964507-1db1e780-7d31-11eb-979e-ed64e07de812.jpg)

Root node와 Last node를 교체 한다. 그리고는 Root node에 있었던 가장 큰값인 16은 제외한다. 그리고는 MAX-HEAPIFY를 실행해 가장 큰값이 Root node에 위치하게끔한다.

![Building05 jpg](https://user-images.githubusercontent.com/66991380/109964511-1ee31480-7d31-11eb-8b79-e2fc7bb9d325.jpg)

다시한번 반복적으로 실행해준다.

![Building06 jpg](https://user-images.githubusercontent.com/66991380/109964513-1f7bab00-7d31-11eb-977d-4b47e41644ad.jpg)

최종적으로 오름차순으로 정렬된 배열 형태를 가지게 된다.

전체 수행시간은 O(nlgn)

### 힙정렬 알고리즘

입력받은 배열을 MaxHeap으로 만들고 가장 큰값을 차례대로 뽑아내서 정렬하는 알고리즘이다.

시간복잡도는 θ(nlgn)
