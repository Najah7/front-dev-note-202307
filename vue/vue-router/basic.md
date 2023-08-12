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

## `<router-view>`コンポーネント
- ルートにマッチしたコンポーネントを描画するためのコンポーネント
- ルートにマッチしたコンポーネントは、`<router-view>`コンポーネントの位置に描画される

```html
<div id="app">
    <router-view></router-view>
</div>

<script>
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
</script>
```

## URLパラメータの扱いとパターンマッチング
- URLパラメータを扱うには、`:`を使う
- 「*」を使用することも可能。
- パターンマッチングは、`/`で区切られたURLのセグメントごとに行われる
- パターンマッチングの結果は、`$route.params`で取得できる

```html
<div id="app">
    <router-view></router-view>
</div>

<script>
const router = new VueRouter({
    routes: [
        {
            path: "/someurl/:id",
            component: {
                template: "<div>someurl</div>"
            }
        }
    ]
});

const app = new Vue({
    router: router
}).$mount("#app");

console.log(app.$route.params.id);
</script>
```

## 複数のパラメータの場合
```html
<div id="app">
    <router-view></router-view>
</div>

<script>
const router = new VueRouter({
    routes: [
        {
            path: "/someurl/:id/:name",
            component: {
                template: "<div>someurl</div>"
            }
        }
    ]
});

const app = new Vue({
    router: router
}).$mount("#app");

console.log(app.$route.params.id);
console.log(app.$route.params.name);
</script>
```

## 名前付きルート
- 名前付きルートを使うと、URLパラメータの値を直接指定することができる

```html
<div id="app">
    <router-link to="{ name: 'someurl', params: { id: 1, name: 'hoge' } }"></router-link>
</div>

<script>
const router = new VueRouter({
    routes: [
        {
            path: "/someurl/:id/:name",
            name: "someurl",
            component: {
                template: "<div>someurl</div>"
            }
        }
    ]
});

const app = new Vue({
    router: router
}).$mount("#app");

console.log(app.$route.params.id);
console.log(app.$route.params.name);
</script>
```

## router.pushを使った遷移
- `router.push`を使うと、ルーターの遷移を行うことができる
- `router.push`の引数には、`{ name: 'ルート名', params: { パラメータ名: 値 } }`の形式で指定する

```html
<div id="app">
    <router-view></router-view>
</div>

<script>
const router = new VueRouter({
    routes: [
        {
            path: "/someurl/:id/:name",
            name: "someurl",
            component: {
                template: "<div>someurl</div>"
            }
        }
    ]
});

const app = new Vue({
    router: router
}).$mount("#app");

router.push({ name: "someurl", params: { id: 1, name: "hoge" } });
</script>
```

## フック関数
- ページ遷移の前後に実行される関数
- フック関数の種類
    - グローバルのフック関数
    - ルート単位のフック関数
    - コンポーネント内のフック関数

###　router.beforEach
- グローバルのフック関数
- ページ遷移の前に実行される関数
- 引数
    - to: 遷移先のルート
    - from: 遷移元のルート
    - next: 遷移処理を完了するための関数
        - next()を呼び出すと、遷移処理が完了する
        - next(false)を呼び出すと、遷移処理がキャンセルされる
        - next(ルート名)を呼び出すと、指定したルートに遷移する

```html
<div id="app">
    <router-view></router-view>
</div>

<script>
const router = new VueRouter({
    routes: [
        {
            path: "/someurl/:id/:name",
            name: "someurl",
            component: {
                template: "<div>someurl</div>"
            }
        }
    ]
});

router.beforeEach((to, from, next) => {
    if (to.params.id === "1") {
        next("/someurl");
    } else {
        next(false);
    }
});

const app = new Vue({
    router: router
}).$mount("#app");

router.push({ name: "someurl", params: { id: 1, name: "hoge" } });
</script>
```

### router.beforeRouteEnter
- ルート単位のフック関数
- ページ遷移の前に実行される関数

```html
<div id="app">
    <router-view></router-view>
</div>

<script>
const router = new VueRouter({
    routes: [
        {
            path: "/someurl/:id/:name",
            name: "someurl",
            component: {
                template: "<div>someurl</div>",
                beforeRouteEnter(to, from, next) {
                    if (to.query.redirect === 'true') {
                        next('/someurl');
                    } else {
                        next();
                    }
                }
            }
        }
    ]
});

const app = new Vue({
    router: router
}).$mount("#app");

router.push({ name: "someurl", params: { id: 1, name: "hoge" } });
</script>
```

### コンポーネント内のフック関数
- コンポーネント内で定義するフック関数

```html
<div id="app">
    <router-view></router-view>
</div>

<script>
    var vm = {
        template: "<div>someurl</div>",
        data: function() {
            return {
                id: 0,
                name: ""
            };
        },
        beforeRouteEnter(to, from, next) {
            if (to.query.redirect === 'true') {
                next('/someurl');
            } else {
                next();
            }
        }
    };
</script>
```

## $router v.s. $route
- $router
    - Vue Routerのインスタンス
    - 1つのアプリケーションにつき1つのインスタンスを持つ
    - ルーターの遷移処理を行うためのメソッドを持つ
    - アプリ全体の履歴などは$routerで管理する
- $route
    - 現在のルートの情報を持つ
    - ルーティングが発生するごとに生成される。
    - 現在アクティブなルートの情報を持つ
    - Routerオブジェクト
    - ルートのパスやパラメータなどの情報を持つ
    - $route.paramsでURLパラメータの値を取得できる

## $router v.s. $routeのまとめ

### Routerインスタンス
| プロパティ / メソッド | 説明 |
| --- | --- |
| app | ルーターが使用されているrootのVueインスタンス |
| mode | ルーターのモード |
| currentRoute | 現在のルートのルート情報 |
| beforeEach | ページ遷移の前に実行される関数 |
| afterEach | ページ遷移の後に実行される関数 |
| push | ページ遷移を行うメソッド |
| replace | ページ遷移を行うメソッド(historyスタックに新しいエントリは追加されない) |
| go(n) | historyスタックをnステップ進めるか、もしくは、戻るのかを表す１つのintergerをnとしてとる |
| back | historyスタックを１つ戻す |
| forward | historyスタックを１つ進める |
| addRoutes(routes) | ルートを動的に追加する |

### Routeオブジェクト
| プロパティ / メソッド | 説明 |
| --- | --- |
| path |　現在のルートのパス |
| params | 現在のルートのパラメータ(key/valueのペア) |
| query | 現在のルートのクエリパラメータ(key/valueのペア) |
| hash | 現在のルートのハッシュ（URLに#がある時点の源氏アのルートハッシュを取得できる） |
| fullPath | 現在のルートのフルパス |
| name | 現在のルートの名前 |

## リダイレクト
- リダイレクトは、ルートのパスを別のパスに変更すること
- リダイレクトの設定方法
    - ルートオブジェクトのredirectプロパティにリダイレクト先のパスを指定する
    - ルートオブジェクトのredirectプロパティに関数を指定する
    - ルートオブジェクトのredirectプロパティにオブジェクトを指定する
```html
<div id="app">
    <router-view></router-view>
</div>

<script>
const router = new VueRouter({
    routes: [
        {
            path: "/someurl/:id/:name",
            name: "someurl",
            component: {
                template: "<div>someurl</div>",
                redirect: "/someurl"
            }
        }
    ]
});

const app = new Vue({
    router: router
}).$mount("#app");

router.push({ name: "someurl", params: { id: 1, name: "hoge" } });

// リダイレクト先を動的に変更する場合
router.push({ name: "someurl", params: { id: 1, name: "hoge" }, query: { redirect: true } });
</script>
```

## エイリアス
- エイリアスは、ルートのパスを別のパスに変更すること
- パスは変わらないが、コンポーネントを変更することができる
- エイリアスの設定方法
    - ルートオブジェクトのaliasプロパティにエイリアス先のパスを指定する
    - ルートオブジェクトのaliasプロパティに関数を指定する
    - ルートオブジェクトのaliasプロパティにオブジェクトを指定する
```html
<div id="app">
    <router-view></router-view>
</div>

<script>
const router = new VueRouter({
    routes: [
        {
            path: "/someurl/:id/:name",
            name: "someurl",
            component: {
                template: "<div>someurl</div>",
                alias: "/someurl"
            }
        }
    ]
});

const app = new Vue({
    router: router
}).$mount("#app");

router.push({ name: "someurl", params: { id: 1, name: "hoge" } });
</script>
```

## 履歴管理
- やり方
    - URL Hash
    - HTML5 History API