# スロット
- 外からコンテンツを受け取るための仕組み

## スロットを使う場面
- ページ全体のレイアウトを表現するコンポーネントに。（ヘッダー、フッターなど）
- アクションシートのコンポーネントに対して、選択可能なアクションを挿入する
- スライダーの各アイテムの内容を指定する

## スロットの種類
- 単一スロット
    - 固定の一箇所に要素を挿入する
    - 1つのスロットには、複数の要素を挿入することができる
- 名前付きスロット
    - name属性で名前を付けたスロットを持つコンポーネント
    - 指定した特定の場所に要素を挿入することができる

## 単一スロットのサンプルコード
```html
<div id="app">
    <my-component>
        <p>スロットの中身</p>
    </my-component>
</div>

<script>
    Vue.component('my-component', {
        template: '<div><slot></slot></div>'
    });

    const app = new Vue({
        el: '#app'
    });
</script>
```

## 名前付きスロットのサンプルコード
- name属性でslotの名前を指定できる
```html
<div id="app">
    <my-component>
        <template v-slot:header>
            <h2>ヘッダー</h2>
        </template>
        <template v-slot:footer>
            <h2>フッター</h2>
        </template>
    </my-component>
</div>

<script>
    Vue.component('my-component', {
        template: `
            <div>
                <header>
                    <slot name="header"></slot>
                </header>
                <main>
                    <slot></slot>
                </main>
                <footer>
                    <slot name="footer"></slot>
                </footer>
            </div>
        `
    });

    const app = new Vue({
        el: '#app'
    });
</script>
```
## 単一スロット＆名前付きスロットのサンプルコード

```html
<div id="app">
    <my-component>
        <template v-slot:header>
            <h2>ヘッダー</h2>
        </template>
        <template v-slot:footer>
            <h2>フッター</h2>
        </template>
        <p>スロットの中身</p>
    </my-component>
</div>

<script>
    Vue.component('my-component', {
        template: `
            <div>
                <header>
                    <slot name="header"></slot>
                </header>
                <main>
                    <slot></slot>
                </main>
                <footer>
                    <slot name="footer"></slot>
                </footer>
            </div>
        `
    });

    const app = new Vue({
        el: '#app'
    });
</script>
```

## スロットのスコープ
- スロットで子に渡された要素は、親のスコープが適用される

## スコープ付きスロット
- スロットには、スコープを持たせることができる
- 親から子のスコープの値にアクセスできる
- v-bindを使うことで、子から親のスコープの値にアクセスできる

## スコープ付きスロットのサンプルコード
```html
<div id="app">
    <todo-lis :todo="todos">
        <li slot-scope="{ todo }">{{ props.todo.text }}</li>
    </todo-lis>
</div>
```
