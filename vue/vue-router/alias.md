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