react-modalについて

参照：
[GitHub](https://github.com/reactjs/react-modal)
[公式ドキュメント](https://reactcommunity.org/react-modal)

環境：
macOS(Catalina) / React 16.13

---
## 1. react-modalとは

- Reactでモーダルを簡単に実装できるライブラリ。
---

## 2. インストール

```
$ npm install --save react-modal

または

$ yarn add react-modal
```

---

## 3. 導入例

```JavaScript
import React from 'react';
import ReactDOM from 'react-dom';

// react-modalをインポート
import ReactModal from 'react-modal';

// 例としてAppクラスでモーダルを設定
class App extends React.Component {
  constructor () {
    super();
    this.state = {
      showModal: false
    };

    this.handleOpenModal = this.handleOpenModal.bind(this);
    this.handleCloseModal = this.handleCloseModal.bind(this);
  }

  // モーダルの開閉メソッドの定義
  handleOpenModal () {
    this.setState({ showModal: true });
  }

  handleCloseModal () {
    this.setState({ showModal: false });
  }

  // モーダルのタグはインポートした名前と合わせる必要がある。
  render () {
    return (
      <div>
        <button onClick={this.handleOpenModal}>Trigger Modal</button>
        <ReactModal
           isOpen={this.state.showModal}
           contentLabel="Minimal Modal Example"
        >
          <button onClick={this.handleCloseModal}>Close Modal</button>
        </ReactModal>
      </div>
    );
  }
}

const props = {};

ReactDOM.render(
  <App {...props} />, document.getElementById('root')
)
```
