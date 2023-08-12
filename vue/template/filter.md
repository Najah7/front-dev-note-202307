### フィルタ
- フィルタは、マスタッシュ構文やディレクティブの値に対して、特別な加工を行うためのテンプレート構文
- フィルタの書式
    - データのキー | フィルタ名
- フィルタのサンプルコード
```html
<div id="app">
  {{ 値 | フィルタ名 }}
</div>

<script>
const vm = new Vue({
  data: {
    message: 'Hello, Vue.js!'
  },
  filters: {
    フィルタ名: function(値) {
      // 値を加工する処理
      return 加工した値
    }
  }
}) $mount('#app')
</script>
```

#### フィルタのチェーン
- フィルタは、複数のフィルタをチェーンさせることができる
- フィルタのチェーンの書式
    - データのキー | フィルタ名1 | フィルタ名2
- フィルタのチェーンのサンプルコード
```html
<div id="app">
  {{ message | filterA | filterB }}
</div>

<script>
const vm = new Vue({
  data: {
    message: 'Hello, Vue.js!'
  },
  filters: {
    filterA: function(値) {
      // 値を加工する処理
      return 加工した値
    },
    filterB: function(値) {
      // 値を加工する処理
      return 加工した値
    }
  }
}) $mount('#app')
</script>
```