### v-bindの省略記法
- v-bindディレクティブは、v-bind:属性名の省略記法がある
- v-bindの省略記法の書式
    - :属性名="データのキー"
- v-bindの省略記法のサンプルコード
```html
<div id="app">
  <a :href="url">Google</a>
</div>

<script>
const vm = new Vue({
  data: {
    url: 'https://www.google.com/'
  },
}) $mount('#app')
</script>
```

#### 属性値での値の展開
- v-bindディレクティブを使うと、属性値にVueインスタンスのデータを展開できる
- v-bindディレクティブの書式
    - v-bind:属性名="データのキー"
- v-bindディレクティブのサンプルコード
```html
<div id="app">
  <a v-bind:href="url">Google</a>
</div>

<script>
const vm = new Vue({
  data: {
    url: 'https://www.google.com/'
  },
}) $mount('#app')
</script>
```