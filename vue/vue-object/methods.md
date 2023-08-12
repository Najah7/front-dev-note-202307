# methods
- テンプレートで利用するメソッド
- メソッドの書式
    - methodsオプションにメソッドを定義する
    - メソッド名: 関数

## メソッドのサンプルコード
```html
<div id="app">
  <button v-on:click="handleClick">ボタン</button>
</div>

<script>
const vm = new Vue({
  methods: {
    handleClick: function(event) {
      // イベントハンドラの処理
    }
  }
}) $mount('#app')
</script>
```


## 算出プロパティ v.s.　メソッド
- 算出プロパティ
  - 依存しているデータが変更されない限り、一度計算した結果をキャッシュする
  - メソッドが呼び出されるたびに計算される