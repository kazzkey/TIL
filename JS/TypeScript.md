# TypeScriptについて

参照：
[公式ドキュメント](https://www.typescriptlang.org/docs) / 
[TypeScriptの概要(Qiita)](https://qiita.com/EBIHARA_kenji/items/4de2a1ee6e2a541246f6) / 
[TypeScript Deep Dive 日本語版](https://typescript-jp.gitbook.io/deep-dive/)

環境：
macOS(Catalina) / Node.js 12.19.0 / npm 6.14.8 / tsc 4.0.3

---
## 1. TypeScriptとは
- AltJS(JSのかわりとなるもの)のひとつ。Microsoftが開発。
- JSに変換するコンパイラとしても使える。

---
## 2. 特徴
- JSのスーパーセット(上位互換)である。
- 「型定義」が使えるなど、従来のJSにできなかったことができる。
- ファイルの拡張子は`.ts`となる。

---

## 3. 準備

- Node.jsがインストールされていることが前提
```
$ npm install -g typescript
```


---
## 4. 型定義

(例)
```TypeScript
// Number
let decimal: number = 6;

// String
let color: string = "blue";

// Array
let list: number[] = [1, 2, 3];
// or
let list: Array<number> = [1, 2, 3];
```