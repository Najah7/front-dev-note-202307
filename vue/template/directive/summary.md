# ディレクティブ
- ディレクティブは、HTML要素に対して特別な動作をさせるためのテンプレート構文
- Vueインスタンスをマウントした要素とその子孫でしか使えない

## 代表的なディレクティブ
|ディレクティブ名|説明|
|:--|:--|
|`v-if="条件式"` |条件式がtrueの場合に要素を表示する|
|`v-for="要素" in 配列"` |配列の要素分繰り返し要素を表示する|
|`v-bind="属性名"` |属性名にデータをバインドする|
|`v-on="イベント名"` |イベント名にイベントハンドラをバインドする|
|`v-model="データのキー"` |フォームの入力値をデータにバインドする|
|`v-show="条件式"` |条件式がtrueの場合に要素を表示する|
|`v-text="データのキー"` |データの値をテキストとして表示する|
|`v-html="データのキー"` |データの値をHTMLとして表示する|
|`v-cloak` |Vueインスタンスがマウントされるまで要素を非表示にする|

### v-vindの例
- `v-bind:class="{ クラス名: 条件式 }"`：条件式がtrueの場合にクラスを追加する👈算出プロパティに書くのが一般的
- `v-bind:style="{ スタイル名: データのキー }"`：データの値をスタイルの値として追加する

## ディレクティブのサンプルコード
```html
<div id="app">
  <p v-if="show">Hello, Vue.js!</p>
</div>

<script>
const vm = new Vue({
  data: {
    show: true
  },
}) $mount('#app')
</script>
```

## ディレクティブと三項演算子
- ディレクティブと三項演算子を組み合わせることで、条件によってディレクティブを切り替えることができる

#### ディレクティブと三項演算子のサンプルコード
```html
<div id="app">
  <p v-bind:class="isActive ? 'active' : ''">Hello, Vue.js!</p>
</div>

<script>
const vm = new Vue({
  data: {
    isActive: true
  },
}) $mount('#app')
</script>

<!-- 算出プロパティに配置 -->

<div id="app">
  <p v-bind:class="activeClass">Hello, Vue.js!</p>
</div>

<script>
const vm = new Vue({
  data: {
    isActive: true
  },
  computed: {
    activeClass: function() {
      return this.isActive ? 'active' : ''
    }
  }
}) $mount('#app')
</script>
```

※falseがいらない場合：`v-bind:class="isActive && 'active'"`