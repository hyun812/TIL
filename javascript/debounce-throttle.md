## 디바운스

- 특정 시간 동안 이벤트가 발생하지 않을 때 마지막 이벤트를 처리하는 기법

- 짧은 시간 간격으로 이벤트가 발생하면 호출하지 않다가 일정 시간이 경과된 후에 이벤트 핸들러가 한 번만 호출되도록 함

- 사용자 입력 처리, 폼 제출 등

```javascript
const debounce = (callback, delay) => {
  let timerId;

  // debounce 함수는 timerId를 기억하는 클로저를 반환
  return (...args) => {
    // delay가 경과하기 이전에 이벤트가 발생하면 이전 타이머를 취소하고 새로운 타이머를 재설정
    // 따라서 delay 보다 짧은 간격으로 이벤트가 발생하면 callback은 호출되지 않음
    if (timerId) clearTimeout(timerId);
    timerId = setTimeout(callback, delay, ...args);
  };
};
```

<br/>

## 스로틀

- 일정 시간 간격으로 이벤트 처리하는 기법

- 짧은 시간 간격으로 연속해서 발생하는 이벤트를 그룹화해서 일정 시간 단위로 이벤트 핸들러가 호출되도록 호출 주기를 만듬

- 스크롤, 리사이즈, 마우스 이동 등

```javascript
const throttle = (callback, delay) => {
  let timerId;

  // throttle 함수는 timerId를 기억하는 클로저를 반환
  return (...args) => {
    // delay가 경과하기 이전에 이벤트가 발생하면 아무것도 하지 않다가
    // delay가 경과했을 때 이벤트가 발생하면 새로운 타이머를 재설정
    // 따라서 delay 간격으로 callback 호출
    if (timerId) return;
    timerId = setTimeout(() => {
      callback(...args);
      timerId = null;
    }, delay);
  };
};
```
