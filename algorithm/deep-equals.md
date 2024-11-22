```javascript
const deepEquals = (o1, o2) => {
  if (o1 === o2) return true;

  if (o1 === null || o2 === null) return false; // 값 중 하나라도 null이면 (둘다 null 인경우는 위에서 true)

  if (typeof o1 !== typeof o2) return false; // type이 다르면

  if (typeof o1 === 'object') {
    const key1 = Object.keys(o1);
    const key2 = Object.keys(o2);

    if (key1.length !== key2.length) return false;

    for (const key of key1) {
      if (!deepEquals(o1[key], o2[key])) return false;
    }

    return true;
  }

  return false;
};

const obj1 = { a: 1, b: { c: 2, d: { e: 3 } } };
const obj2 = { b: { d: { e: 3, f: 4 }, c: 2 }, a: 1 };

console.log(deepEquals(obj1, obj2)); // false
```

### 주의할 점

- typeof null도 'object'로 판별하기 때문에 주의해야함
