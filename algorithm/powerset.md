## 부분집합

```javascript
function getSubsets(arr) {
  const subsets = [[]];

  arr.forEach((value) => {
    subsets.push(...subsets.map((subset) => [...subset, value]));
  });

  return subsets;
}

console.log(getSubsets([1, 2])); // [[], [1], [2], [1, 2]]
```
