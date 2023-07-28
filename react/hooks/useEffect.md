# useEffectを用いたコンポーネント
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