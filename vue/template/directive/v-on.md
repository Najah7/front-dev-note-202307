## イベントハンドリング
- イベントハンドリングは、イベントが発生した時に呼び出される関数
- イベントハンドリングの書式
    - v-on:イベント名="イベントハンドラ"
    - @イベント名="イベントハンドラ"
- `$event`は、イベントオブジェクトを参照するための特別な変数。Vue.jsによって提供されている
- v-onの省略記法
    - v-on:イベント名の省略記法
        - v-on:click="handleClick" → @click="handleClick"
- イベントハンドリングのサンプルコード
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