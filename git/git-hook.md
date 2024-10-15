## Git Hook 이란?

Git에서 특정 이벤트가 발생했을 때 자동으로 특정 스크립트를 실행할 수 있도록 하는 기능

<table>
  <thead>
    <tr>
      <td>분류</td>
      <td>훅</td>
      <td>설명</td>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td rowspan="4">커밋 워크플로 훅</td>
      <td>pre-commit</td>
      <td>commit 을 실행하기 전에 실행</td>
    </tr>
    <tr>
      <td>prepare-commit-msg</td>
      <td>commit 메시지를 생성하고 편집기를 실행하기 전에 실행</td>
    </tr>
    <tr>
      <td>commit-msg</td>
      <td>commit 메시지를 완성한 후 commit 을 최종 완료하기 전에 실행</td>
    </tr>
    <tr>
      <td>post-commit</td>
      <td>commit 을 완료한 후 실행</td>
    </tr>
    <tr>
      <td rowspan="4">기타 훅</td>
      <td>pre-rebase</td>
      <td>Rebase 하기 전에 실행</td>
    </tr>
    <tr>
      <td>post-rewrite</td>
      <td>git commit –amend, git rebase 와 같이 커밋을 변경하는 명령을 실행한 후 실행</td>
    </tr>
    <tr>
      <td>post-merge</td>
      <td>Merge 가 끝나고 나서 실행</td>
    </tr>
    <tr>
      <td>pre-push</td>
      <td>git push 명령 실행 시 동작하며 리모트 정보를 업데이트 하고 난 후 리모트로 데이터를 전송하기 전에 실행. push 를 중단시킬 수 있음</td>
    </tr>
  </tbody>
</table>

## Husky란?

Git Hook 제어를 보다 간편하게 지원하는 npm 모듈

`npm install` 과정에서 사전에 세팅해준 git hook을 모두 적용시킴

### ESLint + lint-staged + Husky 조합으로 lint 적용

```
npm install --save-dev husky

npx husky init
```

```
npm install lint-staged --save-dev
```

```json
// package.json
{
  "scripts": {
    "postinstall": "husky install",
    "lint": "eslint src --ext ts,tsx --report-unused-disable-directives --cache",
    "lint-staged": "lint-staged"
  },
  "lint-staged": {
    "**/*.{tsx,ts,jsx,js}": ["prettier --cache --write"]
  }
}
```

```
npx husky add .husky/pre-commit "npm lint-staged"
npx husky add .husky/pre-push "npm run lint"
```
