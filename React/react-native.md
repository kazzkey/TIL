# React Nativeについて

参照：
[公式ドキュメント](https://reactnative.dev/) / 
[はじめて学ぶReactNativeハンズオン勉強会](https://npo-fitness-engineer.connpass.com/event/194833/) / 
[React勉強会資料](https://adoring-agnesi-69fd1d.netlify.app/)

環境：
macOS(Catalina) / 
[Expo Snack](https://snack.expo.io/)を使用
　
---
　
## 1. React Nativeとは

- Reactベースでネイティブアプリを開発できる
- iOSやAndroidどちらのアプリも作ることができる

　
## 2. 準備

```JavaScript
// React Nativeに必要なコンポーネントをインポート
import {
  ImageBackground,
  StyleSheet,
  Text,
  View,
  ScrollView,
  Dimensions,
  TextInput,
  Button,
  KeyboardAvoidingView,
} from 'react-native'

const App = () => {
  return (
    // 処理
  )
}
```

### 各コンポーネントの役割

- **KeyboardAvoidingView**タグ
  - このタグで囲むことでインプット時にキーボードに隠れてしまうのを解消できる
```JSX
<KeyboardAvoidingView behavior={"padding"}>
</KeyboardAvoidingView>
```

- **ImageBackgound**タグ
  - 背景画像を指定できる
```JSX
<ImageBackground source={{uri: "画像のパス"}}>
</ImageBackground>
```

- **ScrollView**タグ
  - このタグで囲んだ部分のスクロール表示をかんたんに実装できる

-  **View**タグ
  - HTMLでいうdivタグのようなもの

- **Text**タグ
  - テキストを表示するときのタグ

- **TextInput**タグ
  - スマートフォンのキーボードを表示させて入力画面を実装できる

- **Button**タグ
  - ボタンを実装できる

