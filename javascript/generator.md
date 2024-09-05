## 제너레이터란?

> 코드 블록의 실행을 일시 중지했다가 필요한 시점에 재개할 수 있는 특수한 함수

- 제너레이터가 함수가 반환한 객체는 이터러블이면서 동시에 이터레이터임
- `function*` 키워드로 선언
- 하나 이상의 yield 표현식을 포함함
- 화살표 함수로 정의할 수 없음

<br/>

### 일반함수와의 차이점

1. 제너레이터 함수는 함수 호출자에게 함수 실행의 제어권을 양도할 수 있음
2. 제너레이터 함수는 함수 호출자와 함수의 상태를 주고받을 수 있음
3. 제너레이터 함수를 호출하면 제너레이터 객체를 반홤함

<br/>

## 제너레이터의 일시 중지와 재개

- `yield` 는 제네레이터 함수를 멈추거나 다시 시작하게 하는데 사용되는 키워드
- next 메서드를 호출하면 yield 표현식까지 실행되고 일시 중지 (함수의 제어권이 호출자로 양도됨)
- next 메서드에 전달한 인수는 제너레이터 함수의 yield 표현식을 할당받는 변수에 할당됨
- **yield 표현식의 평가 결과가 할당되지 않는 것에 주의**

<br/>

```javascript
function* getFunc() {
  // 첫 번째 next를 호출하면 첫 번째 yield 표현식까지 실행되고 일시 중지
  // x에는 아직 아무것도 할당되지 않고 next 메서드가 두 번째 호출될 때 결정됨
  // 1 은 next 메서드가 반환한 이터레이터 리절트 객체의 value 프로퍼티에 할당
  const x = yield 1;

  // 두 번째 next를 호출하면 두 번째 yield 표현식까지 실행되고 일시 중지
  // 두 번째 next 메서드가 호출되면 전달한 인수 10은 x 변수에 할당됨
  // y에는 아직 아무것도 할당되지 않고 next 메서드가 세 번째 호출될 때 결정됨
  // x + 10 은 next 메서드가 반환한 이터레이터 리절트 객체의 value 프로퍼티에 할당
  const y = yield x + 10;

  // 세 번째 next를 호출하면 함수 끝까지 실행
  // 세 번째 next 메서드가 호출되면 전달한 인수 20은 y 변수에 할당됨
  // x + y 는 next 메서드가 반환한 이터레이터 리절트 객체의 value 프로퍼티에 할당
  return x + y;
}

const generator = getFunc(0);

let res = generator.next();
console.log(res); // {value: 1, done: false}

res = generator.next(10);
console.log(res); // {value: 20, done: false}

res = generator.next(20);
console.log(res); // {value: 30, done: true}
```
