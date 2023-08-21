# ミックスイン

## ミックスインの命名のコツ
- 前提として、どのような機能が盛り込まれているか一目でわかるようにする
- そのために、最小限の機能に絞る
- 命名のポイント
    - 動詞 + able

```js
// mixin.js

export default {
  data() {
    return {
      message: 'Hello, World!'
    }
  },
  methods: {
    reverseMessage() {
      this.message = this.message.split('').reverse().join('')
    }
  }
}
```

```js
// main.js

import Vue from 'vue'
import App from './App.vue'
import mixin from './mixin'


// グローバルミックスイン
Vue.mixin(mixin)

new Vue({
  el: '#app',
  render: h => h(App)
})

// ローカルミックスイン
new Vue({
  el: '#app',
  render: h => h(App),
  mixins: [mixin]
})
```
