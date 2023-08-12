## 算出プロパティ
- 算出プロパティは、算出プロパティの値を算出するためのテンプレート構文
- thisでVueインスタンスのデータにアクセスできる
- 算出プロパティの書式
    - computed: {
        算出プロパティ名: function() {
            // 算出プロパティの値を算出する処理
            return 算出プロパティの値
        }
    }
- 算出プロパティのサンプルコード
```html
<div id="app">
  <p>{{ fullName }}</p>
</div>

<script>
const vm = new Vue({
  data: {
    firstName: 'Taro',
    lastName: 'Yamada'
  },
  computed: {
    fullName: function() {
      return this.firstName + ' ' + this.lastName
    }
  }
}) $mount('#app')
```

## 算出プロパティ v.s.　メソッド
- 算出プロパティ
  - 依存しているデータが変更されない限り、一度計算した結果をキャッシュする
  - メソッドが呼び出されるたびに計算される