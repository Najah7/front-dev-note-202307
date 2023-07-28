# useRefを用いたコンポーネント
- 書き換え可能なrefオブジェクトを作成するためのフック
- 使い道
  - データの保持：Ref場合、状態を更新するたびに再描画が発生するが、Refの場合は再描画が発生しない。なので描画に関係のない値の保持に使う。
  - DOMの参照：`ref.current`でDOMの参照をセットできる。inputなどで使える。

## 描画と関係のない値の保持
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

# forwardRefを用いたコンポーネント
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