# カスタムHooks

##　カスタムHooksとは
- Hooksを組み合わせて作成した関数。
- Hooksを使ったロジックを再利用するために作成する。
- 概念は関数化。機能部分を関数化するのが目的
- Hooksの条件
  - 頭文字がuse

※NOTE: Hooksの条件について、調べてけど、結構緩めな感じがする。


# useDebugValueを用いたカスタムフック
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