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