## 부분집합

```javascript
const getSubsets = function (arr) {
  let flag = new Array(arr.length).fill(false);
  const subSets = [];

  const subSet = (depth) => {
    if (depth === arr.length) {
      const subSet = arr.filter((el, index) => flag[index]);
      subSets.push(subSet);
      return;
    }

    flag[depth] = true;
    subSet(depth + 1);
    flag[depth] = false;
    subSet(depth + 1);
  };

  subSet(0); // depth 0 부터 시작
  return subSets;
};
const example = [1, 2, 3];
const result = getSubsets(example);
console.log(result);
```
