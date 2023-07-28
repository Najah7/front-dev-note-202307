# Reactを用いたモダン開発で使うツールや技術

## React Hooks
- React Hooksとは
    - React Hooksとは、関数コンポーネントで状態管理やライフサイクルを扱うための仕組み。
    - React Hooksのメリット
        - クラスコンポーネントよりもシンプルに書ける
        - コンポーネントの再利用性が高まる
        - コンポーネントのテストが容易になる
        - ライフサイクルメソッドの代替が可能
    - 代表的なReact Hooks
        - useState()
        - useEffect()
        - useContext()
        - useReducer()
        - useCallback()
        - useMemo()
        - useRef()
        - useImperativeHandle()
        - useLayoutEffect()
        - useDebugValue()

## Redux
- Reduxとは
    - Reduxとは、Reactアプリケーションの状態管理を行うためのライブラリ。
    - Reduxのメリット
        - コンポーネントの再利用性が高まる
        - コンポーネントのテストが容易になる
        - ライフサイクルメソッドの代替が可能
    - Reduxの概念
        - Store：アプリケーションの状態を保持する場所
        - Action：Storeに対して、どのような処理を行うかを伝えるためのオブジェクト
        - Reducer：Actionを受け取り、Storeの状態をどのように変更するかを定義する関数
        - Dispatch：ActionをReducerに送るための関数
        - Selector：Storeの状態を取得するための関数
    - Reduxの実装
        - Storeの作成
        - Actionの作成
        - Reducerの作成
        - Dispatchの作成
        - Selectorの作成
    - ReduxのHooks
        - useSelector()
        - useDispatch()
        - useStore()
        - useAction()
        - useReducer()

## Storybook
- Storybookとは
    - Storybookとは、UIコンポーネントの開発・テスト・ドキュメント作成を行うためのツール。
    - コンポーネントをカタログ化して、開発できるツール。
    - Storybookのメリット
        - コンポーネントのUIの確認が容易になる
        - 開発者間の分業が容易になる
        - デザイナーと共通認識をとりやすい
        - コンポーネントに渡す値を動的に変更し、振る舞いを確認できる
        - コンポーネントの再利用性が高まる
        - コンポーネントのテストが容易になる
        - ライフサイクルメソッドの代替が可能
    - Storybookの実装
        - Storybookのインストール：`npx sb init`
        - Storybookの設定
        - Storybookの実行
        - Storybookのコンポーネント作成
        - Storybookのコンポーネントのテスト
        - Storybookのコンポーネントのドキュメント作成
- [参考Youtube](https://www.youtube.com/watch?v=S4JgdSGsEQw)


## CommonJSとESモジュール

両方がモジュールの使用。<br>
CommonJSが先。<br>
ESモジュールは、CommonJSの欠点を解決するために作られた。<br>
なので、現在ではESモジュールが主流。<br>

- CommonJS
    - Node.jsのモジュールシステム
    - ブラウザでは動作しない
    - モジュールの読み込み
        - require関数
    - モジュールのエクスポート
        - module.exportsオブジェクト
- ESモジュール
    - ES2015で導入されたモジュールシステム
    - ブラウザでも動作する
    - モジュールの読み込み
        - import文
    - モジュールのエクスポート
        - export文

### 上記が解決しようとした問題
- モジュール機構がない
- 標準ライブラリがない
- Webサーバーやデータベースとの標準的なインターフェースがない
- パッケージのマネジメントシステムがない

## Deno
JavaScriptとTypeScriptの実行環境。<br>
Node.jsの開発者が作成。<br>
Node.jsの欠点を解決するために作られた。<br>

### Node.jsとの違い
- ファイルやネットワークアクセスなどは明示的に宣言した場合のみ許可される
- TypeScriptをネイティブでサポート
- モジュール依存管理npmとpakage.jsonの廃止
- ESモジュール形式でURLを指定しimportを行い、実行時のモジュール管理が行われる
- 実行環境は単一のバイナリファイルとして提供されている

## Babel
ES2015以降のコードをES5に変換するツール。<br>

## ビルドツールとタスクランナー
- ビルドシステム：ソースコード上で読み込んでいるモジュールの依存を解決し、実行可能なJavaScriptの形式に変換する仕組み。これによりサーバサイドとクライアントサイドで同じコードを使えるように。
- タスクランナー：ビルドシステムを実行するためのツール。ビルドシステムを実行するためのタスクを登録しておき、それを実行するためのツール。
しかし、学習コストがかかるため、あまり使われなくなり、npmのスクリプトによるコマンド実行を利用する方針に置き換えられた
 - 代表的なビルドランナー
    - Grunt
    - Gulp

## Webpack
- モジュールバンドラー
    - モジュールをまとめて1つのファイルにする
    - モジュールの依存関係を解決する
    - モジュールを変換する
- Webpackのメリット
    - 利用しているモジュールのバージョン管理と解決を自動化
    - ファイルの結合やコードの圧縮などを自動化
    - プラグイン機構によりさまざまなカスタマイズができる
    - ホットリロードなどの開発効率化ツールを同梱している