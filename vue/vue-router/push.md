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