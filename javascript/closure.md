## 클로저란 ?

- 함수와 그 **함수가 선언됐을 때의 렉시컬 환경(Lexical environment)**과의 조합
- 반환된 내부 함수가 자신이 선언됐을 때의 환경인 스코프를 기억하여 소멸된 이후에도 그 환경에 접근할 수 있음을 의미
- 즉 자신이 생성될 때의 환경을 기억하는 함수

<br/>

```javascript
// 외부 함수
const outer = () => {
  // 카운트 상태를 유지하기 위한 자유 변수
  let count = 0;

  // 내부 함수
  const inner = () => {
    return ++count;
  };
  return inner; // 클로저를 반환
};

const counter = outer();
// outer 함수가 종료됐지만 count는 inner 함수를 통해 접근 가능함
console.log(counter()); // 1
console.log(counter()); // 2
console.log(counter()); // 3
```

> 외부에서 직접 접근할 수 없는 변수의 상태를 유지하면서도 특정 함수에 의해 접근 가능하며 이는 부수효과를 최대한 억제하고 안정성을 높일 수 있음
