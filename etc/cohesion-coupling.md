> 모듈화는 큰 규모의 코드를 작은 단위로 분리하는 것

## 응집도

- 모듈 내부 요소들간의 연관 정도
- 응집도가 높을수록 명확하고 독립적인 책임을 가지며, 코드의 이해도와 유지보수가 쉬워짐
- 단일 책임을 가지도록 설계해야함

```javascript
// 낮은 응집도 -> 하나의 함수에서 여러 기능을 수행
function handlerUser() {
  loginUser();
  printUserInfo();
  updateUserInfo();
}
```

<br/>

## 결합도

- 모듈과 모듈 간의 의존 정도
- 결합도가 높다면 하나의 구조를 변경하게 됐을 때 연관된 모듈들을 모두 수정해야하며, 이는 유지보수 측면에서 매우 안좋음
- 결합도가 낮을수록 모듈 간의 독립성이 높아짐

```javascript
// 높은 결합도 -> API URL에 직접적으로 의존하고 있음
function getUserData() {
  return fetch('https://api.example.com/users')
    .then((response) => response.json())
    .then((data) => console.log(data));
}

getUserData();

---------------------------------------------------------

// 낮은 결합도
// -> API URL을 외부에서 주입받기 때문에 URL이 변경되더라도 함수 자체는 수정할 필요가 없음
function getUserData(apiUrl) {
  return fetch(apiUrl)
    .then((response) => response.json())
    .then((data) => console.log(data));
}

const apiUrl = 'https://api.example.com/users';
getUserData(apiUrl);
```

<br/>

## 좋은 설계란?

- `높은 응집도`와 `낮은 결합도`로 유지보수성과 확장성을 높여야함
- 코드의 책임을 분리하고, 의존성을 최소화
