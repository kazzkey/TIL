# async/awaitについて

参照：
[【JavaScript入門】5分で理解！async / awaitの使い方と非同期処理の書き方](https://www.sejuku.net/blog/69618)

環境：
macOS(Catalina)

---
## 1. async/awaitとは
- JavaScriptの非同期処理を扱うための仕組み。
- 従来のPromiseよりもわかりやすく記述できるメリットがある。

---
## 2. Promiseについて
- `then()`を使ってチェーンを繋いでいくため、単調になりやすい。

(例)
```JavaScript
getDate()
.then(function(data) {
 
  return getYear(data)
 
}).then(function(year) {
 
  return getSomething(year)
 
}).then(function(item) {
 
  getAnotherThing(item)
 
})
```
---

## 3. async/awaitの書き方

### 【基本的な構文】

```JavaScript
// function型
async funstion() {
  // 処理
}

// アロー関数型
const hoge = async () => {
  // 処理
}
```
```JavaScript
await Promise処理
```