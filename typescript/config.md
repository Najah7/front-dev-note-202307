# TypeScriptの開発時の設定

## tsconfig.json
- typescriptの設定ファイル
- プロジェクトのルートディレクトリに配置する
- コンパイルに必要なオプションを記述する
- 対象となるファイルを指定する

### tsconfig.jsonの作成
```bash
tsc --init
```

### tsconfig.jsonの設定
- `allowJs`:JavaScriptファイルをコンパイルするかどうか
- `checkJs`:JavaScriptファイルの型チェックを行うかどうか
- `noImplicitAny`:暗黙的なany型を許可するかどうか
- `strictNullChecks`:nullとundefinedの代入を許可するかどうか
- `noUnusedLocals`:未使用のローカル変数をエラーとするかどうか
- `noUnusedParameters`:未使用のパラメータをエラーとするかどうか
- `noImplicitReturns`:関数の戻り値がない場合をエラーとするかどうか
- `noFallthroughCasesInSwitch`:switch文のcase文の最後にbreakがない場合をエラーとするかどうか
- `allowSyntheticDefaultImports`:default importを許可するかどうか
- `esModuleInterop`:CommonJSモジュールをESモジュールとして扱うかどうか
- `experimentalDecorators`:デコレータを有効にするかどうか
- `emitDecoratorMetadata`:デコレータのメタデータを出力するかどうか
- `target`:コンパイル後のJavaScriptのバージョンを指定
- `module`:コンパイル後のJavaScriptのモジュール方式を指定
- `outDir`:コンパイル後のJavaScriptの出力先を指定
- `rootDir`:コンパイル対象のTypeScriptのソースコードのルートディレクトリを指定
- `sourceMap`:ソースマップを出力するかどうか
- `noEmitOnError`:コンパイルエラーがある場合にJavaScriptを出力しないかどうか
- `strict`:`noImplicitAny`、`strictNullChecks`、`noUnusedLocals`、`noUnusedParameters`、`noImplicitReturns`、`noFallthroughCasesInSwitch`を有効にするかどうか
- `baseUrl`:モジュールの解決に使用するベースパスを指定
- `paths`:モジュールの解決に使用するパスを指定
- `typeRoots`:型定義ファイルの検索パスを指定
- `types`:型定義ファイルの指定
- `lib`:コンパイルに含めるライブラリを指定
- `include`:コンパイル対象のファイルを指定
- `exclude`:コンパイル対象から除外するファイルを指定

## Prettier
- コードフォーマッター

### Prettierのインストール
```bash
npm install --save-dev prettier
```

### Prettierの設定
- `.prettierrc`ファイルを作成する
- 代表的な値
    - `printWidth`:1行の最大文字数
    - `tabWidth`:タブの幅
    - `useTabs`:インデントにタブを使用するかどうか
    - `semi`:セミコロンを使用するかどうか
    - `singleQuote`:シングルクォートを使用するかどうか
    - `quoteProps`:オブジェクトのプロパティにクォートを使用するかどうか
    - `jsxSingleQuote`:JSXの属性にシングルクォートを使用するかどうか
    - `trailingComma`:末尾のカンマを使用するかどうか
    - `bracketSpacing`:オブジェクトのプロパティの前後にスペースを使用するかどうか
    - `jsxBracketSameLine`:JSXの閉じ括弧を同じ行にするかどうか
    - `arrowParens`:アロー関数の引数に括弧を使用するかどうか
    - `requirePragma`:ファイルの先頭に`// @format`を記述するかどうか
    - `insertPragma`:ファイルの先頭に`// @format`を記述するかどうか
    - `proseWrap`:テキストの折り返し方法
    - `htmlWhitespaceSensitivity`:HTMLの空白文字の扱い方
    - `endOfLine`:改行コードの種類

### package.jsonの設定
```json
"scripts": {
    "prettier-format": "prettier --config .prettierrc 'src/**/*.ts' --write"
}
```

### Prettierの実行
```bash
npx prettier --write .
```

## ESLint

### ESLintのインストール
```bash
npm install --save-dev eslint
```

### ESLintの設定
- `.eslintrc.js`ファイルを作成する
- 代表的な値
    - `env`:グローバル変数の定義
    - `extends`:共有設定の指定
    - `parser`:パーサーの指定
    - `parserOptions`:パーサーのオプション
    - `plugins`:使用するプラグインの指定
    - `rules`:ルールの指定
        - `semi`:セミコロンの有無（["error", "always"]などのように設定）
        ※エラーを出す場合は"error"、警告を出す場合は"warn"、無効にする場合は"off"を指定
        - `quotes`:クォートの種類
    - `settings`:プラグインの設定

### package.jsonの設定
```json
"scripts": {
    "eslint-check": "eslint --config .eslintrc.js 'src/**/*.ts'"
}
```