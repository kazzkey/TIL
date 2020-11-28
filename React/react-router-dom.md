# react-router-domについて

参照：
[公式ドキュメント](https://reactrouter.com/web/guides/) / 
[Reactハンズオン勉強会（SPA開発編）](https://npo-fitness-engineer.connpass.com/event/194639/) / 
[Qiita: React Router v4 からの主な移行・変更点一覧](https://qiita.com/TsutomuNakamura/items/b202bc7ebb2693937c13)

環境：
macOS(Catalina) / React

前提：
- `npx create-react-app`などでアプリケーションを作成
<br>
---
## 1. react-router-domとは

- ルーティングをかんたんに設定できるReactのライブラリ
  - (参考) [Qiita: react-routerとreact-router-domの違い](https://qiita.com/koja1234/items/486f7396ed9c2568b235)

<br>
## 2. インストール

```sh
# ディレクトリ下で

$ npm i react-router-dom
```

<br>
## 3. 準備

- `src`ディレクトリ下に`routes.js`と`pages`ディレクトリを作成
- `pages`ディレクトリ下にコンポーネントを作成
  - Next.jsと同じ要領でこれが各ページになる

(例)
```JavaScript
// pages/Top.js

// Linkをインポートできる
import { Link } from 'react-router-dom';

const Top = () => {
  return (
    <div>
      <h1>This is Top page!!</h1>

      {/* Linkのpathの設定は`to="/hoge"`のように設定する */}
      <Link to="/about">About</Link>
    </div>
  );
};

export default Top;
```

```JavaScript
// pages/About.js

import { Link } from 'react-router-dom';

const About = () => {
  return (
    <div>
      <h1>This is About page!!</h1>

      <Link to="/">Top</Link>
    </div>
  );
};

export default About;
```

<br>
## 4. ルーティングの設定

### `routes.js`の設定

- ルートページには`exact: true`を指定
  - pathの部分一致を防ぐため
  - (参考) [Qiita: react-router-domのプロパティ"exact"とは？](https://qiita.com/ike_pon/items/bde0f8a0281ae432f332)

```JavaScript
// routes.js

// それぞれのページをインポート
import Top from './pages/Top';
import About from './pages/About';

// routes配列の中に連想配列でページを格納
const routes = [
  { path: '/', component: Top, exact: true },
  { path: '/about', component: About },
  {/* 他のページを設定していくときはここに追加していけばよい */}
];

export default routes;
```

### `App.js`の設定

- mapメソッドを使えば、App.jsにルーティングを直書きするよりDRY
- `Switch`はマッチする`Route`の最初のひとつだけをレンダリングしてくれる。なかった場合、一致するすぺてがレンダリングされてしまう。
  - (参考) [Switch](https://reactrouter.com/web/api/Switch)
- `withRouter()`でラップすると、コンポーネント間のRouterのアクセスができる
  - (参考) [withRouter](https://reactrouter.com/web/api/withRouter)

```JavaScript
// App.js

import React from "react";
import { Route, Switch, withRouter } from "react-router-dom";
import routes from "./routes";

const App = () => {
	return (
    <Switch>
      {routes.map((route, idx) => (
        <Route
          path={route.path}
          exact={route.exact}
          component={route.component}
          key={idx}
        />
      ))}
    </Switch>
	);
};

export default withRouter(App);
```

### `index.js`の設定

- `App`コンポーネントを`BrowserRouter`で囲む
  - (参考) [BrowserRouter](https://reactrouter.com/web/api/BrowserRouter)

```JavaScript
// index.js

import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter } from "react-router-dom";
import App from './App';

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>,
  document.getElementById('root')
);
```