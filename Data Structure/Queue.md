## Queue 이란?

Queue는 **선입선출** (First in First Out) 자료구조이다

#### 📌 JavaScript의 경우 shift() 메서드를 통해 큐를 흉내낼 수 있지만 나머지 배열 원소에 대한 재정렬이 필요하기 때문에 많은 비용이 발생함

<br>

## 연결리스트를 통한 큐 구현 (javascript)

```javascript
class Node {
  constructor(data) {
    this.data = data;
    this.next = null;
  }
}

class Queue {
  constructor() {
    this.front = null;
    this.rear = null;
    this.size = 0;
  }

  enqueue(data) {
    const newNode = new Node(data);

    if (!this.size) this.front = newNode;
    else this.rear.next = newNode;

    this.rear = newNode;
    this.size++;
  }

  dequeue() {
    if (!this.size) return null;

    const data = this.front.data;
    this.front = this.front.next;
    this.size--;
    return data;
  }
}
```
