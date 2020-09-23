# react-reduxについて

参照：
掌田津耶乃『React.js Next.js 超入門』(秀和システム) / 
[公式](https://react-redux.js.org/)

環境：
macOS(Catalina) / React 16.13 / react-redux 7.2

---
## 1. react-reduxとは

- 値や処理をアプリ内で統合し管理するReactのライブラリ。
---

## 2. インストール

```
$ npm install react-redux

または

$ yarn add react-redux
```

---

## 3. Reduxのしくみ

- Store：データを保管し管理するもの。
- Provider：ストアを他のコンポーネントに受け渡すための仕組み。
- Reducer：ストアに保管されているステートを変更するための仕組み。

---

## 4. 構成

値管理の流れ
```
「ステート」用意 → 「レデューサー」用意 → 「ストア」用意 
```

index.js
```JavaScript
import React from 'react';
import ReactDOM from 'react-dom';

// redux関係のインポート
import { Provider } from 'react-redux';
import { createStore, combineReducers } from 'redux';
import App from './App';

// ステートの値を設定
let hoge = {
  // 定義
}

// レデューサー
function fuga(state = hoge, action) {
  // 処理
}

// ストアを作成
let store = createStore(fuga);

// レンダリング
ReactDOM.render(
  <Provider store={ store }>
    <App />
  </Provider>,
  document.getElementById('root')
);
```

App.js
```JavaScript
import React from 'react';

// redux関係のインポート
import { connect } from 'react-redux';

// ステートのマッピング
function mappingState(state) {
  return state;
}

class App extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return (
      // 表示内容
    );
  }
}
// ストアへのコネクト
App = connect()(App);


class Foo extends React.Component {
  render() {
    return (
      // 表示内容
    );
  }
}

// ストアへのコネクト　必要なステートがある場合は指定する
Foo = connect(mappingState)(Message);

export default App;
```