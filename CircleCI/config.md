# Circle CI 設定

参照：
[CircleCI Documentation](https://circleci.com/docs/)

環境：
macOS(Catalina) / Ruby 2.6.5 / Rails 5.2.4 / PostgreSQL

## 1.準備
#### config.yml作成

2.1の場合の作成例
```ruby
version: 2.1

orbs:
  ruby: circleci/ruby@1.1.0

jobs:
  build:
    docker:
      - image: circleci/ruby:2.6.5-browsers
        environment:
          BUNDLER_VERSION: 2.1.4
          TZ: "Asia/Tokyo"
    steps:
      - checkout
      - ruby/install-deps

  test:
    parallelism: 3
    docker:
      - image: circleci/ruby:2.6.5-browsers
        environment:
          DB_HOST: 127.0.0.1
          RAILS_ENV: test
          BUNDLER_VERSION: 2.1.4
          TZ: "Asia/Tokyo"
      - image: circleci/postgres
        environment:
          POSTGRES_USER: postgres
          POSTGRES_DB: app_test
          POSTGRES_PASSWORD: password
    steps:
      - checkout
      - ruby/install-deps
      - run: mv config/database.ci.yml config/database.yml
      - run:
          name: Wait for DB
          command: dockerize -wait tcp://localhost:5432 -timeout 1m
      - run: bundle exec rake db:create
      - run: bundle exec rake db:schema:load
      - run: bundle exec rspec

workflows:
  version: 2
  build_and_test:
    jobs:
      - build
      - test:
          requires:
            - build
```

#### databese.ci.yml作成

 自動テスト用の設定。`run: mv config/database.ci.yml config/database.yml`で置き換わる。
```ruby
default: &default
  adapter: postgresql
  encoding: unicode
  # For details on connection pooling, see Rails configuration guide
  # http://guides.rubyonrails.org/configuring.html#database-pooling
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>

test:
  <<: *default
  host: 127.0.0.1
  username: postgres
  password: password
  database: app_test
```