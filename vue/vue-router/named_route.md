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