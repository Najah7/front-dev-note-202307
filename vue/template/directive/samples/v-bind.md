# v-bind
- 属性とdataをバインドするためのディレクティブ。
- 属性なので、styleやclassなどでよく使う。

### v-bindの省略記法
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