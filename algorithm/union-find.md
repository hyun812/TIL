### 정의

- 서로소 집합(Disjoin-Set)이라고도 함
- 해당 노드들이 서로 같은 그래프에 속하는지 판별 (합집합을 찾는 알고리즘)
- 각 집합이 서로 공통 원소를 가지지 않는 서로소 또는 상호 배타적 집합이 구해짐

```javascript
const parents = new Array(N + 1).fill(0);
// 각 노드가 각각의 집합에 포함되도록 초기화
const init = () => {
  for (let i = 0; i <= N; i++) {
    parents[i] = i;
  }
};

// 특정 노드의 부모 노드를 찾음 (해당 노드가 속한 집합의 루트 반환)
const find = (a) => {
  if (a === parents[a]) return a;
  else {
    const b = find(parents[a]);
    parents[a] = b; // 경로 압축 (Path Compression)
    return b;
  }
};

// 두 노드 a, b를 합침
const union = (a, b) => {
  let aRoot = find(a);
  let bRoot = find(b);

  if (aRoot === bRoot) return false;

  parents[bRoot] = aRoot;
  return true;
};
```
