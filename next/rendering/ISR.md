# ISR
- SSGのHTMLをキャッシュしておき、必要に応じて再生成する
- アクセスに応じて、ページを再生成する
- 有効期限を設定することができる

# サンプルコード
```tsx
import { GetStaticProps, NextPage } from 'next';
import Head from 'next/head';
import { useRouter } from 'next/router';

type ISRProps = {
    message: string;
}

const ISR: NextPage<ISRProps> = (props) => {
    const {message} = props;

    const router = useRouter();

    if (router.isFallback) {
        return <div>Loading...</div>
    }

    return (
        <>
            <Head>
                <title>ISR</title>
            </Head>
            <div>
                ISR
            </div>
            <div>
                {props.message}
            </div>
        </>
    );
};

export const getStaticProps: GetStaticProps<ISRProps> = async (context) => {
    const timestamp = new Date().getTime();
    const message = `${timestamp}にgetStaticPropsが実行されました。`;
    return {
        props: {
            message
        },
        revalidate: 60 // 秒単位で指定する。60秒後に再生成される。
    }
}

export default ISR;
```