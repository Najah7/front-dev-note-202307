# React

## プロジェクトの作成
```bash
npx create-react-app <プロジェクト名> --template typescript
```

## ディレクトリ構成
```bash
├── README.md：プロジェクトの説明
├── node_modules：パッケージのインストール先
├── package.json：パッケージの管理
├── public
│   ├── favicon.ico：favicon
│   ├── index.html：アプリケーションのエントリーポイント
│   └── manifest.json：PWAの設定
├── src
│   ├── App.css：アプリケーションのスタイル
│   ├── App.test.tsx：テスト
│   ├── App.tsx：アプリケーションのエントリーポイント
│   ├── index.css：アプリケーションのスタイル
│   ├── index.tsx：アプリケーションのエントリーポイント
│   ├── logo.svg：ロゴ
│   ├── react-app-env.d.ts：環境変数の型定義
│   ├── reportWebVitals.ts：パフォーマンスの計測
│   └── setupTests.ts：テストの設定
└── tsconfig.json：TypeScriptの設定
```

## Reactの内容がページに反映されるまでの流れ
1. `public/index.html`が読み込まれ、ブラウザに表示される
2. ブラウザがJavaScriptのコードを取得し、Reactのコードを実行する
3. render()で与えられたAppを、rootオブジェクト作成時に与えられたrootというIDを持つ要素に描画する

※rootというIDをもつdivタグ以下にAppコンポーネントが描画される

## src/index.tsxの内容
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

## Reactで使われるTypeScriptの型
- `JSX.Element`：JSXで書かれた要素の型
- `React.FC`：関数コンポーネントの型
- `React.VFC`：関数コンポーネントの型（暗黙的にchildrenをとらない）
- `React.ReactNode`：JSXで書かれた要素の型
- `React.Component`：クラスコンポーネントの型


## コンポーネントの作成
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

## JSXで書かれたコンポーネントがブラウザで表示するまでの流れ
1. webpackがJSXをJavaScript(JavaScriptのオブジェクト)に変換する
2. 変換されたJavaScriptのコードをブラウザが読み込み・実行することで画面への描画が行われる
3. 仮想DOMと実際のDOMの差分を検知し、変更があった部分のみを実際のDOMに反映する

### 仮想DOM
- メモリ上に保存された模式的なDOMツリー
- 前回構築した時の仮想DOMと比較し、変更があった部分のみを実際のDOMに反映する

## JSXのルール
- 基本はHTMLと同じ
- `{}`で囲むことでJavaScriptの式を埋め込むことができる
- `className`属性を使用することで、`class`属性を指定することができる

## Reactコンポーネント
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

## propsを用いたコンポーネント
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

## useStateを用いたコンポーネント
- コンポーネントの状態を管理するためのフック
- `useState`を用いることで、コンポーネントの状態を管理することができる

```tsx
import React, { useState } from 'react';

const App: React.FC = (): JSX.Element => {
  const [count, setCount] = useState<number>(0);

  return (
    <div>
      <h1>Hello World</h1>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>+</button>
    </div>
  );
};
```

## useEffectを用いたコンポーネント
- 副作用を扱うためのフック
- 副作用とは：コンポーネントの描画に関係ない処理
- `useEffect`を用いることで、コンポーネントの描画後に副作用を実行することができる
- 引数
  - 第一引数：副作用を実行する関数
  - 第二引数：副作用を実行するタイミングを制御する配列
    - 空の配列を渡すと、初回のみ実行される
    - 何も渡さないと、毎回実行される
    - 特定の値を渡すと、その値が変更された時のみ実行される

```tsx
import React, { useState, useEffect } from 'react';

const App: React.FC = (): JSX.Element => {
  const [count, setCount] = useState<number>(0);

  useEffect(() => {
    console.log('useEffect');
  }, [count]);

  return (
    <div>
      <h1>Hello World</h1>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>+</button>
    </div>
  );
};
```

## useLayoutEffectを用いたコンポーネント
- `useEffect`と同じように副作用を扱うためのフック
- `useEffect`との違い
  - `useEffect`はDOMの描画後に実行される
  - `useLayoutEffect`はDOMの描画前に実行される

```tsx
import React, { useState, useEffect, useLayoutEffect } from 'react';

const App: React.FC = (): JSX.Element => {
  const [count, setCount] = useState<number>(0);

  useEffect(() => {
    console.log('useEffect');
  }, [count]);

  useLayoutEffect(() => {
    console.log('useLayoutEffect');
  }, [count]);

  return (
    <div>
      <h1>Hello World</h1>
      <p>{count}</p>
      <button onClick={() => setCount(count + 1)}>+</button>
    </div>
  );
};
```

## useRefを用いたコンポーネント
- 書き換え可能なrefオブジェクトを作成するためのフック
- 使い道
  - データの保持：Ref場合、状態を更新するたびに再描画が発生するが、Refの場合は再描画が発生しない。なので描画に関係のない値の保持に使う。
  - DOMの参照：`ref.current`でDOMの参照をセットできる。inputなどで使える。

### 描画と関係のない値の保持
```tsx
import React, { useState, useEffect, useLayoutEffect, useRef } from 'react';

const App: React.FC = (): JSX.Element => {
  const [count, setCount] = useState<number>(0);
  const countRef = useRef<number>(0);

  useEffect(() => {
    console.log('useEffect');
  }, [count]);

  useLayoutEffect(() => {
    console.log('useLayoutEffect');
  }, [count]);

  return (
    <div>
      <h1>Hello World</h1>
      <p>{count}</p>
      <p>{countRef.current}</p>
      <button onClick={() => setCount(count + 1)}>+</button>
    </div>
  );
};
```

### DOMの参照
```tsx
import React, { useState, useEffect, useLayoutEffect, useRef } from 'react';

const App: React.FC = (): JSX.Element => {
  const [count, setCount] = useState<number>(0);
  const countRef = useRef<HTMLInputElement>(null);

  useEffect(() => {
    console.log('useEffect');
  }, [count]);

  useLayoutEffect(() => {
    console.log('useLayoutEffect');
  }, [count]);

  return (
    <div>
      <h1>Hello World</h1>
      <p>{count}</p>
      <p>{countRef.current}</p>
      <button onClick={() => setCount(count + 1)}>+</button>
      <input type="text" ref={countRef} />
    </div>
  );
};
```

## forwardRefを用いたコンポーネント
- `ref`を受け取ることができるコンポーネントを作成するためのフック
- `ref`を受け取るコンポーネントは、`React.forwardRef`でラップする必要がある
```tsx
import React, {useRef} from 'react';

const MyInput = (props, ref) => {
  console.log(ref); // {current: undefined}
  return <input type="text" />;
};

const WrappedMyInput = React.forwardRef(MyInput);

const App = () => {
  const ref = useRef();

  return (
    <div>
      <WrappedMyInput ref={ref} />
    </div>
  );
};

export default App;
```

## useImperativeHandleを用いたコンポーネント
- `useRef`に代入される値を制御するためのフック
- `useRef`と組み合わせて使う。
- 引数
  - 第一引数：`useRef`で作成したrefオブジェクト
  - 第二引数：`useRef`で作成したrefオブジェクトに代入される値
  - 第三引数：`useRef`で依存配列

```tsx
import React, { useRef, useImperativeHandle } from 'react';

const MyInput = (props, ref) => {
  const inputRef = useRef();

  useImperativeHandle(ref, () => ({
    focus: () => {
      inputRef.current.focus();
    },
  }));

  return <input type="text" ref={inputRef} />;
};

const WrappedMyInput = React.forwardRef(MyInput);

const App = () => {
  const ref = useRef();

  return (
    <div>
      <WrappedMyInput ref={ref} />
      <button onClick={() => ref.current.focus()}>フォーカス</button>
    </div>
  );
};

export default App;
```

## Contextを用いたコンポーネント
- propsでバケツリレーで値を渡さなくて済む。
- コンポーネントツリーとは別に、グローバルに値を保持している
- 構成要素
  - Provider：値を渡す側
  - Consumer：値を受け取る側
- 使い方
  - 流れ
    1. contextの作成
    2. Providerで値を設定
    3. Consumerで値を受け取る
  - cotextの作成
  ```tsx
  import React from 'react';

  const UserContext = React.createContext({
    name: 'Guest',
    age: 20,
  });
  ```
  - Providerで値を渡す
  ```tsx
  import React from 'react';
  import UserContext from './contexts/UserContext';

  const App: React.FC = (): JSX.Element => {
    return (
      <UserContext.Provider value={{ name: 'Taro', age: 20 }}>
        <div>
          <h1>Hello World</h1>
        </div>
      </UserContext.Provider>
    );
  };
  ```
- Consumerで値を受け取る
```tsx
import React from 'react';

const UserContext = React.createContext({
  name: 'Guest',
  age: 20,
});

const App: React.FC = (): JSX.Element => {
  return (
    <UserContext.Provider value={{ name: 'Taro', age: 20 }}>
      <div>
        <h1>Hello World</h1>
        <UserContext.Consumer>
          {(value) => {
            return (
              <div>
                <h1>Hello {value.name}</h1>
              </div>
            );
          }}
        </UserContext.Consumer>
      </div>
    </UserContext.Provider>
  );
};
```

## useContextを用いたコンポーネント

## useReducerを用いたコンポーネント
- `useState`の代わりに`useReducer`を用いることで、複雑な状態を管理することができる
- 配列やオブジェクトなどの複数のデータをまとめたものを状態として扱う場合に用いられる
- useReducerの構成要素
  - dispatch：更新するための関数
  - action：更新の種類を表すオブジェクト
  - reducer：更新の種類に応じて状態を更新する関数。
- useReducerの使い方
  - 基本的な流れ
    - reducerの作成
    - useReducerの呼び出し(第１引数にreducer、第２引数に初期値を指定。戻り値は配列で、第１要素に状態、第２要素にdispatch関数が格納されている)
    - 後はStateと同じ
```tsx
import React, { useReducer } from 'react';

type StateType = {
  count: number;
};

const initialState: StateType = {
  count: 0,
};

const reducer = (state: StateType, action: any): StateType => {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error();
  }
};

const App: React.FC = (): JSX.Element => {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <h1>Hello World</h1>
      <p>{state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>+</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>-</button>
    </div>
  );
};
```

##　メモ化について
- 再描画のタイミング
  - propsが変更されたとき
  - コンポーネント内で参照しているstateが変更されたとき
  - コンポーネント内で参照しているContextの値が変更されたとき
  - 親コンポーネントが再描画されたとき
- メモ化が有効な場面：親コンポーネントが再描画されたとき
<br>👆メモ化を用いたら、props, state, contextの値が変更されたときにのみ再描画されるようになる
## useCallbackを用いたコンポーネント
- コンポーネントの再レンダリングを防ぐためのフック
- 必要のない子要素のレンダリングや計算を防ぐことができる
- `useCallback`を用いることで、関数をメモ化することができる

## memoを用いたコンポーネント
- コンポーネントの再レンダリングを防ぐためのフック
- `memo`を用いることで、コンポーネントをメモ化することができる
-　親要素のコールバック関数を子要素にある場合再描画されてしまうので注意（useCallbackが必要）
```tsx
import React, { memo } from 'react';

type Props = {
  count: number;
};

const ComponentA: React.FC<Props> = memo<Props>((props) => {
  console.log('ComponentA');
  return (
    <div>
      <h1>ComponentA</h1>
      <p>{props.count}</p>
    </div>
  );
});

```

## useCallbackを用いたコンポーネント
- コンポーネントの再レンダリングを防ぐためのフック
- `useCallback`を用いることで、関数をメモ化することができる
- 親からコールバック関数をもらったときに用いる。（なぜなら、親の再描画のタイミングで子コンポーネントの内部状態が変化し、再描画してしまうから。）
- React.memoと併用する。memoのコールバック問題を解決するために使う。
- メモ化したコンポーネントにメモ化したコールバック関数を渡すことで、コールバック関数の再生成を防ぐことができる。
- 引数
  - 第１引数：メモ化関数
  - 第２引数：依存配列。（空の場合は常に同じ値を返す）
```tsx
import React, { useCallback, useState } from 'react';

const App: React.FC = (): JSX.Element => {
  const [count, setCount] = useState<number>(0);
  const [text, setText] = useState<string>('');

  const handleClick = useCallback(() => {
    setCount(count + 1);
  }, [count]);

  const handleChange = useCallback(
    (e: React.ChangeEvent<HTMLInputElement>) => {
      setText(e.target.value);
    },
    []
  );

  return (
    <div>
      <h1>Hello World</h1>
      <p>{count}</p>
      <button onClick={handleClick}>+</button>
      <input type="text" value={text} onChange={handleChange} />
    </div>
  );
};
```

## useMemoを用いたコンポーネント
- コンポーネントの再描画を防ぐためのフック
- メモ化された値を返すフック
- 不要な値の計算をスキップできる
- 引数
  - 第1引数：値を生成する関数
  - 第2引数：依存配列

```tsx
import React, { useMemo, useState } from 'react';

const App: React.FC = (): JSX.Element => {
  const [count, setCount] = useState<number>(0);
  const [text, setText] = useState<string>('');

  const doubleCount = useMemo(() => {
    return count * 2;
  }, [count]);

  const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
    setText(e.target.value);
  };

  return (
    <div>
      <h1>Hello World</h1>
      <p>{doubleCount}</p>
      <button onClick={() => setCount(count + 1)}>+</button>
      <input type="text" value={text} onChange={handleChange} />
    </div>
  );
};
```

## React.me vs useCallback vs useMemo
- React.memo
  - コンポーネントの再描画を防ぐためのフック
  - メモ化されたコンポーネントを返すフック
  - 引数
    - 第1引数：コンポーネント
    - 第2引数：依存配列
- useCallback
  - コンポーネントの再描画を防ぐためのフック
  - メモ化されたコールバック関数を返すフック
  - 基本的にはReact.memoの欠点回避のために使うイメージ
  - 引数
    - 第1引数：コールバック関数
    - 第2引数：依存配列
- useMemo
  - コンポーネントの再描画を防ぐためのフック
  - メモ化された値を返すフック
  - 引数
    - 第1引数：値を生成する関数
    - 第2引数：依存配列


## useDebugValueを用いたカスタムフック
- カスタムフックのデバッグ用のフック
- 引数
  - 第1引数：デバッグ用の値
  - 第2引数：デバッグ用の関数
```tsx
import React, { useEffect, useState, useDebugValue } from 'react';

const useCounter = (initialCount: number) => {
  const [count, setCount] = useState<number>(initialCount);

  useEffect(() => {
    const timer = setTimeout(() => {
      setCount((prevCount) => prevCount + 1);
    }, 1000);
    return () => clearTimeout(timer);
  }, [count]);

  useDebugValue(count > 0 ? '正の数' : '負の数');

  return count;
};