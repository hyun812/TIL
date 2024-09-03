<br/>

> 자바스크립트는 비동기 처리를 위한 패턴으로 콜백 함수를 사용했으나, 이는 콜백 헬로인해 가독성이 나쁘고, 에러 처리가 힘들다는 한계가 존재함

<br/>

### 콜백 헬

```javascript
function increaseAndPrint(n, callback) {
  setTimeout(() => {
    const increased = n + 1;
    console.log(increased);
    if (callback) {
      callback(increased); // 콜백함수 호출
    }
  }, 1000);
}

increaseAndPrint(0, (n) => {
  increaseAndPrint(n, (n) => {
    increaseAndPrint(n, (n) => {
      increaseAndPrint(n, (n) => {
        increaseAndPrint(n, (n) => {
          console.log('끝!');
        });
      });
    });
  });
});
```

<br/>

## Promise

> Promise는 이를 극복하기 위해 ES6에서 도입되었음

- **비동기 처리 상태와 처리 결과를 관리하는 객체**
- Promise 생성자 안에는 두 개의 매개변수를 가진 콜백 함수 (executor)를 넣게됨
  - 작업이 성공했을 때 호출 할 resolve와 실패 했을 때 호출 할 reject 함수
- Promise의 상태에는 총 3가지가 존재함
  - pending: 비동기 처리가 아직 수행되지 않은 상태
  - fulfilled: 비동기 처리가 성공한 상태
  - rejected: 비동기 처리가 실패한 상태
- fulfilled와 rejected상태를 settled 상태라고 함

```javascript
const promise = new Promise((resolve, reject) => {
  // 비동기 작업 수행
  const data = fetch('서버로부터 요청할 URL');

  if (data) resolve(data); // 만일 요청이 성공하여 데이터가 있다면
  else reject('Error'); // 만일 요청이 실패하여 데이터가 없다면
});
```

<br/>

## 프로미스의 후속 처리 메서드

- 모든 후속 처리 메서드들은 프로미스를 반환하며 비동기로 동작함

#### then()

- 두 개의 콜백함수를 인수로 전달받음
- 첫 번째 콜백함수는 비동기 처리가 성공했을 때 호출
- 두 번째 콜백함수는 비동기 처리가 실패했을 때 호출

#### catch()

- 비동기 처리가 실패했을 때 호출

#### finally()

- 프로미스의 성공 또는 실패와 상관없이 무조건 한 번 호출

```javascript
const promise = new Promise((resolve, reject) => {
  // 처리 내용
});

promise
  .then((v) => console.log(v))
  .catch((e) => console.error(e))
  .finally(() => console.log('Bye!'));
```
