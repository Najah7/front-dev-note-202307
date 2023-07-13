# TypeScriptのツール

## TypeScriptのインストール
```sh
$ npm install -g typescript
```

## TypeScriptのコンパイル
```sh
$ tsc <ファイル名>
```
## TypeScriptのコンパイラの構成要素
- Scanner：ソースコードをトークンに分割する
- Parser：トークンを構文木に変換する
- Binder：構文木に対して意味解析を行う
- Checker：構文木に対して型チェックを行う
- Emitter：構文木をJavaScriptに変換する

### オプション
- `--target`：コンパイル後のJavaScriptのバージョンを指定
- `--watch`：ファイルの変更を監視して自動的にコンパイル
- `--outDir`：コンパイル後のJavaScriptの出力先を指定
- `--module`：コンパイル後のJavaScriptのモジュール方式を指定
- `--lib`：コンパイル時に参照する型定義ファイルを指定
- `--declaration`：コンパイル時に型定義ファイルを出力
- `--sourceMap`：ソースマップを出力
- `--removeComments`：コメントを削除
- `--noImplicitAny`：暗黙的なany型を許可しない
- `--strictNullChecks`：nullとundefinedの代入を許可しない
- `--noUnusedLocals`：未使用のローカル変数をエラーとする
- `--noUnusedParameters`：未使用のパラメータをエラーとする
- `--noImplicitReturns`：関数の戻り値がない場合をエラーとする
- `--noFallthroughCasesInSwitch`：switch文のcase文の最後にbreakがない場合をエラーとする
- `--allowJs`：JavaScriptファイルをコンパイルする
- `--checkJs`：JavaScriptファイルの型チェックを有効にする
- `--jsx`：JSXの使用を許可する
- `--experimentalDecorators`：デコレータを有効にする
- `--emitDecoratorMetadata`：デコレータのメタデータを出力する
- `--noEmit`：コンパイル結果を出力しない
- `--importHelpers`：ヘルパー関数をインポートする
- `--noEmitHelpers`：ヘルパー関数を出力しない
- `--newLine`：改行コードを指定
- `--locale`：メッセージの言語を指定
- `--listFiles`：コンパイル対象のファイルを表示
- `--pretty`：コンパイル結果を整形
- `--noErrorTruncation`：エラーメッセージを切り詰めない
- `--diagnostics`：エラー発生時に詳細な情報を表示
- `--traceResolution`：モジュールの解決過程を表示
- `--allowUnusedLabels`：未使用のラベルを許可する
- `--allowUnreachableCode`：到達不可能なコードを許可する
- `--noImplicitUseStrict`：暗黙的なstrictモードを許可しない
- `--noLib`：組み込みの型定義ファイルを使用しない
- `--preserveConstEnums`：const enumを出力する
- `--stripInternal`：@internalを削除する
- `--noResolve`：型チェック時に参照解決を行わない
- `--allowSyntheticDefaultImports`：default importを許可する
- `--declarationDir`：型定義ファイルの出力先を指定

