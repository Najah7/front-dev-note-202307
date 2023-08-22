## UIのデータの定義
- Vue.jsでは、UIのデータをdataオプションで定義する
- dataオプションで定義したデータは、Vueインスタンスのdataプロパティから参照できる

### dataオプションのサンプルコード
```html
<div id="app">
  {{ message }}
</div>

<script>
const vm = new Vue({
  data: {
    キー: 値
  }
}) $mount('#app')
</script>
```