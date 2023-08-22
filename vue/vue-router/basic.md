# Vue Router
- Vue.jsの公式のプラグインのルータ。
- SPA構築のために用いるルーティングライブラリ。
- URLごとに特定のコンポーネントを出し分ける、表示を変えるといったページ遷移を実現するための動作が可能になる。

## SPA実装時の考慮点
- クライアントサイドでの履歴管理なども含めたページ遷移
- 非同期通信によるデータの取得
- Viewのレンダリング
- モジュール化されたコードの管理

## Vue Routerで実現できること
- ネストしたルーティング
- リダイレクトとエイリアス
- HTML5 History APIとURL Hashによる履歴管理（IE9での自動的なフォールバックも可能）
- 自動的にCSSクラスがアクティブになるリンクの仕組み
- Vue.jsのトランザクションの仕組みを使ったページ遷移時のトランザクション
- スクロールの振る舞いのカスタム

## Routerのインストール
- CDNを使う場合
    - https://router.vuejs.org/installation.html 👈公式のVue RouterのWebページ
- npmを使う場合
    - `npm install vue-router`

## Routerを実装するにあたっての構成要素
- ルート：URLとViewの情報を保持する１つのレコード
- ルーターコンストラクタ

## ルートの定義
```ts
{
    path: "/someurl",
    component: {
        template: "<div>someurl</div>"
    }
}
```

## ルーターをコンポーネントに組み込む
- Vue Routerのインスタンスを作成する
- Vue RouterのインスタンスをVueインスタンスに渡す
```ts
const router = new VueRouter({
    routes: [
        {
            path: "/someurl",
            component: {
                template: "<div>someurl</div>"
            }
        }
    ]
});

const app = new Vue({
    router: router
}).$mount("#app");
```
## 履歴管理
- やり方
    - URL Hash
    - HTML5 History API