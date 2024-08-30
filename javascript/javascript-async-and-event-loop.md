## Javascript는 싱글 스레드 언어

- 한번에 하나의 작업만 수행이 가능
- 싱글 스레드 언어가 작업을 동시에 처리할 수 있는 비동기 처리의 핵심 요소는 `Event Loop` 때문
- 브라우저나 Node.js 환경에서 이를 처린

## 내부 구성

![img](/assets/event-loop.png)

- **Javascript 엔진**
  - **Call Stack** : 자바스크립트 엔진이 코드 실행을 위해 사용하는 메모리 구조
  - **Heap** : 동적으로 생성된 자바스크립트 객체가 저장되는 공간
- **Web APIs** : 브라우저에서 제공하는 API 모음으로, 비동기적으로 실행되는 작업들을 전담하여 처리함 (AJAX 호출, 타이머 함수, DOM 조작 등)
- **Callback Queue** : 비동기적 작업이 완료되면 실행되는 함수들이 대기하는 공간
- **Event Loop :** 비동기 함수들을 적절한 시점에 실행시키는 관리자

<br/>

## Event Loop

- 브라우저 내부의 Call Stack, Callback Queue, Web APIs 등의 요소들을 모니터링 하면서 비동기적으로 실행되는 작업들을 관리하고, 실행 흐름을 제어함
- Call Stack를 주시하고 비어있으면 Callback Queue의 첫번째 콜백함수를 Call Stack로 보내주는 역할
- 작업을 옮기는 역할만을 수행하며 작업을 처리하는 주체는 자바스크립트 엔진과 Wep API

### Event Loop 동작 과정

```javascript
function bar() {
  setTimeout(() => {
    console.log('Second');
  }, 500);
}

function foo() {
  console.log('First');
}

function baz() {
  console.log('Third');
}

bar();
foo();
baz();
```

1. bar() 함수가 호출되고 그안의 setTimeout() 함수가 호출되어 스택에 쌓임
2. setTimeout() 함수의 매개변수에 할당된 콜백 함수를 Timer Web API에 전달 후 내부적으로 타이머 설정, 이후 Call Stack 에서 제거
3. 다음 foo() 함수가 호출되고 콘솔창(output)에 "First" 가 출력
4. 시간이 만료되면 이벤트 루프는 Web API에서 가지고 있던 콜백 함수를 Callback Queue 로 옮김
5. 그다음 baz() 함수가 호출되고 콘솔창에 "Third" 가 출력
6. 스택에 있는 모든 메인 자바스크립트 코드가 실행 완료 되어 Call Stack이 비워지게 됨
7. 이벤트 루프는 Call Stack 이 비어있는 것을 탐지하여, Callback Queue 에 있는 콜백 함수를 Call Stack 으로 옮김
8. Call Stack 에서 콜백 함수 코드를 실행하게 되고 콘솔창에는 "Second" 가 출력
