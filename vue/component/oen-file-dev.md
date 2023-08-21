# 単一ファイルでのコンポーネント開発

## 構成要素
- `template` : HTML
- `script` : JavaScript
- `style` : CSS

# ビルドの方法(.vue→.js)
- webpack + vue-loader
- rollup-plugin-vue + rollup
- vueify + browserify

※単一ファイルコンポーネントが提供するすべての機能（仕様）を利用できるのは、webpack + vue-loaderのみ

# 動作の流れ
1. JSファイルへのバンドル化
    - 依存するライブラリがJSファイルにバンドルされる（HTML, CSS, JS）
1. HTMLとして描画されたテンプレート
    - body要素以下にtemplateを描画する（JSで配置している）
1. 挿入されたスタイル
    - head要素以下にstyleを挿入する（JSで指定している）

## ビルド＆表示のコマンド
- `vue server ファイル名 --open`
    - `npm run build`
    - `npm run serve`

## 外部ファイルのインポート
- `<template src="ファイル名"></template>`
- `<script src="ファイル名"></script>`
- `<style src="ファイル名"></style>`

## スコープ付きCSS
- コンポーネントのスコープ内でのみ有効なCSS
- `<style scoped></style>`

## CSSモジュール
- CSSのクラス名をユニークなものに変換する仕組み
- CSSモジュールを使うことで、CSSのクラス名の衝突を防ぐことができる
- CSSモジュールを使うには、`<style module></style>`を使う
- 名前を付けることで、1つのファイルで複数のCSSモジュールを定義できる
```html
<template>
    <div class="container">
        <p class="text">Hello, Vue.js!</p>
    </div>
</template>

<style module="任意の名前">
    .container {
        border: 1px solid #ccc;
    }
    .text {
        color: red;
    }
</style>
```

## 他言語実装のサポート
- HTMLに変換できるマークアップ言語
    - Pug
    - Haml
- CSSプリプロセッサー
    - Sass
    - Less
    - Stylus
- AltJS
    - TypeScript
    - CoffeeScript
    - Babel

## 他言語の環境構築
- `vue create other-lang`

## 対話内容
| 対話項目 | 意味 |
|:--|:--|
| Use class-style component syntax? | クラス構文を使うか？ |
| Use Babel alongside TypeScript (required for modern mode, auto-detected polyfills, transpiling JSX)? | TypeScriptとBabelを併用するか？ |
| Pick a CSS pre-processor (PostCSS, Autoprefixer and CSS Modules are supported by default) | CSSプリプロセッサーを選択するか？ |
| where do you prefer placing config for Babel, ESLint, etc.? | 設定ファイルをどこに置くか？ |
| Save this as a preset for future projects? | 今回の設定をプリセットとして保存するか？ |


### HTMLに変換できるマークアップ言語
```html
<template lang="pug">
    div.container
        p.text Hello, Vue.js!
</template>
```

### CSSプリプロセッサー
```html
<style lang="sass">
    .container
        border: 1px solid #ccc
    .text
        color: red
</style>
```

### AltJS
```html
<script lang="ts">
    export default {
        data() {
            return {
                message: 'Hello, Vue.js!'
            }
        }
    }
</script>
```