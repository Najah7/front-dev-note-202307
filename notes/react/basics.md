# Reactの内容がページに反映されるまでの流れ
1. `public/index.html`が読み込まれ、ブラウザに表示される
2. ブラウザがJavaScriptのコードを取得し、Reactのコードを実行する
3. render()で与えられたAppを、rootオブジェクト作成時に与えられたrootというIDを持つ要素に描画する

※rootというIDをもつdivタグ以下にAppコンポーネントが描画される

# src/index.tsxの内容
```tsx
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';

const root = ReactDOM.createRoot(
    document.getElementById('root') // rootというIDをもつ要素を作成
)

root.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
);
```

# コンポーネントの作成
- `src/components`ディレクトリを作成
```tsx
import React from 'react';

const App: React.FC = () => {
  return (
    <div>
      <h1>Hello World</h1>
    </div>
  );
};

```

# JSXで書かれたコンポーネントがブラウザで表示するまでの流れ
1. webpackがJSXをJavaScript(JavaScriptのオブジェクト)に変換する
2. 変換されたJavaScriptのコードをブラウザが読み込み・実行することで画面への描画が行われる
3. 仮想DOMと実際のDOMの差分を検知し、変更があった部分のみを実際のDOMに反映する

## 仮想DOM
- メモリ上に保存された模式的なDOMツリー
- 前回構築した時の仮想DOMと比較し、変更があった部分のみを実際のDOMに反映する

# JSXのルール
- 基本はHTMLと同じ
- `{}`で囲むことでJavaScriptの式を埋め込むことができる
- `className`属性を使用することで、`class`属性を指定することができる

# Reactコンポーネント
- 見た目と振る舞いをセットにしたUIの部品の単位
- 関数コンポーネント
```tsx
import React from 'react';

const App: React.FC = (): JSX.Element => {
  return (
    <div>
      <h1>Hello World</h1>
    </div>
  );
};

```
- クラスコンポーネント
```tsx
import React from 'react';

class App extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello World</h1>
      </div>
    );
  }
}
```
- 関数コンポーネント
```tsx
import React from 'react';

const App: React.FC = () => {
  return (
    <div>
      <h1>Hello World</h1>
    </div>
  );
};
```

# propsを用いたコンポーネント
```tsx
import React from 'react';

type Props = {
  name: string;
  children: React.ReactNode;
};

const App: React.FC<Props> = ({ name }):  JSX.Element =>{
  return (
    <div>
      <h1>Hello {name}</h1>
    </div>
  );
};
```