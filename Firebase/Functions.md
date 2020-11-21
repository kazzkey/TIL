# Cloud Functionsについて

参照：
[公式ドキュメント](https://firebase.google.com/docs/functions?hl=ja)

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

1. `functions/index.js`
```JavaScript
// functions/index.js

const functions = require('firebase-functions');

exports.helloWorld = functions.https.onRequest((request, response) => {
  functions.logger.info("Hello logs!", {structuredData: true});
  response.send("Hello from Firebase!");
});
```

2. 実行

開発環境
```
$ npm run serve
```

本番環境
```
$ npm run deploy
```