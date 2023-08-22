# コンポーネント開発

## コンポーネント開発の利点
- 再利用性の向上により、開発効率の向上
- すでに使用されているコンポーネントを再利用することで品質を保てる
- コンポーネントを適切に区切り、疎結合にした場合、保守性が向上する
- カプセル化された開発で意識すべき範囲を限定できるようになる。

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

## コンポーネントの実装の仕方
- テンプレートベース：Vue.component()メソッドでコンポーネントを定義する。
- コンストラクタベース：Vue.extend()メソッドでコンポーネントを定義する。戻り値にVueコンストラクタが返る。

## コンポーネントの定義
- 定義方法
    - `Vue.component()`でコンポーネントを作成する
      - 引数
          - 第１引数：コンポーネント名(string)
          - 第２引数：コンポーネントのオプションオブジェクト（Vueオブジェクトと同じオプションを指定する）（object）
    - Vue.extend()メソッドでのサブコンストラクタ方式（コンストラクタベース）

※カスタムタグのテンプレートベースの方が、コンストラクタベースよりも一般的で、おススメ。<br>理由は、HTML内で使えわかりやすいから。

## data()
- オプション関数。
- コンポーネントでは、dataオプションは、関数で定義する。
- vue objectのdataを定義する。
- vue objectとは定義の仕方が事なるので注意

```vue
<template>
  <div>
    <p>{{ message }}</p>
  </div>
</template>

<script>
Vue.component('my-component', {
  data(): {
    return {
      message: 'Hello, Vue.js!'
    }
  }
})
</script>
```

## Componentの命名規則
- ケバブケース（ハイフネーション）で命名する
- ケバブケース：`<my-component></my-component>`

## Component特有のよく使うオプション
- props：親コンポーネントから受け取るデータを定義できる
- components：コンポーネントの中で別のコンポーネントを定義できる（ローカルコンポーネント）



## 一応、Vue.componentでよく使うオプション一覧
| オプション名 | 説明 |
|:--|:--|
| data | UIの状態・データを定義する |
| props | 親コンポーネントから受け取るデータを定義する |
| computed | 算出プロパティを定義する |
| methods | メソッドを定義する |
| watch | ウォッチャを定義する |
|filters | フィルタを定義する |
| template | テンプレートを定義する |
| create ...etc | ライフサイクルフック系 |

## サンプルコード

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

## コンポーネント間のデータのやりとり
- 親コンポーネントから子コンポーネントへのデータの受け渡し
    - propsをで渡す
    - propsオプションを使う
    - propsオプションは、配列かオブジェクトで定義する
- 子コンポーネントから親コンポーネントへのデータの受け渡し
    - eventを渡す
    - $on()
      - イベントのlisten。カスタムイベントをlistenする
      - `v-on`ディレクティブを使うことで、イベントをlistenするのが、Vueでは一般的
      - `@<event>`で省略記法でもOK
    - $emit()
      - Vue.jsコンポーネント内でイベントを発火するために使用されるメソッドです。
      - これにより、子コンポーネントから親コンポーネントに対してカスタムイベントを送信できます。
      - 親コンポーネントは、v-on ディレクティブ（または @ ショートカット）を使用してこれらのイベントを受信し、適切なアクションを実行することができます。

具体的には、以
    
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


