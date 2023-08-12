## watchオプション
- watchオプションで監視対象のプロパティとその変更時に呼び出すハンドラを定義できる
- watchオプションで定義したハンドラは、Vueインスタンスのwatchプロパティから参照できる
- 引数
    - 第１引数: 監視対象の値を返す関数
    - 第2引数：値が変わった場合に呼び出されるコールバック関数<br>
※オプションで指定することでコールバック関数のみを定義できる

### watchオプションのサンプルコード
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

vm.$watch(
  function() {
    return this.message
  },
  function(newValue, oldValue) {
    console.log(`new: ${newValue}, old: ${oldValue}`)
  }
)
</script>
```