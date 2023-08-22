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