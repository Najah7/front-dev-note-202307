# SCSS

## 入れ子でのスタイルの定義
- CSSのように入れ子でスタイルを定義できる
- ただし、入れ子が深くなりすぎると可読性が下がるので注意

```scss
body {
    color: #333;
    font-size: 16px;

    .container {
        width: 100%;
        height: 100%;
    }
}
```

## &とは
- `&`は親要素を参照するためのキーワード

```scss
a {
    color: #333;
    text-decoration: none;

    &:hover {
        text-decoration: underline;
    }
}
```

## __とは
- `__`は子要素を参照するためのキーワード

```scss
.container {
    width: 100%;
    height: 100%;

    &__item {
        width: 50%;
        height: 50%;
    }
}
```

## @importとは
- `@import`はファイルを読み込むためのキーワード
- `@import`を使うと、読み込んだファイルの中身がそのまま読み込んだファイルに展開される
- 読み込まれるファイルは`_`から始まるファイル名にすることで、コンパイル時にCSSファイルに出力されないようにできる


```scss
// _animation.scssを読み込む
// _variables.scssを読み込む

@import "animation";
@import "variables";
```

## @functionとは
- `@function`は関数を定義するためのキーワード

```scss
@function double($number) {
    @return $number * 2;
}

.container {
    width: double(100px);
    height: double(100px);
}
```

## @mixinとは
- `@mixin`はミックスインを定義するためのキーワード

```scss
// 5pxがデフォルト値
@mixin border-radius($radius: 5px) {
    -webkit-border-radius: $radius;
    -moz-border-radius: $radius;
    border-radius: $radius;
}

@mixin flex-center {
    display: flex;
    justify-content: center;
    align-items: center;
}

.container {
    @include border-radius(10px);
    @include flex-center;
}
```

## @ifとは
- `@if`は条件分岐を行うためのキーワード

```scss
@mixin border-radius($radius: 5px) {
    @if $radius > 0 {
        -webkit-border-radius: $radius;
        -moz-border-radius: $radius;
        border-radius: $radius;
    }
}
```

## @contentとは
- `@content`はミックスインの中で、ミックスインを呼び出した箇所のコードを展開するためのキーワード

```scss
@mixin media($breakpoint) {
    @media screen and (min-width: $breakpoint) {
        @content;
    }
}

.container {
    width: 100%;

    @include media(768px) {
        width: 50%;
    }
}
```

## @extendとは
- `@extend`はスタイルを継承するためのキーワード

```scss 
.button {
    display: inline-block;
    padding: 10px 20px;
    border-radius: 5px;
    background-color: #333;
    color: #fff;
}

.button--primary {
    @extend .button;
    background-color: #f00;
}
```

