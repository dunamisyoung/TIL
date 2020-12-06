# 🔥 알고리즘 문제풀이

## 2. 정렬

## 2. - 1 정렬확인

주어진 배열(array)이 정렬되어 있다면 true, 그렇지 않다면 false를 반환하는 함수를 구현하라. 단, 어떠한 빌트인 함수도 사용하지 않고 for 문을 사용하여 구현하여야 한다.

### 문제

```javascript
function isSorted(array) {}

console.log(isSorted([1, 2, 3, 4, 5])); // true
console.log(isSorted([2, 3, 4, 1, 5])); // false
```

### 풀이

```javascript
function isSorted(array) {
  let str = '';
  let imagine = '';
  let result = '';

  for (let i = 0; i < array.length; i++) {
    str = str + array[i];
  }

  for (let j = 0; j < array.length; j++) {
    imagine = imagine + array[0]++;
  }

  if (str === imagine) result = true;
  else result = false;

  return result;
}
console.log(isSorted([1, 2, 3, 4, 5])); // true
console.log(isSorted([2, 3, 4, 1, 5])); // false
```

```javascript
function isSorted(array) {
  for (let i = 0; i < array.length; i++) {
    if (array[i] > array[i + 1]) return false;
  }
  return true;
}

console.log(isSorted([1, 2, 3, 4, 5])); // true
console.log(isSorted([2, 3, 4, 1, 5])); // false
```

## 2. - 2 버블 정렬

- 버블 정렬(buble sort)은 순차적으로 배열을 순회하면서 인접한 두 요소를 비교하여 작은 요소를 왼쪽으로, 큰 요소를 오른쪽으로 교환한다.
- 버블 정렬은 가장 간단하지만 가장 느린 정렬 알고리즘이다.
- 시간 복잡도: O(n2)

버블 정렬을 통해 주어진 배열(array)을 정렬하는 함수를 구현하라. 단, 어떠한 빌트인 함수도 사용하지 않고 for 문을 사용하여 구현하여야 한다.

### 문제

```javascript
function bubbleSort(array) {}

console.log(bubbleSort([2, 4, 5, 1, 3])); // [1, 2, 3, 4, 5]
console.log(bubbleSort([5, 2, 1, 3, 4, 6])); // [1, 2, 3, 4, 5, 6]
console.log(bubbleSort([3, 1, 0, -1, 4, 2])); // [-1, 0, 1, 2, 3, 4]
```

### 풀이

```javascript
function bubbleSort(array) {
  let imagine = '';
  for (let i = 0; i < array.length; i++) {
    for (let k = 0; k < array.length; k++) {
      if (array[k] > array[k + 1]) {
        imagine = array[k];
        array[k] = array[k + 1];
        array[k + 1] = imagine;
      }
    }
  }
  return array;
}

console.log(bubbleSort([2, 4, 5, 1, 3]));
console.log(bubbleSort([5, 2, 1, 3, 4, 6]));
console.log(bubbleSort([3, 1, 0, -1, 4, 2]));
```
