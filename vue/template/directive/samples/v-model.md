## フォーム入力バインディング
- フォーム入力バインディングは、フォームの入力値をデータ（vue objectのdata）にバインドするためのテンプレート構文
- フォーム入力バインディングの書式
    - v-model="データのキー"
- フォーム入力バインディングのサンプルコード
```html
<div id="app">
  <input type="text" v-model="message">
  <p>{{ message }}</p>
</div>

<script>
const vm = new Vue({
  data: {
    message: 'Hello, Vue.js!'
  },
}) $mount('#app')
</script>
```