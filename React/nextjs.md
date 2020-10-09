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

または

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
1. pagesディレクトリの作成
2. ディレクトリ内にJSファイル作成(この階層がURLになる)
3. index.jsはホーム(/)となる

 - 作成ファイル内でComponentを作成
```JavaScript
export default function ComponentName() {
  return <h1>hoge</h1>
}
```

### 【リンクの作成】

1. Linkをインポート
2. <Link>タグ内に<a>タグを作成
3. classNameなどは<a>タグに記述する

```JavaScript
import Link from 'next/link'

export default function ComponentName() {

  // Linkタグ内hrefでパスを指定(pages以下を表記)
  return (
    <Link href="/foo/bar">
      <a>this is link to "/foo/bar" </a>
    </Link>
  )
}
```