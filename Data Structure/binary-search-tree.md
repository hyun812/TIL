## 이진 탐색 트리란?

### 조건

- 노드의 왼쪽 하위 트리에는 노드의 키보다 작은 키가있는 노드 만 포함됩니다
- 노드의 오른쪽 하위 트리에는 노드의 키보다 큰 키가있는 노드 만 포함됩니다.
- 왼쪽 및 오른쪽 하위 트리도 각각 이진 검색 트리 여야합니다.

### 시간복잡도

> 검색, 삽입, 삭제 모두 O(logn) 다만, 한쪽으로 치우쳐진 트리라면 O(n)

## 구현

```javascript
class Node {
  constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
  }
}

class BST {
  constructor() {
    this.root = null;
  }

  getRoot() {
    return this.root;
  }

  insert(value) {
    const node = new Node(value);

    if (!this.root) {
      this.root = node;
      return;
    }

    let cur = this.root;
    while (cur) {
      if (value === cur.value) return;

      if (value < cur.value) {
        if (cur.left === null) {
          cur.left = node;
          break;
        }
        cur = cur.left;
      }

      if (value > cur.value) {
        if (cur.right === null) {
          cur.right = node;
          break;
        }
        cur = cur.right;
      }
    }
  }

  preOrder(node) {
    if (!node) return;

    console.log(node.value);
    this.preOrder(node.left);
    this.preOrder(node.right);
  }

  inOrder(node) {
    if (!node) return;

    this.inOrder(node.left);
    console.log(node.value);
    this.inOrder(node.right);
  }

  postOrder(node) {
    if (!node) return;

    this.postOrder(node.left);
    this.postOrder(node.right);
    console.log(node.value);
  }
}
```
