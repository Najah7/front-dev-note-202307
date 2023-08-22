## router v.s. $route
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