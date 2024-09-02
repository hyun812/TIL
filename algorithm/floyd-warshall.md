## 플로이드-워셜 알고리즘

- 가중 그래프에서 간선 가중치의 합이 최소가 되는 경로를 찾는 알고리즘 중 하나
- 모든 정점으로 부터 모든 정점까지의 최단 경로를 구할 수 있음
- 시간복잡도: O(n^3)

<br/>

## 구현

- **경유지를 거쳐가는 경로의 비용이 더 적다면 갱신하는 방식 (k=경유지)**
- 자기 자신으로 가는 경로는 0으로 초기화
- 갈 수 없는 경로는 Infinity로 초기화

```javascript
const floydWarshall = (dist) => {
  for (let k = 0; k < len; k++) {
    for (let i = 0; i < len; i++) {
      for (let j = 0; j < len; j++) {
        if (dist[i][j] > dist[i][k] + dist[k][j]) {
          dist[i][j] = dist[i][k] + dist[k][j];
        }
      }
    }
  }
};
```
