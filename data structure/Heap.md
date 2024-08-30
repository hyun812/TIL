## Heap 이란?

힙은, 최댓값 및 최솟값을 찾아내는 연산을 빠르게 하기 위해 고안된 완전이진트리를 기본으로 한 자료구조다.

#### 📌 **완전 이진 트리** : 부모 노드 밑에 자식 노드가 최대 2개, 마지막 레벨을 제외한 모든 레벨에 노드가 완전히 채워져 있는 트리구조

#### 시간복잡도

> 삽입 : O(logn), 삭제 : O(logn)

<br>

## Heap의 종류

### 최대 힙(max heap)

부모 노드의 키 값이 자식 노드의 키 값보다 크거나 같은 완전 이진 트리

- 키 값이 가장 큰 노드를 찾기 위함
- 부모 노드의 키 값 > 자식 노드의 키 값
- 루트 노드 : 키 값이 가장 큰 노드

### 최소 힙(min heap)

부모 노드의 키 값이 자식 노드의 키 값보다 작거나 같은 완전 이진 트리

- 키 값이 가장 작은 노드를 찾기 위함
- 부모 노드의 키 값 < 자식 노드의 키 값
- 루트 노드 : 키 값이 가장 작은 노드

<br>

## 배열을 통한 최소힙 구현 (javascript)

```javascript
class Heap {
  constructor() {
    this.heap = [];
  }

  size() {
    return this.heap.length;
  }

  swap(a, b) {
    [this.heap[a], this.heap[b]] = [this.heap[b], this.heap[a]];
  }

  getParent(index) {
    return Math.floor((index - 1) / 2);
  }

  getLeftChild(index) {
    return index * 2 + 1;
  }

  getRightChild(index) {
    return index * 2 + 2;
  }

  bubbleUp() {
    let index = this.heap.length - 1;
    let parent = this.getParent(index);

    // 부모 노드가 존재하고, 새로운 노드가 부모 노드보다 작은 경우
    while (this.heap[parent] && this.heap[index] < this.heap[parent]) {
      this.swap(parent, index);
      index = parent;
      parent = this.getParent(index);
    }
  }

  bubbleDown(index) {
    let left = this.getLeftChild(index);
    let right = this.getRightChild(index);

    let minIdx = index;

    // 왼쪽 자식 노드가 존재 하면서 값이 루트 노드보다 작거나
    if (left < this.heap.length && this.heap[left] < this.heap[minIdx]) {
      minIdx = left;
    }
    // 오른쪽 자식 노드가 존재 하면서 값이 루트 노드보다 작은 경우
    if (right < this.heap.length && this.heap[right] < this.heap[minIdx]) {
      minIdx = right;
    }

    // 내가 젤 작음
    if (minIdx === index) return;

    this.swap(minIdx, index);
    this.bubbleDown(minIdx);
  }

  push(value) {
    this.heap.push(value);
    this.bubbleUp();
  }

  pop() {
    if (this.heap.length === 0) return;

    if (this.heap.length === 1) {
      return this.heap.pop();
    }

    const min = this.heap[0];
    this.heap[0] = this.heap.pop(); // 제일 뒤에 있는 원소를 제일 앞으로
    this.bubbleDown(0);

    return min;
  }
}
```
