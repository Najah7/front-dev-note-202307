## リストレンダリング

### v-forディレクティブ
- v-forディレクティブは、配列の要素分繰り返し要素を表示するためのテンプレート構文
- v-forディレクティブの書式
    - `v-for="要素" in 配列"`
    - `v-for="(要素, インデックス) in 配列"`
    - `v-for="(値, キー) in オブジェクト"`
    - `v-for="(値, キー, インデックス) in オブジェクト"`
- v-forディレクティブのサンプルコード
```html
<div id="app">
  <ul>
    <li v-for="item in list">{{ item }}</li>
  </ul>
</div>

<script>
const vm = new Vue({
  data: {
    list: ['りんご', 'ばなな', 'いちご']
  },
}) $mount('#app')
</script>
```