# Action Textを用いたCRUD機能作成

参照：
[Railsガイド](https://railsguides.jp/action_text_overview.html)

環境：
Ruby 2.6.5 / Rails 6.0.3 / PostgreSQL 12.3

## 1.準備
#### まずはおなじみ
```
$ rails _6.0.3_ new アプリ名 -d postgresql

$ rails db:create
```

#### Action Textをインストール
```
$ rails action_text:install
```
Yarnパッケージが追加され、必要なマイグレーションがコピーされる。

```
$ rails db:migrate
```

#### Active Strageに関するGemの設定

```ruby
# Use Active Storage variant
gem 'image_processing', '~> 1.2'
```
コメントアウトする。そして`bundle install`


## 2.CRUD作成
#### 例：scaffoldでblog作成
```
$ rails g scaffold blog title:string
```
ちなみにカラムに`content`は入れなくてok。

```
$ rails db:migrate
```

#### リッチテキスト設定を追加
```ruby
# app/models/blog.rb

class Blog < ApplicationRecord
  has_rich_text :content  # 追加
end
```

```ruby
# app/views/blogs/_form.html.erb

<%= form_with(model: blog) do |form| %>

  <div class="field">                   # ここから追加
    <%= form.label :content %>
    <%= form.rich_text_area :content %>
  </div>
<% end %>
```

```ruby
# app/views/blogs/show.html.erb

<%= @message.content %>   # 追加
```

```ruby
# app/controllers/blogs_controller.rb

private

  def blog_params
    params.require(:blog).permit(:title, :content) # 追加
  end
```
