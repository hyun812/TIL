> 💡 **주된 차이점은 원본 배열의 변경 유무**

</br>

# slice()

```jsx
const animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];

console.log(animals.slice(2));
// ["camel", "duck", "elephant"]

console.log(animals.slice(2, 4));
// ["camel", "duck"]

console.log(animals.slice(1, 5));
// ["bison", "camel", "duck", "elephant"]

console.log(animals.slice(-2));
// ["duck", "elephant"]

console.log(animals.slice(2, -1));
// ["camel", "duck"]

console.log(animals.slice());
// ["ant", "bison", "camel", "duck", "elephant"]
```

```jsx
arr.slice([begin[, end]])
```

- `begin` : 시작점에 대한 인덱스를 의미, 음수 인경우 배열의 끝에서부터의 길이를 나타냄
- `end` : 추출을 종료할 기준 인덱스를 의미, end인덱스는 제외하고 추출함
- 추출한 요소를 포함한 새로운 배열을 반환
- **원본 배열의 값은 절대 건드리지 않음**

</br>

# splice()

```jsx
const months = ['Jan', 'March', 'April', 'June'];
months.splice(1, 0, 'Feb');
// Inserts at index 1
console.log(months);
// ["Jan", "Feb", "March", "April", "June"]

months.splice(4, 1, 'May');
// Replaces 1 element at index 4
console.log(months);
// ["Jan", "Feb", "March", "April", "May"]
```

```jsx
array.splice(start[, deleteCount[, item1[, item2[, ...]]]])
```

- `start` : 배열의 변경을 시작할 인덱스를 의미, 음수인 경우 배열의 끝에서부터의 길이를 나타냄
- `deleteCount` : 배열에서 제거할 요소의 수
- `item1, item2, <em>...</em>` : 배열에 추가할 요소
- 제거한 요소를 담은 배열을 반환
- **새로운 배열이 반환될 뿐만 아니라 원본 배열도 변경됨**
