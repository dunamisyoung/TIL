# 🔥 알고리즘 문제풀이

## 2. 정렬

## 2. - 3 선택 정렬

- 선택 정렬(selection sort)은 배열의 최소값을 검색하여 배열의 왼쪽부터 순차적으로 정렬을 반복하는 정렬 알고리즘이다.
- 배열이 미정렬 상태이므로 최소값 검색에는 이진 검색이 아닌 선형 검색 알고리즘을 사용한다.
- 선택 정렬은 버블 정렬보다 빠르다.
- 시간 복잡도: O(n2)

선택 정렬을 통해 주어진 배열(array)을 정렬하는 함수를 구현하라. 단, 어떠한 빌트인 함수도 사용하지 않고 for문을 사용하여 구현하여야 한다.

```javascript
function selectionSort(array) {}

console.log(selectionSort([3, 1, 0, -1, 4, 2])); // [-1, 0, 1, 2, 3, 4]
console.log(selectionSort([2, 4, 5, 1, 3])); // [1, 2, 3, 4, 5]
console.log(selectionSort([5, 2, 1, 3, 4, 6])); // [1, 2, 3, 4, 5, 6]
```

```javascript
function selectionSort(array) {
  var x;

  for (var i = 0; i < array.length; i++) {
    for (var j = 0; j < array.length; j++) {
      if (array[i] < array[j]) {
        x = array[j];
        array[j] = array[i];
        array[i] = x;
      }
    }
  }

  return array;
}
console.log(selectionSort([3, 1, 0, -1, 4, 2])); // [-1, 0, 1, 2, 3, 4]
console.log(selectionSort([2, 4, 5, 1, 3])); // [1, 2, 3, 4, 5]
console.log(selectionSort([5, 2, 1, 3, 4, 6])); // [1, 2, 3, 4, 5, 6]
```

```javascript
function selectionSort(array) {
  for (let i = 0; i < array.length; i++) {
    let mini = i;
    for (let j = i + 1; j < array.length; j++) {
      if (array[mini] > array[j]) {
        // j를 순회하면서 array[mini]가 array[j] 보다 작을때 j의 index값을 mini변수에 저장
        mini = j;
      }
    }
    if (mini !== i) {
      let imagine = array[mini];
      array[mini] = array[i];
      array[i] = imagine;
    }
  }
  return array;
}
console.log(selectionSort([3, 1, 0, -1, 4, 2])); // [-1, 0, 1, 2, 3, 4]
console.log(selectionSort([2, 4, 5, 1, 3])); // [1, 2, 3, 4, 5]
console.log(selectionSort([5, 2, 1, 3, 4, 6])); // [1, 2, 3, 4, 5, 6]
```
