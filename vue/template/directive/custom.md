# カスタムディレクティブ

## フック関数の引数
- el: ディレクティブが紐付いている要素
- binding: ディレクティブの情報
    - name: ディレクティブ名(v-を除いたもの)
    - value: ディレクティブに渡される値
    - expression: 文字列としてのバインディング式。例: v-my-directive="1 + 1"の場合、"1 + 1"が入る
    - arg: ディレクティブの引数。例: v-my-directive:fooの場合、"foo"が入る
    - modifiers: ディレクティブの修飾子。例: v-my-directive.foo.barの場合、{ foo: true, bar: true }が入る
- vnode: Vueコンパイラによって生成された仮想Node

※v-on:click.prevent.stop="foo"👈preventはarg、stopはmodifier

```js
// directive(name, definition-Object)
Vue.directive('ディレクティブ名', {
    bind: function(el, binding, vnode) {
        // ディレクティブが初めて対象の要素に紐付いた時
        // ただ一度だけ呼び出される
        // 初期化処理を記述（ex) イベントリスナーの登録..etc
    },
    inserted: function(el, binding, vnode) {
        // 親Nodeに挿入された時
    },
    update: function(el, binding, vnode, oldVnode) {
        // コンポーネントが更新される度。子コンポーネントが更新される前
        // ディレクティブの値が変化しなくても呼び出される可能性があるので、以前の値と比較することで不要な更新を回避する必要あり
        // if (binding.value !== binding.oldValue) { ... }
    },
    componentUpdated: function(el, binding, vnode, oldVnode) {
        // コンポーネントが更新される度。子コンポーネントが更新された後
        // VNodeが更新された後に呼び出される
    },
    unbind: function(el, binding, vnode) {
        // ディレクティブが紐付いている要素から取り除かれた時
        // ただ一度だけ呼び出される
        // bindで登録したイベントリスナーの削除など後処理を記述するお
    }
});
```