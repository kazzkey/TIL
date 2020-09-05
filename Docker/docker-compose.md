# docker-composeによるRails環境構築

参照：
- [公式クイックスタート](https://docs.docker.com/compose/rails)
- [用語集](https://docs.docker.jp/glossary.html)
- [ベストプラクティス集](https://docs.docker.jp/engine/articles/dockerfile_best-practice.html)

環境：
Ruby 2.6.5 / Rails 5.2.4 / PostgreSQL / Docker for Macでの構築

<br>
## 1.準備
### Dockerfile作成

```
FROM ruby:2.6.5
RUN apt-get update -qq && apt-get install -y nodejs postgresql-client
RUN mkdir /myapp
WORKDIR /myapp
COPY Gemfile /myapp/Gemfile
COPY Gemfile.lock /myapp/Gemfile.lock
RUN bundle install
COPY . /myapp

# Add a script to be executed every time the container starts.
COPY entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]
EXPOSE 3000

# Start the main process.
CMD ["rails", "server", "-b", "0.0.0.0"]
```
【参考】ENTRYPOINT CMDについて
https://qiita.com/uehaj/items/e6dd013e28593c26372d


### Gemfile作成

```
source 'https://rubygems.org'
gem 'rails', '5.2.4'
```

### Gemfile.lock作成

- 中身は空でok

### entrypoint.sh作成

```
#!/bin/bash
set -e

# Remove a potentially pre-existing server.pid for Rails.
rm -f /myapp/tmp/pids/server.pid

# Then exec the container's main process (what's set as CMD in the Dockerfile).
exec "$@"
```

### docker-compose.yml作成

- db, webは好きに名付けてok
```
version: '3'
services:
  db:
    image: postgres
    volumes:
      - ./tmp/db:/var/lib/postgresql/data
    environment:
      POSTGRES_PASSWORD: password
  web:
    build: .
    command: bash -c "rm -f tmp/pids/server.pid && bundle exec rails s -p 3000 -b '0.0.0.0'"
    volumes:
      - .:/myapp
    ports:
      - "3000:3000"
    depends_on:
      - db
```

<br>
## 2.プロジェクトのビルド
### rails new

```
$ docker-compose run web rails new . --force --no-deps --database=postgresql
```

### bundle install

```
$ docker-compose build
```

<br>
## 3.DB設定
### config/database.ymlの修正

- host, username, passwordを追加
```
default: &default
  adapter: postgresql
  encoding: unicode
  host: db
  username: postgres
  password: password
  pool: 5

development:
  <<: *default
  database: myapp_development


test:
  <<: *default
  database: myapp_test
```
<br>
## 4.アプリケーションの起動
### コンテナ起動

```
$ docker-compose up
```
`-d`オプションをつけるとバックグラウンドで動作する

### DB作成
```
$ docker-compose run web rails db:create
```

<br>
## 5.アプリケーションの停止
### バックグラウンド起動の場合

```
$ docker-compose down
```
フォアグラウンドでの起動の場合`Ctl + C`で停止できる

<br>
## 6.開発
### docker-compose run をつけてrailsコマンドを実行

```
(例)
$ docker-compose run web rails g controller home index
```
