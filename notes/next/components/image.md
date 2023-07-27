## Image
- 画像を表示するためのコンポーネント
- サーバサイドで画像を最適化してくれる。
- 渡す属性は、基本的にimgタグと同じ。
- widthとheightは必須。
- srcには、publicディレクトリ以下のパスを指定する。
- 静的インポートした画像を表示する場合は、srcには、importした画像を指定する。（静的インポートの場合、widthとheightは必須ではない。）
　👆静的インポートした場合は最適されない。

### 画像の描画方法
- Imageコンポーネントを使った場合
    - 初期段階でビューポートに表示されない画像は描画せず、表示される画像のみ描画する。
    - スクロールによって画像が表示される場合、画像が表示されるまで、画像の代わりにプレースホルダーが表示される。

### propsで渡せるパラメータ
- src：画像のパス
- alt：画像のalt
- width：画像の幅
- height：画像の高さ
- layout：画像のレイアウト
    - fill：画像の幅と高さを100%にする。
    - fixed：画像の幅と高さを指定する。
    - responsive：画像の幅と高さを指定する。画像の幅と高さは、ビューポートの幅と高さによって変わる。
    - intrinsic：画像の幅と高さを指定する。デフォルト。
- placeholder：プレースホルダーの種類。読み込み中に表示される内容。
    - blur：ぼかし。画像のぼかしたものが表示される。
    - empty：空。なにも表示しない。
- blurDataURL：ぼかし。画像のぼかしたものが表示される。blurDataURLには、base64でエンコードした画像を指定する。
- unoptimized：画像の最適化を行わない。

### srcにパスを指定する場合の注意点
- 静的ファイルと違い画像のサイズを事前に取得できないため、layoutがfill以外の場合は、widthとheightを指定する必要がある。
- 外部リソースの画像を表示する場合、デフォルトでは最適化した画像を表示できない。
    - 画像の最適化を行うためには、next.config.jsに設定を追加する必要がある。
    - 下記の設定を追加することで、外部リソースの画像を最適化して表示できる。
    ```js
    module.exports = {
        images: {
            domains: ['example.com']
        }
    }
    ```

### 普通の描画
```tsx
import Image from 'next/image';

const Home: NextPage = () => {
    return (
        <>
            <Head>
                <title>Home</title>
            </Head>
            <div>
                Home
            </div>
            <Image src="/vercel.svg" width={400} height={400} />
        </>
    );
};

export default Home;
```

### 静的インポートした画像の描画
```tsx
import Image from 'next/image';
import vercel from '../public/vercel.svg';

const Home: NextPage = () => {
    return (
        <>
            <Head>
                <title>Home</title>
            </Head>
            <div>
                Home
            </div>
            <Image src={vercel} width={400} height={400} />
        </>
    );
};

export default Home;
```