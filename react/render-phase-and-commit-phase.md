> 리엑트의 렌더링 과정은 크게 `render phase`와 `commit phase` 단계로 나눌 수 있음

## 렌더 단계 (Render Phase)

- `재조정`으로 가상 DOM 요소의 변화를 감지하고 필요한 업데이트를 결정하는 단계

- 순수 계산 단계로 브라우저 화면에 아무런 변화를 주지 않음

- 리엑트는 이 단계에서 작업을 분할하고, 필요하면 작업을 중단할 수 있음

- Fiber Tree를 통해 업데이트 과정을 효율적으로 처리하고 최적화

  - 우선순위 관리

  - 작업을 쪼개고 중단 가능

  - 빠른 복구 및 재사용

<br/>

## 커밋 단계 (Commit Phase)

- 렌더 단계에서 결졍된 변경 사항들을 실제 DOM에 반영하는 단계

- 두 단계는 순차적으로 작동하며, 커밋 단계는 중단되지 않고 연속적으로 실행

- DOM이 업데이트된 후, `useEffect` 및 `useLayoutEffect`를 실행

<br/>