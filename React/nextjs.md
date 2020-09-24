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