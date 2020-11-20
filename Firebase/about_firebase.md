# Firebaseについて

参照：
[公式ドキュメント](https://firebase.google.com/docs?hl=ja) / 
[はじめてみようFirebase](https://www.topgate.co.jp/firebase01-what-is-firebase)

環境：
macOS(Catalina)

---
## 1. Firebaseとは
- Googleが提供しているBaas(Backend as a Service)

---
## 2. 主な機能
#### Hosting
- 静的ファイルをWebページとして公開できる

#### [Cloud Firestore](./Firestore.md)
- NoSQLのDB
- 他にRealtime Databaseもあるが、Googleはこちらを推奨している

#### Cloud Strage
- 写真や動画などバイナリーデータを保存できる
- AWSでいうところのS3

#### Authentication
- 認証機能を簡単に実装できる
- Google認証だけでなくTwitterなどのサードパーティの認証も使用できる

#### [Cloud Functions](./Functions.md)
- Firebaseでバックエンドのプログラムを実行する機能
- Web APIの実装や定期実行などができる
- APIサーバ経由でのメリットがある
  - Webアプリ・ネイティブアプリ共通の処理を一元管理できる
  - セキュリティ面の大事な情報をバックエンドに保持できる
  - バックアップを取ることができる
---