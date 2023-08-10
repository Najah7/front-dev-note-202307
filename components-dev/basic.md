# コンポーネント開発

## コンポーネント開発のメリット
- コンポーネントの再利用性が高まる（デザインに一貫性を持たせやすい）
- コンポーネントのテストが容易になる
- コンポーネントの保守性が高まる
- 開発が容易になる
- コンポーネントの開発が並列化できる

## Presentational Component と Container Component
- Container Componentが親としてビジネスロジックを担い、子のPresentational Componentは親から渡されたpropsをもとに見た目を表示する
- Presentational Component
  - データを持たず、状態を持たない
  - データを受け取って表示するだけ
  - 見た目中心
  ```tsx
    import React from 'react';
    import './style.css';

    type ButtonProps = {
      label: string;
      onClick: () => void;
    };

    export const Button: React.FC<ButtonProps> = ({ label, text, disabled, onClick }) => {
      return (
        <div className="button-container">
          <span className="button-label">{label}</span>
            <button className="button" disabled={disabled} onClick={onClick}>
                {text}
            </button>
        </div>
  ```
- Container Component
    - デザインを一切実装しない
    - ビジネスロジックだけを実装する
    - 振る舞い中心
    ```tsx
    import React from 'react';
    import { useState, useCallback } from 'react';
    import { Button } from './Button';

    const usePopup = () => {
        const cb = useCallback(() => {
            prompt('Hello');
        }, []);

        return cb;
    };

    type CountButtonProps = {
        label: string;
        max: number;
    };

    export const CountButton: React.FC<CountButtonProps> = ({ label, max }) => {
        const [count, setCount] = useState(0);
        const displayPopup = usePopup();
        const [ count, setCount ] = useState(0);

        const onClick = useCallback(() => {
            const newCount = count + 1;
            setCount(newCount);

            if (count >= max) {
                displayPopup();
            }
        }, [count, max]);

    const disabled = count >= max;
    const text = disabled ? 'Cannot Click Anymore' : `You've clicked ${count} times`;

    return <Button label={label} text={text} disabled={disabled} onClick={onClick} />;

    };
    ```


## Storybook
- UIコンポーネント開発向けの支援ツール
- UIコンポーネントを独立した状態で開発できる
- UIコンポーネントのカタログを作成できる
- 一つのコンポーネントを複数の状態で確認できる
- UIコンポーネントのテストができる
- UIコンポーネントのドキュメントが作成できる
- UIコンポーネントのバージョン管理ができる
- Story：UIコンポーネントの状態を表す

### Storybookのインストール
```bash
$ npx sb@latest init # 👈自動的に必要なパッケージをインストールしてくれる
$ npm run storybook
```

### Storybookの設定
- .storybook/main.js
```js
module.exports = {
    stories: ['../src/**/*.stories.@(ts|tsx|js|jsx)'],
    addons: ['@storybook/addon-essentials'],
};
```

### Storybookの使い方

#### サンプルコード(コンポーネントと同じ場所に配置する)
- src/components/Button/Button.stories.tsx
```tsx
import React from 'react';
import { Story, Meta } from '@storybook/react';
import { Button, ButtonProps } from './Button';

export default {
    title: 'Example/Button',
    component: Button,
    // argTypes: コンポーネントのpropsの設定
    // backgroundColor: 引数名
    // control: プロパティのコントロールを表示する
    // control: 'color': プロパティのコントロールを色選択にする(カラーピッカーが表示される)
    argTypes: {
        backgroundColor: { control: 'color' },
    },
} as Meta;

const Template: Story<ButtonProps> = (args) => <Button {...args} />;
export const Primary = Template.bind({});
Primary.args = {
    label: 'ボタン',
};
```

#### サンプルコード(コンポーネントと別の場所に配置する)
- src/stories/Button.stories.tsx
```tsx
import React from 'react';
import { Story, Meta } from '@storybook/react';
import { Button, ButtonProps } from '../components/Button/Button';

export default {
    title: 'Example/Button',
    component: Button,
    // argTypes: コンポーネントのpropsの設定
    // backgroundColor: 引数名
    // control: プロパティのコントロールを表示する
    // control: 'color': プロパティのコントロールを色選択にする(カラーピッカーが表示される)
    argTypes: {
        backgroundColor: { control: 'color' },
    },
} as Meta;

const Template: Story<ButtonProps> = (args) => <Button {...args} />;
// bind: テンプレート関数に引数をバインドする
export const Primary = Template.bind({});
Primary.args = {
    label: 'ボタン',
};
```



