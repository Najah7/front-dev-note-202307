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