# React.jsについて

参照：
掌田津耶乃『React.js Next.js 超入門』(秀和システム) / [React公式](https://ja.reactjs.org/)

環境：
macOS(Catalina) / React 16.13

---
## 1. React.jsとは
- フロントエンド・フレームワークのひとつ。Facebookが開発。
---
## 2. 特徴
#### ◎リアクティブプログラミング
- 元の値を変更すると、表示も自動更新される。

#### ◎仮想DOM
- 仮想DOMを操作することで高速になる。

#### ◎豊富な拡張機能
- コンポーネントや拡張プログラムを組み込んで使うことができる。

---

## 3. 動作の仕組み(基本的な動き方)

1. React組み込みタグを指定
```html
<div id="root">hoge</div>
```

2. 組み込み用タグの取得
```JavaScript
let dom = document.querySelector('#root');
```

3. エレメントを作成
```JavaScript
React.createElement(タグ名, 属性, 組み込まれるもの)


(例)
React.createElement(
  'p', {}, 'Hello React!!'
);
```

4. レンダリング実行
```JavaScript
ReactDOM.render(エレメント, DOM)
```
---
## 4. アプリケーション作成

#### コマンド(例)

```
# 作成
$ npx create-react-app プロジェクト名


# プロジェクト実行
$ yarn start


# プロジェクトをビルド
$ yarn build


#プロジェクトをテスト
$ yarn test
```

---
## 5. コンポーネント

#### 【 コンポーネントとは 】
- 表示内容や必要なデータ、処理などを一つのオブジェクトにまとめた「部品」のようなもの。組み込んでいろいろと使うことができる。

#### 【 コンポーネントの定義 】
1. ES2015(ES6)のクラスを用いた書き方
```JavaScript
class App extends React.Component {

  render() {
    return <h1>Hello World!</h1>;
  }
}
```
2. 関数を用いた書き方
```JavaScript
function App() {
  return <h1>Hello World!</h1>;
}
```

#### 【 コンポーネントの表示 】

レンダリング時に`<コンポーネント名 />`のようにタグで表示できる。
```JavaScript
ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

#### 【 コンポーネントにプロパティを渡す 】

引数`props`で受け渡しをする。<br>
クラスで定義するときは`this`が必要。
```JavaScript
// 定義(関数)
function Hello(props) {
  return <h1>Hello { props.name }!</h1>;
}

// 定義(クラス)
class Hello extends React.Component {
  render() {
    return <h1>Hello { this.props.name }!</h1>;
  }
}

----------------------------------------------------

// 呼び出し
ReactDOM.render(
  <Hello name="Taro" />,
  document.getElementById('root')
);

----------------------------------------------------

// 表示
Hello Taro!
```

#### 【コンポーネントのクラスの成り立ち】

```JavaScript
// React.Componentクラスを継承する形で始める
class Hello extends React.Component {

  // オブジェクトの初期値をここに設定する
  constructor(props) {
    super(props);
    this.hoge = props.hoge  //例
  }

  // メソッドを定義するときはここに記述する

  // レンダリングするためのメソッドを最後に記述する
  render() {
    return <h1>Hello { this.hoge }!</h1>;
  }
}
```

---
## 6. ステート

#### 【 ステートとは 】
- コンポーネントで利用する「値」の保管庫のようなもの。

#### 【 プロパティとの違い 】
- 「値を取り出して表示する」点においては同じ。ただstateは変更可能。

#### 【例】
以下の2つはどちらも同じ結果になる。

1. `state`を使った表示
```JavaScript
class Hello extends React.Component {

  constructor(props) {
    super(props);
    // state変数に初期値を設定
    this.state = { msg: 'Hello!' };
  }

  render() {
    return <h1>{ this.state.msg }!</h1>
  }
}

----------------------------------------------------

// 呼び出し
ReactDOM.render(
  <Hello />,
  document.getElementById('root')
);
```

2. `props`を使った表示
```JavaScript
class Hello extends React.Component {

  constructor(props) {
    super(props);
  }

  render() {
    return <h1>{ this.props.msg }!</h1>
  }
}

----------------------------------------------------

// 呼び出し
ReactDOM.render(
  <Hello msg="Hello" />,
  document.getElementById('root')
);
```

#### 【ステートの更新】

1. シンプルに値を更新する方法 / `setState({…値…})`
```JavaScript
class Hello extends React.Component {

  constructor(props) {
    super(props);
    this.state = { msg: 'Hello!' };
  }

  render() {
    return <div>
      <h1>{ this.state.msg }!</h1>
      <button onClick={() => this.setState({msg: 'Bye!'})}>Click</button>
    </div>
  }
}
```
※ `this.state.msg = 'Bye!'のように直接変更はできない。`

2. 現ステートを利用し新たな値を設定する方法 / `setState((state)=>({…値…}))`
```JavaScript
class Hello extends React.Component {

  constructor(props) {
    super(props);
    this.state = { msg: 'Hello!' };
    let timer = setInterval(()=>{
      this.setState((state)=>({
        msg: state.msg + "!"
      }));
    }, 10000);
  }

  render() {
    return <div>
      <h1>{ this.state.msg }!</h1>
    </div>
  }
}
```

---
## 7. イベント処理

```JavaScript
class Toggle extends React.Component {

  constructor(props) {
    super(props);
    this.state = { isToggleOn: true };

    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState(state => ({
      isToggleOn: !state.isToggleOn
    }));
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}

ReactDOM.render(
  <Toggle />,
  document.getElementById('root')
);
```

#### 【ポイント】
1. 関数設定
   - `onClick={ this.handleClick }`のようにメソッドを設定する。
   - メソッドはクラス内に定義する。

2. メソッドをバインド
   - `this.handleClick = this.handleClick.bind(this)`のように引数`this`をバインドすることで、イベントからメソッドが実行できるようになる。