# RSpec等テスト関係一括導入

環境：
macOS(Catalina) / Ruby 2.6.5 / Rails 5.2.4 / RSpec 3.9

## 1.準備
#### 不要なファイルを作成しないよう設定
```ruby
# config/application.rb

config.generators do |g|
  g.test_framework :rspec,
                   model_specs: true,
                   view_specs: false,
                   helper_specs: false,
                   routing_specs: false,
                   controller_specs: false,
                   request_specs: false
end
```
(例)モデルスペック、システムスペックのみ行う場合

#### Gemインストール
```ruby
# Gemfile

group :development, :test do
  gem 'rspec-rails'
  gem 'spring-commands-rspec'
  gem 'factory_bot_rails'
  gem 'faker'
  gem 'launchy'
end

group :test do
  gem 'capybara'
  gem 'webdrivers'
end
```
- `spring-commands-rspec`: `bin/rspec`コマンドで実行するためのGem。
- `factory_bot_rails`: テストデータの関連付けができる。
- `faker`: 名前をランダムで返すGem。日本語名なら`gimei`がオススメ。
- `launchy`: Capybaraテスト中に現在ページを確認できるようにしてくれる。
- `capybara`: アプリケーション操作をしてくれる。
- `webdrivers`: ブラウザでの自動テストをサポート。
※`gem 'selenium-webdriver'` `gem 'chromedriver-helper'`があったら削除。


## 2.設定
```
$ bundle install
$ bundle exec spring binstub rspec
$ rails generate rspec:install
$ echo --format documentation >> .rspec
```
