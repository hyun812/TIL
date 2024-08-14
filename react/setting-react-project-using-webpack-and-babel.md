💡 **[웹팩](https://webpack.js.org/)은 여러개 파일을 하나의 파일로 합쳐주는 번들러(bundler)
하나의 시작점(entry point)으로부터 의존적인 모듈을 전부 찾아내서 하나의 결과물을 만들어 낸다.**

## 사용 이유

1. 여러 개의 파일을 하나로 번들링하기 때문에 `HTTP 요청 횟수를 줄일 수 있다` => `로딩 속도 향상`

2. IIFE (즉시 실행 함수) 를 통해 스코프 문제를 해결하여 스코프 충돌에 대한 걱정 없이 스크립트파일을 연결 및 결합하여 `안전한 번들링`

3. 코드 스플리팅을 이용하여 필요한 모듈만 로드해 요청 지연을 줄일 수 있음

4. 모듈화된 코드를 사용하여 개발 및 유지보수가 쉽다

## webpack.config.js

### 속성

1. **mode**
   - `development` | `production` | `none`
   - 별도로 지정하지 않으면 default ‘production’
2. **entry**
   - 어플리케이션의 진입점
   - 어떤 모듈로부터 시작해 디펜던시 그래프를 그려나갈지 명시 (여러 개 지정 가능)
3. **output**
   - 웹팩이 번들링 한 후 결과물을 어디로 내보낼지 지정
   - filename, path 지정 가능
   - clean을 true로 설정하면 지정한 결과물이 dist안에서 사용하지 않는 파일을 알아서 정리해줌
4. **loader**
   - 웹팩은 기본적으로 js와 json 파일만을 이해할 수 있기 때문에 loader를 사용
   - ‘test’ , ‘use’ 필수 속성
     - text : 어떤 파일을 변환할지 식별 ( 정규표현식 사용 )
     - use: 파일 변환 시 어떤 로더를 사용해야하는지 명시
5. [**plugins**](https://webpack.js.org/plugins/)
   - 로더는 특정 유형의 모듈을 변환 but, 플러그인은 번들 최적화, 자산 관리, 환경 변수 주입 등 더 광범위한 작업을 수행하는데 활용
   - `html-webpack-plugin`
     애플리케이션에 대한 HTML 파일을 생성하고 생성된 모든 번들을 자동으로 이 파일에 삽입
6. [DevServer](https://webpack.kr/configuration/dev-server/)

## 세팅

**package.json 생성**

```jsx
npm init -y
```

</br>

**React 개발 환경 설치**

```jsx
npm install react react-dom
```

</br>

**webpack 설치**

```jsx
npm install -D webpack webpack-cli webpack-dev-server
```

</br>

**babel 설치**

```jsx
npm i -D @babel/core @babel/cli @babel/preset-env @babel/preset-react
```

- `@babel/core` : 바벨을 사용하기 위해 필수 설치
- `@babel/cli` : 바벨을 cli에서 사용하기 위해 설치
- `@babel/preset-env` : ES6를 변환하기 위해 설치, 원래는 연도별로 babel-reset-es2015, babel-reset-es2016와 같이 제공했지만 바벨 7 이후부터 하나로 합쳐짐
- `@babel/preset-react` : react 코드를 변환하기 위해 설치

```jsx
// .babelrc
{
  "presets": ["@babel/env", "@babel/react"]
}
```

</br>

**loader, plugins 설치**

```jsx
npm i -D css-loader style-loader file-loader babel-loader html-webpack-plugin
```

- `css-loader` : js에서 css 파일 import 하기 위한 로더
- `style-loader` : 실제 DOM 요소에 css 적용하기 위한 로더
- `file-loader` : 파일을 import/require()로 사용하기 위해 설치, 예를 들어 이미지를 import해서 img 태그의 src에 넣을 수 있음
- `babel-loader` : 웹팩에서 바벨을 로더를 사용하기 위해 설치
- `html-webpack-plugin` : 웹팩 번들을 제공하는 HTML 파일 생성을 단순화

</br>

**webpack 설정 파일 작성**

```jsx
// webpack.config.js

const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
  name: 'React-webpack-setting',
  mode: 'development',
  resolve: {
    extensions: ['.js', '.jsx'],
  },
  entry: './src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'app.js',
    clean: true,
  },
  module: {
    rules: [
      {
        test: /\.?js$/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env', '@babel/preset-react'],
          },
        },
      },
      {
        test: /\.css$/i,
        use: ['style-loader', 'css-loader'],
      },
      {
        test: /\.(png|jpe?g|gif)$/i,
        use: [
          {
            loader: 'file-loader',
          },
        ],
      },
    ],
  },
  plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html',
    }),
  ],
  devServer: {
    host: 'localhost',
    port: 3000,
    open: true,
    compress: true,
    liveReload: true,
  },
};
```

</br>

**파일 작성**

```jsx
// index.js
// react 구성 요소를 렌더링 하는 진입점 파일
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';

ReactDOM.render(<App />, document.getElementById('root'));
```

```jsx
// index.html

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
```

</br>

**npm script 작성**

```jsx
// package.json
{
	...
	"scripts": {
    "dev": "webpack-dev-server",
    "build": "webpack --mode production"
  },
  ...
}
```
