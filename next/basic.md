# Next.jsの特徴
- Reactのページ遷移の快適さなどを維持して、ページ単位でSSRやSSGを容易できる。
- ファイルベースの自動ルーティング（ファイルシステムルーティング）
- APIルート
- 静的ファイルの配信
- CSSモジュール
- ビルドインの便利なコンポーネント
- TypeScriptのサポート
- ゼロコンフィグ
- ホットリローディング

# ページの作成方法
- pagesディレクトリにファイルを作成する。
- エンドポイント名のディレクトリを作成し、page.tsxを作成することで、エンドポイントを作成できる。

# 動的ルーティング
- pagesディレクトリにファイルを作成する。
- `[xxx].tsx`の形式で動的ルーティングを実現できる。

# APIルート
- pages/apiディレクトリ以下にファイルを作成することで、APIルートを作成できる。
- ビルド時はこのAPIは使えないので、getStaticProps/getStaticPathsからは呼び出せない。

## APIルートの作成方法
- pages/apiディレクトリ以下にファイルを作成する。
- ファイル名がエンドポイント名になる。
- ファイル内部に関数を実装する。
- 関数の引数には、リクエスト情報とレスポンス情報が渡される。
- 関数の戻り値は、レスポンス情報と同じ形式で返す。
- レスポンス情報の型は、NextApiRequestとNextApiResponseを使用する。

```tsx
import { NextApiRequest, NextApiResponse } from 'next';

const handler = (req: NextApiRequest, res: NextApiResponse) => {
    res.status(200).json({ message: 'Server is running.' });
}

export default handler;
```

# 環境変数/コンフィグ
- Next.jsはビルドインで環境変数のための.envファイルを処理できる。
- プロジェクトルートに置いてある.envファイルは、ビルド時に自動で読み込まれる。
- 読み込まれるファイル
    - .env
    - .env.local
    - .env.${環境名}
    - .env.${環境名}.local
- .localがついているものは、.gitignoreに追加することで、Gitの管理対象から外す感じ。
- 接頭辞にNEXT_PUBLIC_をつけることで、クライアント側で環境変数を参照できる。

## 注意点
- 普通の環境変数は、再描画などで、クライアント側で読み込もうとしても読み込めない。

## 環境変数の設定方法
- .envファイルに環境変数を設定する。

## 環境変数の読み込み方法
- process.env.環境変数名
- process.env.NEXT_PUBLIC_環境変数名

```tsx
import { NextPage } from 'next';
import Head from 'next/head';

const Home: NextPage = () => {
    const env = process.env.ENV;
    const publicEnv = process.env.NEXT_PUBLIC_ENV;
    return (
        <>
            <Head>
                <title>Home</title>
            </Head>
            <div>
                Home
            </div>
            <div>
                {env}
            </div>
            <div>
                {publicEnv}
            </div>
        </>
    );
};

export default Home;
```