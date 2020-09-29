# レスポンシブデザインのためのCSS

参照：
[Progate](https://prog-8.com)
環境：
macOS(Catalina)

---
## 1. 設定

#### 【メディアクエリ】
- **responsive.css**など、別ファイルを作成して管理すると整理しやすい
```CSS
/* タブレットサイズ時のCSSを設定 */
@media (max-width: 1000px) {
  /* 適用したいCSSを記述 */
}

/* スマートフォンサイズ時のCSSを設定 */
@media (max-width: 670px) {
  /* 適用したいCSSを記述 */
}
```

#### 【レイアウト崩れの修正】

- 要素の幅(width)の合計に`padding`と`border`を含める設定
- `margin`はborder-boxの合計値には含まれない
- 基本的に全ての要素(*)に対して適用するのが望ましい
```CSS
/* HTML全体に適用させる */
* {
  box-sizing: border-box;
}
```

#### 【viewportの設定】

- レスポンシブデザインを適用するためには<head>タグ内に設定する必要がある

```HTML
<head>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
```

#### 【floatの解除】

- `float`の設定などがあるとレイアウトが崩れてしまうことがある
- 空タグを作って、floatを解除することで、レイアウトを整えることができる

```HTML
<!-- 空タグを追加 -->
<div class="clear"></div>
```
```CSS
/* floatを解除 */
.clear {
  clear: left;
}
```

---

## 2. Flexbox

- メディアクエリと合わせて使うことで画面幅に合わせた設定ができる

#### 【要素を横並びにする】

```CSS
/* 親要素のCSS */
.parent {
  display: flex;
}

/* 子要素のCSS */
.child {
  /* 親要素に合わせて伸縮させる */
  flex: auto;
}
```

#### 【要素を折り返す】

- 横並びと合わせて、要素の折返しを設定する

```CSS
.parent {
  display: flex;

  /* 折り返したい要素の親要素に指定する */
  flex-wrap: wrap;
}

.child {
  flex: auto;

  /* 子要素のサイズを親要素に対してどの割合にするか */
  width: 50%;
}
```

#### 【要素を縦並びにする】

```CSS
.parent {
  /* 縦並びにしたい要素の親要素に指定する */
  flex-direction: column;
}

.child {
  /* 中央寄せにする */
  margin: 0 auto;
}
```