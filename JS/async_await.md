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

---

## 4. 実例

- 例として[jsonplaceholderのposts](https://jsonplaceholder.typicode.com/posts)のAPIを叩いてみる
- 基本的にアロー関数型で書いてみる

1. Promiseパターン

```JavaScript
const callApi = () => {
  // fetchでデータを取得する
  // 取得データをresとしてjson型にする
  // jsonデータをpostsに格納する
  fetch("https://jsonplaceholder.typicode.com/posts")
    .then((res) => {
      return res.json();
    })
    .then((posts) => {
      // コンソールにデータがjson型で表示される
      console.log(posts);
    });
}
```

2. async/awaitパターン

```JavaScript
const callApi = async () => {
  // resにfetchで取得したデータを代入
  const res = await fetch("https://jsonplaceholder.typicode.com/posts");
  // json型にしてpostsに代入
  const posts = await res.json();
  // コンソールにデータがjson型で表示される
  console.log(posts);
}
```

### 【比較】
- async/awaitパターンのほうが、記述量も少なく可読性も高い。

### 【ちなみに】
- さらに古い書き方がこちら。最近ではあまり使われない。

```JavaScript
const callApi = () => {
  const xhr = new XMLHttpRequest();
  xhr.open("GET", "https://jsonplaceholder.typicode.com/posts");
  xhr.responseType = "json";
  xhr.send();
  xhr.onload = () => {
    console.log(xhr.response)
  };
}
```