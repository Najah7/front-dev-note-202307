## Vueインスタンスのマウント
- Vueインスタンスをマウントすると、VueインスタンスのテンプレートがDOM要素に描画される
- Vueインスタンスのマウント方法
    - コンストラクタのelオプションでマウントする
    - $mount()メソッドでマウントする

### elオプションでマウントするサンプルコード
```html
<div id="app">
  {{ message }}
</div>

<script>
const vm = new Vue({
  el: '#app',
  data: {
    message: 'Hello, Vue.js!'
  }
})
</script>
```

### $mount()メソッドでマウントするサンプルコード
```html
<div id="app">
  {{ message }}
</div>

<script>
const vm = new Vue({
  data: {
    message: 'Hello, Vue.js!'
  }
}) $mount('#app')
</script>
```