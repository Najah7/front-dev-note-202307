# useReducerを用いたコンポーネント
- `useState`の代わりに`useReducer`を用いることで、複雑な状態を管理することができる
- 配列やオブジェクトなどの複数のデータをまとめたものを状態として扱う場合に用いられる
- useReducerの構成要素
  - reducer：更新の種類に応じて状態を更新する関数。
  - dispatch：更新するための関数
  - action：更新の種類を表すオブジェクト
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