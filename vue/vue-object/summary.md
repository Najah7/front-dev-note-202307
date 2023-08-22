# Vueオブジェクト
- Vue.jsでは、Vueオブジェクトを使って、Vueインスタンスを生成する
- しかし、あまり使わない。Vueコンポーネントを使うことが多い。

## Vueオブジェクトの作成
- `new Vue()`でVueオブジェクトを作成する
- `Vue.createApp()`でVueオブジェクトを作成する

# コンストラクタの概要
- オブジェクトを生成するための関数
- new演算子を使って呼び出す
- Vue.jsでは、コンストラクタを使ってVueインスタンスを生成する(Vue2.0以降)

## 特に大事なオプション
- data
- methods
- computed
- watch
- template

※後は、ライフサイクル系も大事

## コンストラクタのオプション
| オプション名 | 説明 |　型 | デフォルト値 |
|:--|:--|:--|:--|
| el | Vueインスタンスを紐付けるDOM要素のCSSセレクタ | string | - |
| data() | テンプレートで利用するデータ | Object | - |
| methods | テンプレートで利用するメソッド | Object | - |
| computed | テンプレートで利用する算出プロパティ | Object | - |
| watch | 監視対象のプロパティとその変更時に呼び出すハンドラ | Object | - |
| template | テンプレート | string | - |
| render | テンプレートの代わりに描画する関数 | Function | - |
| renderError | 描画中にエラーが発生した時に呼び出す関数 | Function | - |
| beforeCreate | Vueインスタンスが生成された後、データの監視やイベントの購読が行われる前に呼び出される関数 | Function | - |
| created | Vueインスタンスが生成された後、データの監視やイベントの購読が行われた後に呼び出される関数 | Function | - |
| beforeMount | Vueインスタンスがマウントされる前に呼び出される関数 | Function | - |
| mounted | Vueインスタンスがマウントされた後に呼び出される関数 | Function | - |
| beforeUpdate | データが変更され、DOMに適用される前に呼び出される関数 | Function | - |
| updated | データが変更され、DOMに適用された後に呼び出される関数 | Function | - |
| beforeDestroy | Vueインスタンスが破棄される前に呼び出される関数 | Function | - |
| destroyed | Vueインスタンスが破棄された後に呼び出される関数 | Function | - |
| activated | keep-aliveでキャッシュされたコンポーネントがアクティブになった時に呼び出される関数 | Function | - |
| deactivated | keep-aliveでキャッシュされたコンポーネントが非アクティブになった時に呼び出される関数 | Function | - |
| errorCaptured | 子孫コンポーネントでエラーが発生した時に呼び出される関数 | Function | - |
| directives | テンプレートで利用するディレクティブ | Object | - |
| components | テンプレートで利用するコンポーネント | Object | - |
| parent | Vueインスタンスの親となるVueインスタンス | Vueインスタンス | - |
| mixins | テンプレートで利用するミックスイン | Array | - |
| name | Vueインスタンスの名前 | string | - |
| delimiters | テンプレートの区切り文字 | Array | ['{{', '}}'] |
| functional | 関数型コンポーネントとして扱うかどうか | boolean | false |
| model | v-modelディレクティブのオプション | Object | - |
| inheritAttrs | 親コンポーネントからの属性の継承方法 | boolean | true |
| comments | コンポーネントのルート要素のコメントを有効にするかどうか | boolean | false |
| provide | injectオプションで注入する値を設定するオプション | Object | - |
| inject | 親コンポーネントから注入する値を設定するオプション | Object | - |
| model | v-modelディレクティブのオプション | Object | - |

## コンストラクタのオプションのサンプルコード
```ts
const vm = new Vue({
  el: '#app',
  data: {
    message: 'Hello, Vue.js!'
  },
  methods: {
    reverseMessage() {
      this.message = this.message.split('').reverse().join('')
    }
  },
  computed: {
    computedMessage() {
      return this.message.split('').reverse().join('')
    }
  },
  watch: {
    message(newValue, oldValue) {
      console.log(`new: ${newValue}, old: ${oldValue}`)
    }
  }
})
```