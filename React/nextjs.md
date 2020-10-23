# Next.jsについて

参照：
掌田津耶乃『React.js Next.js 超入門』(秀和システム) / 
[公式ドキュメント](https://nextjs.org/docs)

環境：
macOS(Catalina) / React 16.13 / Next 9.5.3

---
## 1. Next.jsとは

- Reactをサーバーサイドでレンダリングし表示するプログラム。
- 生成されるページを「静的Webページ」として作成し、表示することもできる。
- 複数ページアプリとして作成することもできる。
---

## 2. 準備

#### 【一括セットアップ】

```
$ npx create-next-app

# or

$ yarn create next-app
```


#### 【マニュアルセットアップ】
1. プロジェクトの作成
```
$ mkdir app_name

$ cd app_name

$ touch package.json
```

2. package.jsonにscriptを追加
```json
{
  "scripts": {
    "dev": "next",
    "build": "next build",
    "start": "next start",
    "export": "next export"
  }
}
```

3. インストール
```
$ npm install next react react-dom

# or

$ yarn add next react react-dom
```

---

## 3. プロジェクトの実行

```
$ npm run dev
```
---

## 4. 作成

### 【ファイルの作成】
- Next.jsはルーティングの設定が用意されている。

#### `pages`ディレクトリ
- ディレクトリ下に作成したJSファイルの階層がURLになる
- index.jsを作成すると、ルート(/)となる
(例)
`pages/posts/first-post.js`を作った場合、URLは`/posts/first-post`となる

#### `public`ディレクトリ
- 画像等の静的ファイルを管理できる
- publicをルートとしたルートパスで記述すればOK
(例) public下に`vercel.svg`が配置されているとして
```JSX
<img src="/vercel.svg" />
```

#### 記述
(例) 作成ファイル内でComponentを作成
```JavaScript
export default function ComponentName() {
  return <h1>hoge</h1>
}
```

### 【リンクの作成】
- Next.jsではページ遷移のためのLinkコンポーネントが用意されている。
- JSによる遷移なので、高速かつURLを切り替えても再読み込み不要で、クライアントの状態が保持できる。

1. Linkをインポート
2. Linkタグ内にaタグを作成
3. classNameなどはaタグに記述する

```JavaScript
// Linkをインポート
import Link from 'next/link'

export default function ComponentName() {

  // Linkタグ内hrefでパスを指定(pages以下を表記)
  return (
    <div>
      <Link href="/foo/bar">
        <a className="link">this is link to "/foo/bar" </a>
      </Link>
    </div>
  )
}
```

### 【headの設定】
- Next.jsではheadタグを設定するためのHeadコンポーネントが用意されている。
- ページごとに設定できるのでSEO対策などに有効。

```JavaScript
// Headをインポート
import Head from 'next/head'

export default function ComponentName() {

  return (
    <div>
      <Head>
        <title>This is title!</title>
      </Head>
    </div>
  )
}
```

### 【CSSの設定】
- Next.jsではCSS Modules、Sass、styled-jsxを使うことができる

1. styled-jsxでのスタイリング

`<style jsx>{`…`}</style>`の中に記述する
```JavaScript
import Link from 'next/link'

export default function ComponentName() {
  return (
    <div>
      <Link href="/foo/bar">
        <a className="link">this is link to "/foo/bar" </a>
      </Link>

      {/* styled-jsxを設定 */}
      <style jsx>{`
        .link {
          font-size: 20px;
        }
      `}</style>
    </div>
  )
}
```

2. LayoutコンポーネントとCSS Modulesでのスタイリング

`components`ディレクトリをトップに作成し、その中に`layout.js`を作成
```JavaScript
// CSS Modulesをインポート
import styles from './layout.module.css'

// Layoutコンポーネントを作成し、JSX内にclassNameを指定
export default function Layout({ children }) {
  return <div className={styles.hoge}>{children}</div>
}
```

レイアウトしたいファイルにインポート
```JavaScript
import Link from 'next/link'
import Layout from '../../components/layout'

export default function ComponentName() {

  return (
    <Layout>
      <Link href="/foo/bar">
        <a>this is link to "/foo/bar" </a>
      </Link>
    </Layout>
  )
}
```

`components`下に`layout.module.css`を作成
```CSS
.hoge {
  margin: 1rem;
}
```
**※CSS Modulesでは自動でユニークなクラス名に変換してくれる**

3. 全ページで設定するグローバルスタイリング

`pages`下に`_app.js`を作成(ローカル開発時、作成後サーバのリスタートが必要)
このAppコンポーネントが、すべての異なるページに共通するトップレベルのコンポーネントとなる

```JavaScript
export default function App({ Component, pageProps }) {
  return <Component {...pageProps} />
}
```

Global CSSを設定(CSSファイルはどこに配置してもok)
CSSファイルを読み込むためには`_app.js`でのインポートが必要
```JavaScript
// (例) stylesフォルダ内のglobal.cssを読み込みたい場合
import '../styles/global.css'

export default function App({ Component, pageProps }) {
  return <Component {...pageProps} />
}
```

4. その他のスタイリング
- classnames: 適用するクラスを動的に変更できる
- PostCSS: 便利機能を持つプリプロセッサ
- Sass

---

## 5. プリレンダリング
- Next.jsはデフォルトで全ページをPre-renderingする
- ブラウザ側の負荷を下げて表示を高速化できるメリットがある

### 【２種類のプリレンダリング】
1. Static Generation
- ビルドした(next build)ときにHTMLが生成される
- 更新頻度の低いものに適している(ブログ、ECサイト、LP、問い合わせ等)

2. Server-side Rendering
- ユーザがリクエストを投げたときにHTMLが生成される
- 更新頻度の高いものに適している(SNS、チャット、動画配信)

### 【プリレンダリングの使い分け】
- Next.jsではページごとにプリレンダリングの方法を選択できる
- 基本的には Static Generation推奨

### 【Static Generationでのプリレンダリング】
- 外部データがある場合、ビルド時にDBや外部APIからデータを取得
- 取得したデータをもとにHTMLを生成

`getStaticProps`: `pages`ディレクトリ下でのみ使える