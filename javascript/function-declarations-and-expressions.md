## 함수 선언문

```javascript
function 함수명() {
  // 로직
}
```

## 함수 표현식

```javascript
var 함수명 = function 함수명() {
  // 로직
};
```

## 차이점

```javascript
// 함수 참조
console.dir(add_def); // f add_def()
console.dir(add_expr); // undefined

// 함수 호출
console.log(add_def(2, 3)); // 5
console.log(add_expr(2, 5)); // TypeError: add_expr is not a function

// 함수 선언문
function add_def(a, b) {
  return a + b;
}

// 함수 표현식
var add_expr = function (a, b) {
  return a + b;
};
```

- `함수 선언문`으로 함수를 정의하면 `함수 호이스팅`이 발생함
- `함수 표현식`으로 함수를 정의하면 `변수 호이스팅`이 발생함

> 함수 호이스팅은 함수를 호출하기 전에 반드시 함수를 선언해야 한다는 당연한 규칙을 무시하므로 함수 표현식의 사용을 권장
