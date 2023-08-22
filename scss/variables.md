# 変数

## SCSSでの変数の定義
- 変数は`$`を使って定義

```scss
$color: #333;
$font-sizes: (
    small: 12px,
    medium: 16px,
    large: 24px
    );

body {
    color: $color;
    font-size: map-get($font-sizes, medium);
}
```