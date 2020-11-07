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

## 基本的なデータ送受信

```JavaScript
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
```