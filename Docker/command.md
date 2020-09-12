# docker command 備忘録

参照：
[Compose コマンドライン・リファレンス](http://docs.docker.jp/compose/reference/index.html)

環境：
macOS(Catalina) / Docker for Mac

## docker-compose関連
#### コンテナ一覧

起動中コンテナ
```
$ docker-compose ps
```

すべてのコンテナ
```
$ docker-compose ps -a
```

#### イメージ一覧

```
$ docker-compose images
```

#### noneのイメージ削除

すでに存在するイメージと同一名のDockerイメージを作成しようとした場合に、古いものが<none>に置き換わる。このようなイメージは基本的に不要。
```
$ docker image prune
```
