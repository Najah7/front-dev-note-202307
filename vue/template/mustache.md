### マスタッシュ構文（Mustache Syntax）
- マスタッシュ構文は、データをHTMLに表示するためのテンプレート構文
- Mustache展開のJavaScript式は単一の式しか記述できない
- マスタッシュ構文の書式
    - {{ データのキー }}
- マスタッシュ構文のサンプルコード
```html
<div id="app">
  {{ message }}
</div>

<script>
const vm = new Vue({
  data: {
    message: 'Hello, Vue.js!'
  },
}) $mount('#app')
</script>
```