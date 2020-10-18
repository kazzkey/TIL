# git command 備忘録

参照：
[GitHub ヘルプドキュメント](https://docs.github.com/ja/github)

環境：
macOS(Catalina)

## GitHub関連
#### 【プルリクエストをローカルでチェックアウト】

プルリクエストのIDを確認。
```
$ git fetch origin pull/ID/head:BRANCHNAME
```
```
$ git checkout BRANCHNAME
```

#### 【リモートブランチをローカルでチェックアウト】

リモートリポジトリをローカルへ。
```
$ git fetch
```

```
$ git checkout -b BRANCHNAME origin/BRANCHNAME
```

#### 【ローカルのブランチをリモートへプッシュ】
```
$ git push -u origin BRANCHNAME
```

## ローカル関連
#### 【変更内容をターミナル上で確認する】

1. ローカルの変更内容を確認
```
$ git diff
```

2. ログの変更内容を確認
```
$ git log -p
```

#### 【ソースコードを検索する】

```
$ git grep "検索したいワード"
```

#### 【コミットを取り消す(git reset系)】

1. 直前のコミットに戻す
```
# 変更分を全てなかったことにする
$ git reset --hard HEAD^

# コミットのみ取り消すが、変更分は残す
$ git reset --soft HEAD^
```