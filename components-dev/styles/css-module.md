### CSS Modules
- CSSをモジュール化するための仕組み
- CSSファイルとして、ファイルを分離して、インポートして使う
- file.module.cssというファイル名にすると、CSS Modulesとして認識される

#### サンプルコード
```css
/* Button.module.css */
.button {
    background-color: #fff;
    border: 1px solid #ddd;
    border-radius: 3px;
    font-size: 24px;
    padding: 8px 10px;
}
```

```tsx
// Button.tsx

import React from 'react';
import styles from './Button.module.css';

type ButtonProps = {
    label: string;
    onClick: () => void;
};

export const Button: React.FC<ButtonProps> = ({ label, onClick }) => {
    return (
        <button className={styles.button} onClick={onClick}>
            {label}
        </button>
    );
};
```