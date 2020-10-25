# Promiseについて

参照：
[【JavaScript】初心者にもわかるPromiseの使い方](https://techplay.jp/column/581)

環境：
macOS(Catalina)

---
## 1. Promiseとは
- JavaScriptの非同期処理を扱うための仕組み。

## 2. コールバックについて
- コールバックとは、ある関数へ別の関数を渡すこと。
- これを使うことで非同期処理ができるが、複雑になりがち。

## 3.Promiseの書き方
- Promiseはresolveとrejectのふたつの関数を引数にとる。
  * resoleve: 処理が成功したときのメッセージを表示する関数
  * reject: 処理が失敗したときのメッセージを表示する関数

```JavaScript
new Promise(function(resolve, reject) {
  resolve('成功');
});

new Promise(function(resolve, reject) {
  reject('失敗');
});
```

```JavaScript
var sample = new Promise(function(resolve, reject) {
  setTimeout(function() {
    resolve();
  }, 1000);
});

sample.then(function(value) {
  console.log("Promise成功");
});

console.log("先に出力");
```