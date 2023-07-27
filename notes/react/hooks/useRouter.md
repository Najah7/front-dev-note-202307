# useRouter
- ルーティングの情報を取得するためのフック
- 引数
  - 第1引数：ルーティングの情報
- 代表的なプロパティ
  - pathname：現在のパス
  - query：クエリパラメータ
  - asPath：現在のパス（クエリパラメータを含む）
- 代表的メソッド
  - push：ページ遷移
    - 第1引数(pathname)：遷移先のパス
    - query：クエリパラメータ
    ```tsx
    import { useRouter } from 'next/router';

    const router = useRouter();

    const handleClick = () => {
      router.push({
        pathname: '/about',
        query: {
          id: 1
        }
      });
    };
    ```
  - replace：ページ遷移（履歴に残らない）
  - reload：ページのリロード
  - back：戻る
  - prefetch：ページの事前読み込み

## イベントの検知
- useRouterのイベントを検知することができる。

```tsx
import { useRouter } from 'next/router';

const router = useRouter();

const handleClick = () => {
  router.push({
    pathname: '/about',
    query: {
      id: 1
    }
  });
};

useEffect(() => {
  router.events.on('routeChangeStart', () => {
    console.log('routeChangeStart');
  });
  router.events.on('routeChangeComplete', () => {
    console.log('routeChangeComplete');
  });
  router.events.on('beforeHistoryChange', () => {
    console.log('beforeHistoryChange');
  });
  router.events.on('routeChangeError', () => {
    console.log('routeChangeError');
  });
  router.events.on('hashChangeStart', () => {
    console.log('hashChangeStart');
  });
  router.events.on('hashChangeComplete', () => {
    console.log('hashChangeComplete');
  });
}, []);
```