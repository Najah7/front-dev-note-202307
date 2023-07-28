# SSR
- リクエスト毎にHTMLを生成する
- リクエスト毎にデータを取得する
- デファクトのレンダリング方法

# getServersidePropsについて
- SSRを実現するための関数。
- ページを描画する前に呼ばれる関数
- ページコンポーネントにpropsとして渡される。
- ビルド時には実行されない。
- リクエスト毎に実行される。

```tsx
export async function getServerSideProps(context) {
    return {
        props: {
            // propsとして渡したい値を指定する。
        }
    }
}
```

# サンプルコード
```tsx
import { GetServerSideProps, NextPage } from 'next';
import Head from 'next/head';

type SSRProps = {
    message: string;
}

const SSR: NextPage<SSRProps> = (props) => {
    return (
        <>
            <Head>
                <title>SSR</title>
            </Head>
            <div>
                SSR
            </div>
            <div>
                {props.message}
            </div>
        </>
    );
};

export const getServersideProps: GetServerSideProps<SSRProps> = async (context) => {
    const timestamp = new Date().getTime();
    const message = `${timestamp}にgetServerSidePropsが実行されました。`;
    return {
        props: {
            message
        }
    }
}

export default SSR;
```