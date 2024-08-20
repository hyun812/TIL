## Storybook란?

- 스토리북은 UI 컴포넌트를 독립적으로 개발하고 테스트할 수 있게 해주는 오픈소스 도구
- UI 컴포넌트의 개발, 테스트 및 문서화를 지원

<br/>

## Storybook의 장점

- 독립적인 환경에서 UI 컴포넌트를 개발 및 테스트
- 문서화를 자동화하여 팀원이 컴포넌트의 사용 방법과 옵션을 쉽게 이해할 수 있음
- 스토리북의 다양한 애드온을 활용하여, 디자인 가이드라인, 접근성 검사 등 추가적인 기능을 확장

<br/>

## Storybook 세팅 및 구성

### 1. 설치

```
$ npx storybook@latest init
```

### 2. 루트 경로에 `.storybook` 폴더

**.storybook/main.js**
<br/>
storybook을 위한 config 설정

```javascript
import type { StorybookConfig } from '@storybook/react-vite';

const config: StorybookConfig = {
  stories: ['../src/**/*.mdx', '../src/**/*.stories.@(js|jsx|mjs|ts|tsx)'],
  addons: [
    '@storybook/addon-links',
    '@storybook/addon-essentials',
    '@storybook/addon-onboarding',
    '@storybook/addon-interactions',
  ],
  framework: {
    name: '@storybook/react-vite',
    options: {},
  },
  docs: {
    autodocs: 'tag',
  },
};

export default config;
```

**.storybook/preview.js**
<br/>
해당 프로젝트의 모든 story에 대해 global하게 적용될 포맷을 세팅

```javascript
import type { Preview } from '@storybook/react';

// 해당 프로젝트의 모든 story에 대해 global하게 적용될 포맷을 세팅하는 곳
const preview: Preview = {
  parameters: {
    actions: { argTypesRegex: '^on[A-Z].*' },
    // 개발자가 따로 코드를 변경하지 않고 storybook에서 arguments를 동적으로 바꿔가며 인터렉션 할 수 있도록 함
    controls: {
      matchers: {
        // {데이터 타입}: 테스트 할 정규식 표현
        color: /(background|color)$/i,
        date: /Date$/i,
      },
    },
  },
};

export default preview;
```

<br/>

## Story 파일 작성

> story 파일은 development-only로 production bundle에는 포함되지 않음

> 파일 형식은 .stories.tsx를 따름

<br/>

## Story의 주요 객체 및 속성

### 1. meta

- 스토리의 메타 정보 정의

### 2. title

- 현재 스토리의 제목을 정의
- storybook에서 스토리의 위치 및 구조를 결정하는데 사용
- `/` 를 통해 계층 구조를 설정할 수 있음

### 3. component

- 현재 스토리에서 사용되는 컴포넌트를 지정
- 옵셔널 값이지만, addon에 사용되기 때문에 적어주는 것을 권장

### 3. argTypes: { ... }

- 컴포넌트의 인자(Props)를 직접 조작할 수 있도록 설정할 수 있음
- args를 다르게 부여하여 여러개의 story를 재사용 할 수 있음
- 속성
  Boolean, Text, Number, Color, Object, Select, Radio, InlineRadio, Check, InlineCheck, Range, Date, File

### 4. Decorator

- 기능적으로 추가적인 렌더링을 통해 감쌀 수 있는 방법
- 일반적으로 2가지의 경우에 사용됨

1. 추가적으로 컴포넌트를 새로운 마크업으로 감싸기 위함

   ```jsx
   import { Meta } from '@storybook/react';

   export default {
     component: YourComponent,
     decorators: [
       (Story) => (
         <div style={{ margin: '3em' }}>
           <Story/>
         </div>
       ),
     ],
   } as Meta;
   ```

2. Context Provider으로 감싸야 하는 경우

   ```jsx
   // .storybook/preview.js

   import React from 'react';

   import { ThemeProvider } from 'styled-components';

   export const decorators = [
     (Story) => (
       <ThemeProvider theme="default">
         <Story />
       </ThemeProvider>
     ),
   ];
   ```

<br/>

## 배포

### 1. 정적 배포

```
$ npm run build-storybook
```

### 2. Chromatic 설치

storybook 관리자가 만든 무료 배포 서비스

```
$ npm i chromatic
```

### 3. 깃허브 저장소와 동기화

### 4. project-token

```
$ npm chromatic --project-token=<project-token>
```
