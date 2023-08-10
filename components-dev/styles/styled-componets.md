### styled-components
- CSS in JSのライブラリの１つ
- JS内にCSSを効率的に書くためのもの
- コンポーネントと同じファイルに記述する

#### 書式
```tsx
import styled from 'styled-components';

const StyledButton = styled.button`
    background-color: #fff;
    border: 1px solid #ddd;
    border-radius: 3px;
    font-size: 24px;
    padding: 8px 10px;
`;
```

#### styled-componentsの導入

1. styled-componentsをインストール
```bash
npm install --save styled-components
npm install --save-dev @types/styled-components
```
2. next.config.jsにstyled-componentsの設定を追加
```js
const nextConfig = {
    reactStrictMode: true,
    compiler: {
        styledComponents: true,
    },
}

module.exports = nextConfig;
```

- SSRやSSG使用時にサーバーサイドでスタイルを適用するための設定
```tsx
// pages/_document.tsx

import React from 'react';
import Document, { DocumentContext } 'next/document';
import { ServerStyleSheet } from 'styled-components';

export default class MyDocument extends Document {
    static async getInitialProps(ctx: DocumentContext) {
        const sheet = new ServerStyleSheet();
        const originalRenderPage = ctx.renderPage;

        try {
            ctx.renderPage = () =>
                originalRenderPage({
                    enhanceApp: (App) => (props) =>
                        sheet.collectStyles(<App {...props} />),
                });

            const initialProps = await Document.getInitialProps(ctx);
            return {
                ...initialProps,
                styles: [
                    initialProps.styles,
                    sheet.getStyleElement()
                ],
            };
        } finally {
            sheet.seal();
        }
    }
}
```


#### サンプルコード
```tsx
import React from 'react';
import styled from 'styled-components';

const StyledButton = styled.button`
    background-color: #fff;
    border: 1px solid #ddd;
    border-radius: 3px;
    font-size: 24px;
    padding: 8px 10px;
`;

type ButtonProps = {
    label: string;
    onClick: () => void;
};

export const Button: React.FC<ButtonProps> = ({ label, onClick }) => {
    return <StyledButton onClick={onClick}>{label}</StyledButton>;
};
```

#### サンプルコード（propsでスタイルを変更する）
```tsx
import React from 'react';
import styled from 'styled-components';

type StyledButtonProps = {
    color: string;
};

const StyledButton = styled.button<StyledButtonProps>`
    background-color: ${(props) => props.color};
    border: 1px solid #ddd;
    border-radius: 3px;
    font-size: 24px;
    padding: 8px 10px;
`;
```

#### サンプルコード（mixinsを使う）
```tsx
import React from 'react';
import styled, { css } from 'styled-components';

const redColor = css`
    color: #f00;
`;

const blueBackground = css`
    background-color: #00f;
`;

const StyledButton = styled.button`
    ${redColor}
    ${blueBackground}
    border: 1px solid #ddd;
    border-radius: 3px;
    font-size: 24px;
    padding: 8px 10px;
`;
```

#### サンプルコード（スタイルを継承）
```tsx
import React from 'react';
import styled, { css } from 'styled-components';

const Text = styled.p`
    font-size: 16px;
    line-height: 1.5;
`;

const Title = styled(Text)`
    font-size: 24px;
    font-weight: bold;
`;
```

#### サンプルコード（スタイルを別の要素で使用する
```tsx
import React from 'react';
import styled, { css } from 'styled-components';

const Text = styled.p`
    font-size: 16px;
    line-height: 1.5;
`;

const Title = styled(Text)`
    font-size: 24px;
    font-weight: bold;
`;

const Sample = () => {
    return (
        <>
            <Title as="h1">タイトル</Title>
        </>
    );
};
```

#### サンプルコード（Themeを設定する）

##### Themeの設定
```tsx
// theme.ts
export const theme = {
    colors: {
        primary: '#0070f3',
        secondary: '#ff0000',
        third: '#00ff00',
    },
    fontSize: {
        small: '16px',
        medium: '24px',
        large: '32px',
    },
};
```

##### Themeの使用
```tsx
import React from 'react';
import styled, { css, ThemeProvider } from 'styled-components';
import { theme } from '../theme';

const Text = styled.p`
    font-size: ${(props) => props.theme.fontSize.small};
    line-height: 1.5;
`;

const Title = styled(Text)`
    font-size: ${(props) => props.theme.fontSize.large};
    font-weight: bold;
`;

const Sample = () => {
    return (
        <ThemeProvider theme={theme}>
            <Title as="h1">タイトル</Title>
        </ThemeProvider>
    );
};
```