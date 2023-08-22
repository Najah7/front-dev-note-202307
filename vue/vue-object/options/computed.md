## 算出プロパティ
- 算出プロパティは、テンプレート内で使用するデータを算出するためのプロパティ
  - 算出プロパティ：値の更新を監視し、値が変更されたときに自動的に再計算される
- 子要素にdataを渡すとまずい時に使う使い方もよく使う
  - 子要素に親要素の値を渡して、子で書き換えるのは、ご法度。
  - しかし、親要素の関数を渡して、子要素で関数を実行して、親要素の値を書き換えるのはOK
- thisでVueインスタンスのデータにアクセスできる
- 算出プロパティの書式
    - computed: {
        算出プロパティ名: {
          get: function() {
            // 算出した値を返す
          },
          set: function(newValue) {
            // 値が変更されたときに呼ばれる
          }
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
    fullName: {
      get: function() {
        return this.firstName + ' ' + this.lastName
      },
      set: function(newValue) {
        const names = newValue.split(' ')
        this.firstName = names[0]
        this.lastName = names[names.length - 1]
      }
    }
  }
}) $mount('#app')
```

## 算出プロパティ v.s.　メソッド
- 算出プロパティ
  - 依存しているデータが変更されない限り、一度計算した結果をキャッシュする
  - メソッドが呼び出されるたびに計算される
- メソッド
  - 依存しているデータが変更されなくても、メソッドが呼び出されるたびに計算される