## 조합

```javascript
// 조합
function getCombinations(arr, selectNum) {
  const results = [];

  if (selectNum === 1) return arr.map((el) => [el]);

  arr.forEach((fixed, index, origin) => {
    const rest = origin.slice(index + 1);
    const combinations = getCombinations(rest, selectNum - 1);
    const attached = combinations.map((el) => [fixed, ...el]);

    results.push(...attached);
  });

  return results;
}

// 중복 조합
function getCombinationsWithRepetition(arr, selectNum) {
  const results = [];

  if (selectNum === 1) return arr.map((el) => [el]);

  arr.forEach((fixed, index, origin) => {
    const rest = origin.slice(index);
    const combinations = getCombinationsWithRepetition(rest, selectNum - 1);
    const attached = combinations.map((el) => [fixed, ...el]);

    results.push(...attached);
  });

  return results;
}
```

## 순열

```javascript
// 순열
function getPermutations(arr, selectNum) {
  const results = [];

  if (selectNum === 1) return arr.map((el) => [el]);

  arr.forEach((fixed, index, origin) => {
    const rest = [...origin.slice(0, index), ...origin.slice(index + 1)];
    const permutations = getCombinations(rest, selectNum - 1);
    const attached = permutations.map((el) => [fixed, ...el]);

    results.push(...attached);
  });

  return results;
}

// 중복 순열
function getPermutationsWithRepetition(arr, selectNum) {
  const results = [];

  if (selectNum === 1) return arr.map((el) => [el]);

  arr.forEach((fixed) => {
    const permutations = getPermutationsWithRepetition(arr, selectNum - 1);
    const attached = permutations.map((el) => [fixed, ...el]);

    results.push(...attached);
  });

  return results;
}
```
