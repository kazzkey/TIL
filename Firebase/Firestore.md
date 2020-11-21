# Cloud Firestoreについて

参照：
[公式ドキュメント](https://firebase.google.com/docs/firestore?hl=ja)

環境：
macOS(Catalina) / [Firebase CLI 8.15.1](https://firebase.google.cn/docs/cli?hl=ja)

前提：
- Firebaseコンソール
  - プロジェクト作成
  - [Cloud Firestore設定](https://firebase.google.com/docs/firestore/quickstart?hl=ja)
- ローカル
  - ディレクトリ作成
  - [Firebase CLIインストール → firebase init → Firestore設定](https://firebase.google.cn/docs/cli?hl=ja#install-cli-mac-linux)

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

- POINT
  - `firebase.firestore()`でFirestoreのDBにアクセス
  - `collection('hoge').doc('fuga')`でドキュメントを指定
  - `get()`で取得
  - `data()`でデータ内容を表示

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
// 取得したデータをsnapshot変数に格納しforEach()で全件表示する

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

3. 絞り込んで取得
```JavaScript
// where() や limit() などを使ってSQLのように絞り込める
// 例： 年齢20歳以下のユーザを1件取得

// <async/awaitパターン>
const handleClickFetchButton = async () => {
  const db = firebase.firestore();
  const snapshot = await db.collection('users')
  .where('age', '<=', 20) // where
  .limit(1) // limit
  .get();
  snapshot.forEach((doc) => {
    console.log(doc.id, '=>', doc.data());
  });
};

// <Promiseパターン>
const handleClickFetchButton = () => {
  const db = firebase.firestore();
  db.collection('users')
  .where('age', '<=', 20)
  .limit(1)
  .get()
  .then((snapshot) => {
    snapshot.forEach((doc) => {
      console.log(doc.id, '=>', doc.data());
    });
  });
};
```

## 基本的なデータ送信

- POINT
  - `set()`でドキュメントを作成、または上書き
  - `add()`で新たにドキュメントを追加

1. 1件のドキュメントを作成、または上書き
```JavaScript
// データを取得するボタンを設定したとして…
// この場合、データが存在しない場合は作成される
// データが既に存在する場合は、上書きされる

// <async/awaitパターン>
const handleClickAddButton = async () => {
  const db = firebase.firestore();
  await db
    .collection('users')
    .doc('alovelace')
    .set({
      name: 'Taro',
      age: 20
    })
  });
};
```

2. ドキュメントを新たに追加
```JavaScript
// データを取得するボタンを設定したとして…
// add()の場合、ドキュメントIDを指定しなければ、自動生成される

// <async/awaitパターン>
const handleClickAddButton = async () => {
  const db = firebase.firestore();
  await db
    .collection('users')
    .add({
      name: 'Taro',
      age: 20
    })
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