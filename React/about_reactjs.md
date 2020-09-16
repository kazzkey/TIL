# React.jsについて

参照：
掌田津耶乃『React.js Next.js 超入門』(秀和システム)

環境：
macOS(Catalina) / React 16.13.1

---
## 1.React.jsとは
- フロントエンド・フレームワークのひとつ。Facebookが開発。
---
## 2.特徴
- リアクティブプログラミング
元の値を変更すると、表示も自動更新される。
- 仮想DOM
仮想DOMを操作することで高速になる。
- 豊富な拡張機能
コンポーネントや拡張プログラムを組み込んで使うことができる。

---

## 3.動作の仕組み

1. React組み込みタグを指定
```html
<div id="root">hoge</div>
```

2. 組み込み用タグの取得
```JavaScript
let dom = document.querySelector('#root');
```

3. エレメントを作成
```JavaScript
React.createElement(タグ名, 属性, 組み込まれるもの)


(例)
React.createElement(
  'p', {}, 'Hello React!!'
);
```

4. レンダリング実行
```JavaScript
ReactDOM.render(エレメント, DOM)
```
---
## 4.アプリケーション作成

#### コマンド(例)

```
# 作成
$ npx create-react-app プロジェクト名


# プロジェクト実行
$ yarn start


# プロジェクトをビルド
$ yarn build


#プロジェクトをテスト
$ yarn test
```
