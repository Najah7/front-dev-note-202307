# Contextを用いたコンポーネント
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
  - contextの作成
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

# useContextを用いたコンポーネント

## useContextとは
- useContextは、Contextオブジェクトが提供されている場合に、そのコンテクストの値に簡単にアクセスするためのHooks

```tsx
import React, { useContext } from 'react';

const UserContext = React.createContext({
  name: 'Guest',
  age: 20,
});

const App: React.FC = (): JSX.Element => {
  const user = useContext(UserContext);

  return (
    <div>
      <h1>Hello World</h1>
      <h1>Hello {user.name}</h1>
    </div>
  );
};

export default App;

```