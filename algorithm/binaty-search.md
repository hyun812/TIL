## 이분 탐색 (Binary Search)이란?

> 탐색 범위를 두 부분으로 분할하면서 찾는 방식으로 정렬되어 있는 배열에서 특정한 값을 찾아내는 알고리즘

- 시간복잡도: O(logN)

<br>

## 구현

### 📌 기본

```jsx
const binarySearch = (arr, target) => {
  let left = 0;
  let right = arr.length - 1;
  while (left <= right) {
    const mid = Math.floor((left + right) / 2);

    if (arr[mid] === target) return mid;
    else if (arr[mid] < target) left = mid + 1;
    else right = mid - 1;
  }

  return -1;
};
```

### 📌 lowerBound와 upperBound

#### 주의할점

- right = arr.length 로 설정해야함
- 결국 한 곳에서 만나기 때문에 return의 경우 left, right 상관없음

<br/>

**배열에서 원하는 값 k 이상의 수가 처음으로 나오는 위치**

```jsx
const lowerBound = (arr, target) => {
    let left = 0;
    **let right = arr.length;**
    while(left < right){
        const mid = Math.floor((left + right) / 2);

        if(arr[mid] >= target) right = mid;
        else left = mid + 1;
    }

    return left;
}
```

<br/>

**배열에서 원하는 값 k를 초과하는 수가 처음으로 나오는 위치**

```jsx
const upperBound = (arr, target) => {
  let left = 0;
  let right = arr.length;
  while (left < right) {
    const mid = Math.floor((left + right) / 2);

    if (arr[mid] > target) right = mid;
    else left = mid + 1;
  }

  return right;
};
```
