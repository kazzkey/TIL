# JSX構文例

参照：
掌田津耶乃『React.js Next.js 超入門』(秀和システム)

環境：
macOS(Catalina) / React 16.13.1

---
## 1.条件分岐

```JSX
// 真偽
{ 真偽値 && --JSXの記述--- }


(例)
let hoge = true;

let el = (
  <div>
  { hoge &&
    <p>fuga</p>
  }
  </div>
)
```

```JSX
// 三項演算子
{ 真偽値 ? --true時のJSX-- : --false時のJSX--}


(例)
let hoge = true;

let el = (
  <div>
  { hoge ?
    <p>fuga</p>
  :
    <p>piyo</p>
  }
  </div>
)
```

---
## 2.繰り返し

```JSX
// mapを使った繰り返し
{ 配列.map( (value) => ( 新しい項目 ) ) }


(例)
{ data.map((value) =>(
  <p>{ value.hoge }</p>
))}
```
