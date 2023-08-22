# v-cloak
- v-cloakディレクティブは、Vueインスタンスがマウントされるまで要素を非表示にする

## v-cloakディレクティブのサンプルコード
```html
<style>
[v-cloak] {
  display: none;
  /* you can also use other CSS attributes to hide the element */
}

<div id="app">
  <p v-cloak>{{ message }}</p>
</div>

<script>
const vm = new Vue({
  data: {
    message: 'Hello, Vue.js!'
  },
}) $mount('#app')
</script>
```