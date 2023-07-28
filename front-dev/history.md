# 前提知識
1. JQuery
    - 人気が出た理由
        - クロスブラウザ互換を実現
        - DOM操作を簡単に実現
        - アニメーションを簡単に実現
        - JQuery UIを利用することで、UIを簡単に実現
    - 人気が下がった理由
    - グローバルスコープを汚染する
    - DOM操作の実装が複雑になりやすい
    - ルーティングなど、複数ページのWebアプリケーションを実装する仕組みがない
    - ブラウザ間の挙動の違いが少なくなった。
1. SPAとMVC/MVVMフレームワーク
    - SPA：Single Page Application
        - SPAを支える技術
            - URLパスとViewのルーティング機能
            - クライアントサイドでのブラウザ履歴管理によるページ遷移
            - 非同期によるデータの取得
            - Viewのレンダリング
            - モジュール化されたコードの管理
            - History API：ブラウザ履歴を操作するAPI（HTML5に導入された）
                - pushState：ブラウザ履歴に新しい履歴を追加する
                - replaceState：ブラウザ履歴の現在の履歴を置き換える
                - popstate：ブラウザ履歴の変更を検知する
        - メリット
            - ページ遷移をクライアントサイドで行う
            - Ajaxを利用して、サーバーからデータを取得する(HTMLを逐一渡すよりも、データのみをやり取りする方が軽い)
            - Ajaxによりクライアントとサーバーの役割を明確に分けることができる（バックエンドをネイティブアプリでも使える） 
        - デメリット
            - JSを読み込みレンダリングが発生するため、対策しない場合、初期表示に時間がかかる
            - フロントエンドの学習コスト増加
            - フロントエンドのコード量増加
            - 経験のある人材の採用が難しい
    - MVC/MVVMフレームワーク
        - MVC：Model View Controller
            - Model：データを管理する
            - View：ユーザーインターフェースを管理する
            - Controller：ModelとViewの間を仲介する
            - ex) backbone.js, Ember.js
        - MVVM：Model View ViewModel
            - Model：データを管理する
            - View：ユーザーインターフェースを管理する
            - ViewModel：ModelとViewの間を仲介する
            - ex) Knockout.js, Vue.js, AngularJS
1. Reactの登場
- React
    - コンポーネント指向・関数コンポーネント
    - 状態管理
    - 仮想DOM：ノードが変更があった場合、変更前後の仮想DOMを比較して変更箇所を特定し、必要におじてまとめて実際のDOMに反映する
    -宣言的UI
    - 単一方向のデータフロー
    - Fluxアーキテクチャとの親和性
        - Flux
            -　単一方向のデータフロー
            - 状態管理をわかりやすくするためにある
                1. Action
                1. Dispatcher
                1. Store
                1. View
                1. Action
                1. Dispatcher
                1. Store
                1. View ...
    - Redux：Fluxを発展的に継承したライブラリ
1. Node.jsの躍進
    - Node.js
        - サーバサイドでJSを実行できる環境
        - ノンブロッキングI/O（多くのリクエストを遅延が少なく処理できる）の特徴が注目された
    - npm
        - Node.jsのパッケージ管理ツール
        - 特徴
            - モジュール読み込みの機構
            - パッケージ管理
            - ビルドシステム
            - 技術スタックの統一
            - package.jsonで記述するだけで組み込むことが可能になっている
1. AltJsの流行とTypeScriptの定番化
    - AltJs
        - JSの代替言語
        - コンパイルすることでJSに変換する
        - 違う言語からJSに変換する発想。
        - 代表的な同じ思想の言語
            - CoffeeScript：コード量を減らす思想を持つAltJS
            - TypeScript：Microsoftが開発。静的型宣言が特徴
            - Dart：Googleが開発をリードしているAltJSとしても使える言語。Flutterで使われている
            - ClojureScript：Cloujureという関数型言語をJSに変換するAltJS
            - Elm：関数型言語。ReactのようなUIライブラリを持っている
            - PureScript：Haskellという関数型言語をJSに変換するAltJS
1. SSR/SSGの必要性
    - SSR：サーバーサイドレンダリング
        - サーバー側でHTMLを生成してからクライアントに返す
        - SRAの初期表時が遅い問題を解決するために登場
        - メリット
            - 初期表示が早い
            - SEO対策がしやすい
        - デメリット
            - サーバサイドJavaScriptのランタイムが必要
            - サーバーの負荷が高い（サーバでレンダリングするので）
            - サーバーとクライアントでJavaScriptのロジックが分散してしまう
    - SSG：静的サイトジェネレーター
        - ビルド時にHTMLを生成する
        - メリット
            - 初期表示が早い
            - SEO対策がしやすい
            - サーバーの負荷が低い(デプロイ時にHTMLを生成するので)
        - デメリット
            - ビルド時間が長い
            - ビルド時にサーバーが必要
            - ビルド時にサーバーの負荷が高い
1. Next.jsの登場と受容
- Next.js
    - Reactベースのモダンアプリを開発するためのフルスタックフレームワーク
    - SSR/SSGをサポート
    - SPA/SSR/SSGの切り替えが容易
    - 簡単なページルーティング
    - TypeScriptベース
    - 学習コストが低い
    - webpackの設定の隠蔽
    - ディレクトリベースの自動ルーティング
    - コードの分割・統合
    - SWC（Rustのコンパイラ）による高速ビルド
    - Next.js特徴
        - Reactの機能範囲
            - 宣言的UI
            - Virtual DOM
            - TypeScriptサポート
            - UIテスト
        - UI・コンポーネントの実装
            - ファイルシステムルーティング
            - APIルーティング
            - SSR/SSG
            - ISRによるビルド短縮
        - サーバサイドの実装
            - 環境変数
            - 高速リロード
            - ESLint
            - 簡易Webpackビルド
        - 開発環境サポート
            - IE11含むブラウザサポート
            - 画像最適化
            - フォント最適化
            - 国際化対応
            - Vercelへの簡易デプロイ



## Hydration（Reactコンポーネントの復元）
SSRされたHTMLをブラウザで読み込んだ際に、Reactコンポーネントに復元すること。<br>
静的→動的に戻すこと。<br>
ReactDOMの`hydrate()`を使う。<br>

### 注意点
- まず静的なHTMLを表示し、その後にJSを実行するので、HTML表示とJS実行のタイミングがずれる。<br>
