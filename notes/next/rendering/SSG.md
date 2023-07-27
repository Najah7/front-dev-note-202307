# SSG
- ビルド時にHTMLを生成する
- ビルド時にデータを取得する
- ビルド時に`getStaticProps`を使用し、ページにpropsを返す
- 初期化後は通常のReactアプリケーション同様に、APIなどからデータを取得する

# getStaticPropsについて
- SSG/ISRを実現するための関数。
    - SSGの場合は、getStaticPathsとセットで使うことが多い
    - ISGの場合は、revalidate（有効期限）を返す必要がある。
- ページを描画する前に呼ばれる関数
- ページコンポーネントにpropsとして渡される。
- ビルド時に実行される。

# getStaticPathについて
- getStaticPropsとセットで使う。
- ビルド時に、どのパスに対して、getStaticPropsを実行するかを指定する。
- 例えば、getStaticPropsを実行するパスを動的に指定したい場合に使用する。
- getStaticPropsの実行前に実行される。
- 下記の2つのオブジェクトを返す
    - path(生成したいページのパスパラメータの組み合わせ)
    - fallback(パスパラメータの組み合わせが存在しない場合の挙動)
        - false: 404を返す
        - true: 404を返さない。リクエスト毎にページを生成する。
        - blocking: 404を返さない。リクエスト毎にページを生成する。ページの生成が完了するまで、リクエストをブロックする。

```tsx
export async function getStaticPath() {
    return {
        paths: [
            {
                params: {...}
            }
        ]
        fallback: false // trueもしくはblockingを指定することで、パスパラメータの組み合わせが存在しない場合の挙動を指定できる。
    }
}
```

# サンプルコード（getStaticProps + getStaticPaths）
```tsx
import { GetStaticPaths, GetStaticProps, NextPage } from 'next';
import Head from 'next/head';
import { useRouter } from 'next/router';
import { ParsedUrlQuery } from 'querystring';

type PostProps = {
    id: string;
    title: string;
}

const Post: NextPage<PostProps> = (props) => {
    const { id } = props
    const router = useRouter();

    if (router.isFallback) {
        return <div>Loading...</div>
    }
    
    return (
        <>
            <Head>
                <title>Post</title>
            </Head>
            <div>
                Post
            </div>
            <div>
                id: {id}
            </div>
            <div>
                title: {props.title}
            </div>
        </>
    );
};

export const getStaticPaths: GetStaticPaths = async () => {
    const paths = [
        {
            params: {
                id: '1'
            }
        },
        {
            params: {
                id: '2'
            }
        }
    ];
    return {
        paths,
        fallback: false
    }
}

interface PostParams extends ParsedUrlQuery {
    id: string;
}

export const getStaticProps: GetStaticProps<PostProps, PostParams> = async (context) => {
    const { id } = context.params;
    const title = `title${id}`;
    return {
        props: {
            id,
            title
        }
    }
}

export default Post;
```
