# useImperativeHandleを用いたコンポーネント
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