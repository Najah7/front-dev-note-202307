# Vuex

## Vuexとは
- Vue.jsの状態管理ライブラリ
- Fluxアーキテクチャの考え方を取り入れたライブラリ

## Vuexのインストール
- npmを使う場合
    - `npm install vuex`

## Vuexの構成要素
- State: アプリケーションの状態
- Getter: Stateを参照する関数
- Mutation: Stateを更新する関数
- Action: 外部APIとのやり取りを行う関数
- Module: State, Getter, Mutation, Actionをまとめる単位
- （Moduleの）流れ
    0. コンポーネント
    1. Action
    2. Mutation
    3. State
    4. getter
    0. コンポーネント

## Vuexの実装
- Vuexのインポート
    - `import Vuex from "vuex";`
- Vuexのインスタンスの作成
    - `const store = new Vuex.Store({});`
- VuexのインスタンスをVueインスタンスに渡す
    - `const app = new Vue({ store: store }).$mount("#app");`
- VuexのインスタンスをVueインスタンスに渡す（省略形）
    - `const app = new Vue({ store }).$mount("#app");`



## サンプルコード
```html
<div id="app">
    <p>{{ count }}</p>
    <button @click="increment">+</button>
    <button @click="decrement">-</button>
</div>

<script>
    const store = new Vuex.Store({
        state: {
            count: 0
        },
        mutations: {
            increment(state) {
                state.count++;
            },
            decrement(state) {
                state.count--;
            }
        }
        getters: {
            count: (state) => `現在の値は${state.count}です。`;
        }
        actions: {
            setCountInLocalStorage(context, payload) {
                localStorage.setItem("count", payload.count);
                context.commit("setCount", payload);
            }
        }
    });

    const app = new Vue({
        el: "#app",
        store,
        methods: {
            increment() {
                this.$store.commit("increment");
                this.$store.dispatch("setCountInLocalStorage", { count: this.$store.state.count });
            },
            decrement() {
                this.$store.commit("decrement");
                this.$store.dispatch("setCountInLocalStorage", { count: this.$store.state.count });
            }
        },
        computed: {
            count() {
                return this.$store.getters.count;
            }
        }
    });
</script>
```

## commit v.s. dispatch
- commit：Mutationを呼び出すメソッド
- dispatch：Actionを呼び出すメソッド

## State vs Component
- ステートに適したデータ
    - サーバーからデータを取得したかどうかを表すフラグ
    - ログイン中のユーザの情報など、アプリケーション全体で使用されるデータ
    - ECサイトにおける商品の情報など、アプリケーションの複数の場所で使用される可能性のあるデータ
- コンポーネントに適したデータ
    - マウスポインタ側で持つべきデータ
    - ドラッグ中の要素の座標
    - 入力中のフォームの値　

## Atmoic Designとストア

| Atomic Design | Vuex |
|:--|:--|
| Atoms | ストアにアクセスしない |
| Molecules | ストアにアクセスする |
| Organisms | ストアにアクセスする |
| Templates | ストアにアクセスしない |
| Pages | ストアにアクセスしない |

※一例。Organismsのみも一般的。

