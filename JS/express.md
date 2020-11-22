# expressについて

参照：
[公式ドキュメント](https://expressjs.com) / 
[GitHub](https://github.com/expressjs/express)

環境：
macOS(Catalina) / Node.js 14.15.0

---
## 1. expressとは
- Node.jsのフレームワークのひとつ

## 2. 仕様

### 1. インストール

(前提)Node.jsインストール、新規プロジェクトならば`npm init`
```
$ npm i express
```
※git管理する場合、`node_modules/`を`.gitignore`記述しておくべき

### 2. Hello World

///POINT///
  - `express()`でexpressの機能を利用できる
  - `get('/', コールバック関数)`でルートに対してGETメソッドを使って処理
  - `listen(ポート番号, コールバック関数)`で指定ポート番号でWebサーバ起動

```JavaScript
// app.js

const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => {
  res.send('Hello World')
});

app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`)
});
```

### 3. `express.Router()`を使ったルーティング

///POINT///
  - 複雑なルーティングの場合は`app.get()`のような方法よりも効果的。
  - 別ファイルにルーティング処理を記述
  - 読み込むファイルに`router`としてrequire
  - `use(パス, router)`で読み込み

```JavaScript
// router/index.js

const express = require('express');
const router = express.Router();

router.get('/', (req, res) => {
  res.send('root page');
});

module.exports = router;
```

```JavaScript
// app.js

const express = require('express');
const router = require('./router/index')

const app = express();
const port = 3000;

app.use('/', router);

app.listen(port, () => {
  console.log(`Example app listening at http://localhost:${port}`)
});
```