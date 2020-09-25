# gem rooでエクセルファイルをDBに保存する

参照：
[Gem](https://github.com/roo-rb/roo) /
[Rails gem rooを使って、エクセルファイルからデータ保存](https://qiita.com/fpckt/items/4220bde5b3b1d1bb6f9f)

環境：
macOS(Catalina) / Ruby 2.6.5 / Rails 5.2.4

---
## 1. 準備

#### 【Gem インストール】
```ruby
# Gemfile

gem 'roo'
```
その後`bundle install`

#### 【rooをrequire】

```ruby
# config/application.rb

require 'roo'  # 追加
```

---
## 2. 設定

#### 【router】

- (例)userの場合
```ruby
#config/routes.rb

resources :users do
    post :import, on: :collection
  end
```

#### 【model】


- クラスメソッドを定義
```ruby
# app/models/user.rb

class User < ApplicationRecord

  validates :grade_class, presence: true, format: { with: /\d[A-Z]/ }
  validates :number, presence: true, numericality: { greater_than: 0 }
  validates :name, presence: true, length: { maximum: 30 }

  def self.import(file)
    xlsx = Roo::Excelx.new(file.tempfile)
    xlsx.each_row_streaming(offset: 1) do |row|
      user = self.new(number: row[0].value, name: row[1].value)
      user.grade_class = xlsx.a1
      next if self.pluck(:id).include?(user.id)
      unless user.save
        flash.now[:alert] = "ユーザの入力に失敗しました"
        render: :index
      end
    end
  end
end
```

#### 【controller】

- importメソッドを作成
```ruby
# app/controllers/users_controller.rb

def import
  User.import(params[:file])
  redirect_to users_url
end
```

#### 【view】

- フォームヘルパー
```ruby
# app/views/users/index.html.erb

<%= form_with url: import_users_path, local: true do |form| %>
  <%= form.file_field :file %>
  <%= form.submit %>
<% end %>
```