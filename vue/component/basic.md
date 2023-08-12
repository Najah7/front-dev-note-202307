# コンポーネント開発

## コンポーネント開発の利点
- 再利用性の向上により、開発効率の向上
- すでに使用されているコンポーネントを再利用することで品質を保てる
- コンポーネントを適切に区切り、疎結合にした場合、保守性が向上する
- カプセル化された開発で意識すべき範囲を限定できるようになる。

## コンポーネントの実装の仕方
- テンプレートベース
- コンストラクタベース

## コンポーネントの定義
- 定義方法
    - Vue.component()メソッドでのカスタムタグ方式（テンプレートベース）
    - Vue.extend()メソッドでのサブコンストラクタ方式（コンストラクタベース）

※カスタムタグのテンプレートベースの方が、コンストラクタベースよりも一般的で、おススメ。<br>理由は、HTML内で使えわかりやすいから。


## Web Components
- UIコンポーネンの標準化を目指す仕様
- 開発者が新たに再利用可能なHTML要素を定義できるようにする一連のAPI。
- Web Componentsは単一APIではなく、仕様策定中のウェブプラットフォームAPI群
- Web Componentsはすべてのブラウザに実装されているわけではない。
- Web Componentsの基になる4つの仕様
    - Custom Elements：独自のHTML要素を定義するための仕様
    - Shadow DOM：DOMツリーの階層を分離するための仕様
    - HTML Templates：HTMLのテンプレートを定義するための仕様
    - HTML Imports：HTMLのインポートを定義するための仕様



## Vue.componentのオプション一覧
| オプション名 | 説明 |
|:--|:--|
| data | UIの状態・データを定義する |
| props | 親コンポーネントから受け取るデータを定義する |
| computed | 算出プロパティを定義する |
| methods | メソッドを定義する |
| watch | ウォッチャを定義する |
|filters | フィルタを定義する |
| template | テンプレートを定義する |
| create ...etc | ライフサイクルフックを定義する |

## Vueでのコンポーネントの定義方法
- Vue.component()メソッドでコンポーネントを定義する
- Vue.component()メソッドの第1引数にコンポーネント名、第2引数にコンポーネントのオプションを指定する
- コンポーネント名は、ケバブケースで指定する
- コンポーネントのオプションは、Vueインスタンスのオプションと同じものを指定できる
- コンポーネントのオプションのdataは、関数で定義する
- コンポーネントのオプションのtemplateは、テンプレート構文で定義する
- コンポーネントのオプションのmethodsは、メソッドを定義する
- コンポーネントのオプションのpropsは、親コンポーネントから受け取るデータを定義する
- コンポーネントのオプションのpropsは、配列かオブジェクトで定義する
- コンポーネントのオプションのpropsは、オブジェクトで定義する場合、キーに受け取るデータの名前、値にデータの型を指定する
- コンポーネントのオプションのpropsは、オブジェクトで定義する場合、値にデータの型を指定すると、データの型が正しくない場合に警告が表示される

```html
<div id="app">
  <my-component></my-component>
</div>

<script>
Vue.component('my-component', {
  data: function() {
    return {
      message: 'Hello, Vue.js!'
    }
  },
  template: '<p>{{ message }}</p>',
  methods: {
    clickHandler: function(event) {
      alert(event.target)
    }
  },
  props: {
    propA: Number,
    propB: [String, Number],
    propC: {
      type: String,
      required: true
    },
    propD: {
      type: Number,
      default: 100
    },
    propE: {
      type: Object,
      default: function() {
        return { message: 'hello' }
      }
    },
    propF: {
      validator: function(value) {
        return value > 10
      }
    }
  }
})

new Vue({
  el: '#app'
})
</script>
```

## Vue.extend()メソッドでコンポーネントを定義する
- Vue.extend()メソッドでコンポーネントを定義する
- Vue.extend()メソッドの戻り値は、Vueコンストラクタ
- Vue.extend()メソッドの戻り値をnew演算子でインスタンス化すると、Vueインスタンスが生成される
- Vue.extend()メソッドの戻り値をnew演算子でインスタンス化すると、Vueインスタンスのオプションは、Vue.extend()メソッドの引数に指定したオプションとマージされる

```html
<div id="app">
  <my-component></my-component>
</div>

<script>
const MyComponent = Vue.extend({
  data: function() {
    return {
      message: 'Hello, Vue.js!'
    }
  },
  template: '<p>{{ message }}</p>',
  methods: {
    clickHandler: function(event) {
      alert(event.target)
    }
  },
  props: {
    propA: Number,
    propB: [String, Number],
    propC: {
      type: String,
      required: true
    },
    propD: {
      type: Number,
      default: 100
    },
    propE: {
      type: Object,
      default: function() {
        return { message: 'hello' }
      }
    },
    propF: {
      validator: function(value) {
        return value > 10
      }
    }
  }
})
```

## ローカルコンポーネントの定義
- Vueインスタンスのcomponentsオプションでローカルコンポーネントを定義する
- ローカルコンポーネントは、定義したVueインスタンス内でのみ使用できる

```html
<div id="app">
  <my-component></my-component>
</div>

<script>
new Vue({
  el: '#app',
  components: {
    'my-component': {
      data: function() {
        return {
          message: 'Hello, Vue.js!'
        }
      },
      template: '<p>{{ message }}</p>',
      methods: {
        clickHandler: function(event) {
          alert(event.target)
        }
      },
      props: {
        propA: Number,
        propB: [String, Number],
        propC: {
          type: String,
          required: true
        },
        propD: {
          type: Number,
          default: 100
        },
        propE: {
          type: Object,
          default: function() {
            return { message: 'hello' }
          }
        },
        propF: {
          validator: function(value) {
            return value > 10
          }
        }
      }
    }
  }
})
</script>
```

## テンプレートを構築するその他の手段
- text/x-templateスクリプトタグを使う
- 描画関数
- 単一ファイルコンポーネント
- インラインテンプレート
- JSX


## コンポーネント間のデータのやりとり
- 親コンポーネントから子コンポーネントへのデータの受け渡し
    - propsをで渡す
    - propsオプションを使う
    - propsオプションは、配列かオブジェクトで定義する
- 子コンポーネントから親コンポーネントへのデータの受け渡し
    - eventを渡す
    - $on()：イベントのlisten。カスタムイベントをlistenする
    - $emit()：イベントのtrigger。カスタムイベントを発火する
    
## Propsとイベントを用いない親子間のやりとり
- どうしてもの時の切り札。普通は使うべきではない。
- $parentと$childrenを使う
    - $parent：親コンポーネントのインスタンスを参照する
    - $children：子コンポーネントのインスタンスを参照する
    - ref：子コンポーネントのインスタンスを参照する

## 子から親のネイティブDOMイベントを取得したい場合
- .native修飾子を使う
- .native修飾子を使うと、子コンポーネントのルート要素で発生したイベントを親コンポーネントでlistenできるようになる

## propsの値に関して、双方向バインディングを実現したい場合
- .sync修飾子を使う
- .sync修飾子を使うと、propsの値を子コンポーネントで変更した場合に、親コンポーネントのデータも変更されるようになる


