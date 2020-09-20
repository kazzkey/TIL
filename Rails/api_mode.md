# APIモードでrailsアプリケーション作成

参照：
[Railsガイド](https://railsguides.jp/api_app.html) /
[Web APIとは何なのか](https://qiita.com/NagaokaKenichi/items/df4c8455ab527aeacf02)

環境：
macOS(Catalina) / Ruby 2.6.5 / Rails 5.2.4 / PostgreSQL

## 1. 準備
#### おなじみのやつに`--api`オプションをつける
```
$ rails _5.2.4_ new アプリ名 -d postgresql --api

$ rails db:create
```

#### scaffoldでタスク機能を作成したとする
```
$ rails g scaffold task content:string

$ rails db:migrate
```

## 2. controllerの中身

#### JSONのレスポンスを返す。
```ruby
class TasksController < ApplicationController
  before_action :set_task, only: [:show, :update, :destroy]

  def index
    @tasks = Task.all

    render json: @tasks
  end

  def show
    render json: @task
  end

  def create
    @task = Task.new(task_params)

    if @task.save
      render json: @task, status: :created, location: @task
    else
      render json: @task.errors, status: :unprocessable_entity
    end
  end

  def update
    if @task.update(task_params)
      render json: @task
    else
      render json: @task.errors, status: :unprocessable_entity
    end
  end

  def destroy
    @task.destroy
  end

  private
    def set_task
      @task = Task.find(params[:id])
    end

    def task_params
      params.require(:task).permit(:content)
    end
end
```

## 3. データ作成

1. `rails c`してコンソール上で作成
2. seedデータを作成して投入
3. curlコマンドで作成
```
$ curl -X POST -H "Content-Type: application/json" -d '{"content":"hoge"}' localhost:3000/tasks
```
curlコマンドに関しては[こちら](https://viral-community.com/security/curl-8263/)が分かりやすい。
