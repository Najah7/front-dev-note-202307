#　メモ化について
- 再描画のタイミング
  - propsが変更されたとき
  - コンポーネント内で参照しているstateが変更されたとき
  - コンポーネント内で参照しているContextの値が変更されたとき
  - 親コンポーネントが再描画されたとき
- メモ化が有効な場面：親コンポーネントが再描画されたとき
<br>👆メモ化を用いたら、props, state, contextの値が変更されたときにのみ再描画されるようになる

# useCallbackを用いたコンポーネント
- コンポーネントの再レンダリングを防ぐためのフック
- 必要のない子要素のレンダリングや計算を防ぐことができる
- `useCallback`を用いることで、関数をメモ化することができる

# memoを用いたコンポーネント
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

# useCallbackを用いたコンポーネント
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

# useMemoを用いたコンポーネント
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

# React.me vs useCallback vs useMemo
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