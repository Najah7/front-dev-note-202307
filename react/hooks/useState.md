# useStateを用いたコンポーネント
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
      <button onClick={(prev) => setCount(prev + 1)}>+</button>
    </div>
  );
};
```