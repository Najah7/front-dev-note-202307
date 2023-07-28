### リンク
- Linkを使うことで、通常のようにHTMLファイルなどを取得して描画するのではなく、クライアントサイドで新しいページを描画することができる。
- 上記が実現されるにあたって、非同期で必要なデータを予め取得している。なので高速になる
- Linkコンポーネントを使用することで、ページ遷移を行うことができる。
- Linkコンポーネントのhrefには、pagesディレクトリ以下のパスを指定する。
- Linkコンポーネントの子要素には、aタグを指定する。
- aタグの代わりにbuttonを使用した場合、onClickコールバックが渡され、コールバックをトリガーにページ遷移が行われる。

※ useRouter.pushでもページ遷移はできる。

```tsx
import Link from 'next/link';

const Home: NextPage = () => {
    return (
        <>
            <Head>
                <title>Home</title>
            </Head>
            <div>
                Home
            </div>
            <Link href="/about">
                <a>About</a>
            </Link>
        </>
    );
};

export default Home;
```

#### オブジェクトでの指定
- Linkコンポーネントのhrefには、オブジェクトを指定することもできる。
- オブジェクトのpathnameには、pagesディレクトリ以下のパスを指定する。

```tsx
import Link from 'next/link';

const Home: NextPage = () => {
    return (
        <>
            <Head>
                <title>Home</title>
            </Head>
            <div>
                Home
            </div>
            <Link href={{
                pathname: '/about',
                query: {
                    id: 1
                }
            }}>
                <a>About</a>
            </Link>
        </>
    );
};

export default Home;
```