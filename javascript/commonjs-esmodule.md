> CommonJS와 ES Module는 자바스크립트에서 모듈을 관리하고 불러오는 두 가지 주요 방식

<br/>

## Common JS

- 주로 Node.js 환경에서 사용
- `동기적`으로 모듈을 로드 (모듈이 로드될 때까지 다음 코드가 실행되지 않는 방식)

```javascript
// CommonJS
const module = require('./module'); // 모듈 가져오기
module.exports = { key: 'value' }; // 모듈 내보내기
```

<br/>

## ES Module (ESM)

- 브라우저와 Node.js환경 모두 지원
- `비동기적`으로 모듈을 로드
- 정적분석이 가능하므로 Tree Shaking이 용이함

```javascript
// ES Module
import module from './module.js'; // 모듈 가져오기
export const key = 'value'; // 모듈 내보내기
```

### 용어 정리

- 정적 분석: 소스 코드를 실행하지 않고 코드의 의존성과 사용 여부를 분석하는 것
- Tree Shaking: 사용되지 않는 코드를 제거하여 번들 크기를 줄이는 최적화 기법
