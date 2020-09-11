# git command 備忘録

参照：
[GitHub ヘルプドキュメント](https://docs.github.com/ja/github)

環境：
macOS(Catalina) / Ruby 2.6.5 / Rails 5.2.4

## GitHub関連
#### プルリクエストをローカルでチェックアウト

プルリクエストのIDを確認。
```
$ git fetch origin pull/ID/head:BRANCHNAME

```
```
$ git checkout BRANCHNAME

```

#### リモートブランチをローカルでチェックアウト

リモートリポジトリをローカルへ。
```
$ git fetch

```

```
$ git checkout -b BRANCHNAME origin/BRANCHNAME

```
