## Trie란?

- 문자열을 저장하고 효율적으로 탐색하기 위한 트리 형태의 자료구조
- 자동 완성, 사전 검색, 철자 검사 및 교정, 문자열 패턴 매칭 등 문자열을 탐색하는데 특화되어 있음
- 저장곤간을 많이 차지한다는 단점
- 시간 복잡도: o(M)
  - M 은 문자열의 길이

## 구현

```javascript
class Node {
  constructor(value = '') {
    this.value = value;
    this.isEndOfWord = false; // insert된 단어인지
    this.child = new Map();
  }
}

class Trie {
  constructor() {
    this.root = new Node();
  }

  insert(word) {
    let cur_node = this.root;

    for (const char of word) {
      if (!cur_node.child.has(char)) {
        cur_node.child.set(char, new Node(cur_node.value + char));
      }
      cur_node = cur_node.child.get(char);
    }
    cur_node.isEndOfWord = true;
  }

  //자동 완성 함수
  autoComplete(word) {
    let cur_node = this.root;
    let result = [];

    // word 문자열까지 노드 이동
    for (const char of word) {
      if (!cur_node.child.has(char)) {
        return [];
      }
      cur_node = cur_node.child.get(char);
    }

    const queue = [cur_node];

    while (queue.length) {
      const { value, isEndOfWord, child } = queue.shift();

      if (isEndOfWord) {
        // insert 되어있는 단어라면 result에 추가
        result.push(value);
      }

      for (const childNode of child.values()) {
        queue.push(childNode);
      }
    }
    return result;
  }

  // 요소 존재 유무
  has(word) {
    let cur_node = this.root;

    for (const char of word) {
      if (!cur_node.child.has(char)) {
        return false;
      }
      cur_node = cur_node.child.get(char);
    }
    return true;
  }
}

const trie = new Trie();
trie.insert('cat');
trie.insert('can');
trie.insert('par');
trie.insert('p');
trie.insert('party');
trie.insert('pan');
trie.insert('peek');

console.log(trie.autoComplete('p')); //['p', 'par', 'party', 'pan', 'peek']
console.log(trie.autoComplete('ca')); //['cat', 'can']
```
