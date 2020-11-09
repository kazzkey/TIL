# Cloud Firestoreについて

参照：
[公式ドキュメント](https://firebase.google.com/docs/firestore?hl=ja)

環境：
macOS(Catalina) / [Firebase CLI 8.15.1](https://firebase.google.cn/docs/cli?hl=ja)

前提：
- Firebaseプロジェクト作成 → [Cloud Firestore設定](https://firebase.google.com/docs/firestore/quickstart?hl=ja)
- ローカルのディレクトリ作成
- [Firebase CLIインストール → ログイン → Firestore設定](https://firebase.google.cn/docs/cli?hl=ja#install-cli-mac-linux)

---

## 基本概念

### 【用語】

#### ドキュメント
- オブジェクト型(key-value)でデータを格納する
- 各データには型を指定できる
- ドキュメント内にコレクションを持つこともできる(＝サブコレクション)

#### コレクション
- 複数のドキュメントを格納する

#### サブコレクション
- ドキュメント内に保持するコレクション

---

## 基本的なデータ受信

1. 1件のドキュメントを取得
```JavaScript
// データを取得するボタンを設定したとして…

// <async/awaitパターン>
const handleClickFetchButton = async () => {
  const db = firebase.firestore();
  const doc = await db.collection('users').doc('alovelace').get();
  console.log('Doc Data:' doc.data());
  });
};

// <Promiseパターン>
const handleClickFetchButton = () => {
  const db = firebase.firestore();
  db.collection('users').doc('alovelace').get().then((doc) => {
    console.log('Doc Data:' doc.data());
  });
};
```

2. コレクションから複数ドキュメントを取得
```JavaScript
// データを取得するボタンを設定したとして…

// <async/awaitパターン>
const handleClickFetchButton = async () => {
  const db = firebase.firestore();
  const snapshot = await db.collection('users').get();
  snapshot.forEach((doc) => {
    console.log(doc.id, '=>', doc.data());
  });
};

// <Promiseパターン>
const handleClickFetchButton = () => {
  const db = firebase.firestore();
  db.collection('users').get().then((snapshot) => {
    snapshot.forEach((doc) => {
      console.log(doc.id, '=>', doc.data());
    });
  });
};
```



<!-- ```JavaScript
document.addEventListener('DOMContentLoaded', () => {
  // wite
  var db = firebase.firestore();
  document.getElementById("submit-btn").onclick = () => {
    db.collection("datas").doc("user").set(
      { "name": document.getElementById("user-name").value,
        "email": document.getElementById("user-email").value
      }).then(() => {
        console.log("Document successfully written!");
      }).catch((error) => {
        console.error("Error writing document: ", error);
      });
  };
  // read
  db.collection("datas").doc("user").get().then((doc) => {
    document.getElementById("user-name").value=doc.data().name
    document.getElementById("user-email").value=doc.data().email
  });
});
``` -->