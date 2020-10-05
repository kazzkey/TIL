# フックについて

参照：
[React公式ドキュメント](https://ja.reactjs.org/)

環境：
macOS(Catalina) / React 16.13

---
## フックとは
- React 16.8で追加された機能、stateなどの機能をクラスを書かずに使うことができる。
- フックはクラス内部や、if文内などでは動作しない。


#### 【useState】
- stateを配列で定義。名前は任意につけることができる。
```
[state変数名, stateの値を更新する関数名] = useState(初期値);
```

```JavaScript
// useStateをインポート
import React, { useState } from 'react';

function Example() {
  // useState
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

#### 【useEffect】
- 関数の実行タイミングをReactのレンダリング後に遅らせる。
- 初回レンダー時と毎回の更新時に呼び出される。
```
userEffect(() => { 関数など });
```

```JavaScript
// useEffectをインポート
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  // useEffect
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  })

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

- クラスの場合は、componentDidMountやcomponentDidUpdateで定義。
- 同じコードを2回書かなくてはならないというデメリットがuseEffectで解消される。
```JavaScript
componentDidMount() {
  document.title = `You clicked ${this.state.count} times`;
}
componentDidUpdate() {
  document.title = `You clicked ${this.state.count} times`;
}
```

- 第二引数に[count]を渡すとcountに変化があったときのみ再レンダーされる。
```JavaScript
import React, { useState, useEffect } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  // useEffectの第二引数に[count]を指定
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  }, [count])

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

#### 【useContext】
- propsをトップダウンで渡すことなく、共有できる。
```
const value = useContext(MyContext);
```

```JavaScript
// useContextをインポート
import React, { useContext } from 'react';

// テーマの定義
const themes = {
  light: {
    foreground: "#000000",
    background: "#eeeeee"
  },
  dark: {
    foreground: "#ffffff",
    background: "#222222"
  }
};

// デフォルトテーマ="light"のコンテクストを作成
const ThemeContext = React.createContext(themes.light);

function App() {
  return (
    // テーマ="dark"を値をして渡す。その際、プロバイダを使用する。
    <ThemeContext.Provider value={themes.dark}>
      <Toolbar />
    </ThemeContext.Provider>
  );
}

// コンテクストを使えば中間のコンポーネントには何も値を渡す必要がなくなる
function Toolbar(props) {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}

function ThemedButton() {
  // コンテクストを読むためにuseContextで指定する
  const theme = useContext(ThemeContext);
  return (
    // コンテクストから呼び出す
    <button style={{ background: theme.background, color: theme.foreground }}>
      I am styled by theme context!
    </button>
  );
}
```

#### 【useReducer】
- useStateの代替。Reduxの機能が公式React機能として使える。
- stateの管理が複雑になる場合に有効。
```
const [state, dispatch] = useReducer(reducer, 初期値);
```

```JavaScript
// useReducerをインポート
import React, { useReducer } from 'react';

// 初期値を定義
const initialState = { count: 0 };

// リデューサを定義
function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement':
      return {count: state.count - 1};
    default:
      throw new Error();
  }
}

function Counter() {

  const [state, dispatch] = useReducer(reducer, initialState);
  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({type: 'decrement'})}>-</button>
      <button onClick={() => dispatch({type: 'increment'})}>+</button>
    </div>
  )
}

export default Counter;
```