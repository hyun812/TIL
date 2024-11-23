## StrictMode

- 개발 중 컴포넌트에서의 일반적인 버그를 빠르게 찾을 수 있도록 도와줌

```javascript
import { StrictMode } from 'react';
import { createRoot } from 'react-dom/client';

const root = createRoot(document.getElementById('root'));
root.render(
  <StrictMode>
    <App />
  </StrictMode>
);
```

<br/>

> React는 작성하는 모든 컴포넌트를 순수함수라고 가정하며, 동일한 입력(props, state, context)에 대해 동일한 JSX를 반환해야 함을 의미

- 컴포넌트를 두 번 렌더링하여 `순수 함수`처럼 동작하는지 확인

- 모든 `useEffect`에 셋업 + 클린업 사이클을 한번더 실행하여 클린업이 누락되어 발생하는 버그를 조기에 발견하도록 도와줌

- 더 이상 사용되지 않는 API에 대해 경고 (주로 클래스 컴포넌트에서 사용되던)

  - 클래스 생명주기, findDOMNode, 레거시 context, 레거시 문자열 refs
