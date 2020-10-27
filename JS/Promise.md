# Promiseについて

参照：
[【JavaScript】初心者にもわかるPromiseの使い方](https://techplay.jp/column/581) / 
[MDN web doc(Promiseを使う)](https://developer.mozilla.org/ja/docs/Web/JavaScript/Guide/Using_promises) / 
[JavaScript Promiseの本](https://azu.github.io/promises-book/)

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

### 【基本的な書き方】
```JavaScript
new Promise(function(resolve, reject) {
  resolve('成功');
});

new Promise(function(resolve, reject) {
  reject('失敗');
});
```

(例)
- この場合、`console.log("Promise成功")`は非同期処理され、"先に出力よりあとに出力される。"
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

### 【Promiseの連結(チェイン)】
- `then()`をつなげていくことで、連結させることができる。チェインとも呼ぶ。

### 【複数の非同期処理の実行】
- `all()`を使うことで、複数の非同期処理の同時実行ができる。

```JavaScript
Promise.all(iterable).then(function(message) {
  // 処理
})
```

(例)
- この場合、allは全ての非同期処理がresolveされたタイミングで結果を返す。
- したがってこのPromise.allはPromise2の影響で1秒後に結果を返す。
```JavaScript
var promise1 = new Promise(function(resolve, reject) {
  setTimeout(function() {
    resolve();
  }, 300);
});

var promise2 = new Promise(function(resolve, reject) {
  setTimeout(function() {
    resolve();
  }, 1000);
});

var promise3 = new Promise(function(resolve, reject) {
  setTimeout(function() {
    resolve();
  }, 500);
});

Promise.all([promise1, promise2, promise3]).then(function() {
  console.log("Fourth");
})

console.log("First");

setTimeout(function() {
  console.log("Third");
}, 600);

console.log("Second");
```

### 【catchを使ったエラーハンドリング】
- `catch()`を使うことで、チェインを実行している最中にエラーが発生してもエラーを捕まえることができる。

(例)
- この場合、ふたつめのチェインに入った段階でエラーを発生させている。
- そのため、3を加算した結果である「6」を返す前にエラーメッセージを表示させる。
```JavaScript
function getNum(num) {
  return new Promise(function(resolve, reject) {
    if (num >= 3) {
      setTimeout(function() {
        resolve(num);
      }, 500);
    } else {
      reject("Failed");
    }
  });
}

gretNum(3).then(function(result) {
  console.log(result);
  return result + 3;
}).then(function(result) {
  // ここでエラーを発生させる
  throw new Error('エラー！失敗しました');
  console.log(result);
  return result + 3;
}).then(function(result) {
  console.log(result);
  // catchを使うことで、エラーが発生した時点でエラーメッセージを返す
}).catch(function(e) {
  console.log('error:', e)
})
```
