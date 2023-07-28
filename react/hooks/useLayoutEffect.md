# useLayoutEffectを用いたコンポーネント
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