# redirect_to時にパラメータを送る

参照：
[stackoverflow](https://stackoverflow.com/questions/1430247/passing-parameters-in-rails-redirect-to) / 
[Ruby on Rails API](https://api.rubyonrails.org/classes/ActionController/Redirecting.html#method-i-redirect_to)

環境：
macOS(Catalina) / Ruby 2.6.5 / Rails 5.2.4

## 方法

```ruby
redirect_to action: "action_name", id: 3

# 例
redirect_to action: "new", blog_id: @blog.id

```

#### ポイント
- どうやら`action: "action_name"`が重要なよう。
- `new_blog_path`のようなprefixではエラーが出るようだ。
