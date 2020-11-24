# Cloud Functionsについて

参照：
[公式ドキュメント](https://firebase.google.com/docs/functions?hl=ja) / 
[前田剛氏のYouTube](https://www.youtube.com/watch?v=PmRUHEnsVQ8)

環境：
macOS(Catalina) / [Firebase CLI 8.16.2](https://firebase.google.cn/docs/cli?hl=ja)

前提：
- Firebaseコンソール
  - プロジェクト作成
  - [Cloud Functions設定](https://firebase.google.com/docs/functions/get-started?hl=ja)
- ローカル
  - ディレクトリ作成
  - [Firebase CLIインストール → firebase init → Functions設定](https://firebase.google.cn/docs/cli?hl=ja#install-cli-mac-linux)

---

## Hello World

### 1. `functions/index.js`
```JavaScript
// functions/index.js

const functions = require('firebase-functions');

exports.helloWorld = functions.https.onRequest((request, response) => {
  functions.logger.info("Hello logs!", {structuredData: true});
  response.send("Hello from Firebase!");
});
```

### 2. 実行

開発環境
```
$ npm run serve
```

本番環境
```
$ npm run deploy
```

## expressでAPI実装

### 1. express導入
```
$ npm i express
```

### 2. routeを設定
  - functionsディレクトリ下に`routers/messages`を作成
  - `route.js`などのファイルを作成

```JavaScript
// functions/messages/route.js

const express = require('express');

const router = express.Router();
const endPoint ='/messages';

// GET / POST
router
  .route(endPoint)
  .get((req, res) => {
    res.json({
      // 処理
    });
  })
  .post((req, res) => {
    res.json({
      // 処理
    });
  });

// PUT / DELETE
router
  .route(`${endPoint}/:id`)
  .put((req, res) => {
    res.json({
      // 処理 IDなどの取得は${req.params.id} 
    });
  })
  .delete((req, res) => {
    res.json({
      // 処理 IDなどの取得は${req.params.id} 
    });
  });

module.exports = router;
```

### 3. `index.js`でAPIを設定
```JavaScript
// functions/index.js

const functions = require('firebase-functions');
const express = require('express');
const messagesRouter = require('./routers/messages/route');

const app = express();
app.use('/', messagesRouter);

exports.api = functions.https.onRequest(app);
```