## Webpack 이란?

- 의존 관계에 있느 리소스(Javascript, CSS, 이미지 등)들을 하나의 파일로 번들링하는 자바스크립트 `모듈 번들러`

## Babel 이란?

- ES6 이상에서 사용되는 최신 사양의 소스코드를 구형 브라우저에서도 동작하는 ES5 사양의 소스 코드로 변환`(트랜스파일링)`하는 자바스크립트 `컴파일러`
- 최신 문법을 구형 문법으로 변환 (`const`, `class` 등)
- 다양한 브라우저 간의 호환성`(크로스 브라우징)`을 위해 사용

## Polyfill 이란?

- 브라우저에서 지원하지 않는 최신 자바스크립트 코드를 브라우저가 이해할 수 있게 지원하는 `코드 조각`
- 말 그대로 구현이 누락된 `새로운 기능`을 메꿔주는 역할 (`Promise`, `Object.assign` 등)
- 최신 기능을 제공하는 코드조각이 올바르게 실행되도록 하기 위해 사용