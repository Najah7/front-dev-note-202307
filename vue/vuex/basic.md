# Vuex

## Vuexとは
- Vue.jsの状態管理ライブラリ
- Fluxアーキテクチャの考え方を取り入れたライブラリ

## Vuexのインストール
- npmを使う場合
    - `npm install vuex`
    
## データフロー
- アプリケーションが持つデータの流れ

## Flux
- View -> Action -> Dispatcher -> Store -> View
    - View: ユーザーが操作する画面
    - Action: Viewでのユーザーの操作
    - Dispatcher: Actionを受け取り、Storeに伝える
    - Store: データを保持する
- 単方向である点が特徴

## データフローの設計において頻出するパターン（デザインパターン）
- 信頼できる唯一のー情報源（Single Source of Truth）
    - アプリケーションの状態は、唯一の情報源であるStoreに集約される
    - どのコンポーネントも同一のデータを参照するため、データや表示の不整合が発生しづらい
    - 複数のデータを組み合わせた処理を比較的容易に実装できる
- 「状態の取得・更新」のカプセル化
    - カプセル化により状態管理のコストを下げる
    - 状態の取得・更新のロジックを様々なコンポーネントで再利用できる
    - 詳細な実装をViewから隠すことで、データ構造や取得処理の変更の影響範囲を小さくする
    - デバッグ時に確認する場所が限られているため、デバッグが容易になる
- 単方向データフロー
    - データを取得しつつつ更新するということができなくなり、実装やデバッグが単純になる
    - データを取得、更新するために何をするかの選択肢が絞られて、理解が容易なコードを書きやすい

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

## Vuexをファイルに分割する
- store.js
```js
import Vue from "vue";
import Vuex from "vuex";

Vue.use(Vuex);

const store = new Vuex.Store({
    // 実装
})

export default store;
```
- main.js
```js
import Vue from "vue";

import store from "./store";

new Vue({
    el: "#app",
    store
});
```

## Storeのモジュール分割
- store.js
```js
import Vue from "vue";
import Vuex from "vuex";

Vue.use(Vuex);

const store = new Vuex.Store({
    modules: {
        // 下記を別ファイルに記述してimportするのが一般的👇
        moduleA: {
            state: {
                count: 0
            },
            mutations: {
                increment(state) {
                    state.count++;
                }
            },
            getters: {
                count: (state) => `現在の値は${state.count}です。`;
            }
        },
        moduleB: {
            state: {
                count: 0
            },
            mutations: {
                increment(state) {
                    state.count++;
                }
            },
            getters: {
                count: (state) => `現在の値は${state.count}です。`;
            }
        }
    }
})

export default store;
```

## namespacedオプションによる名前空間
- namespacedオプションをtrueにすると、モジュールの名前空間が有効になる
- 有効になると、モジュールの名前空間が有効になる

| 分類 | namespacedなし | namespacedあり |
|:--|:--|:--|
| ステート | state.count | state.moduleA.count |
| ゲッター | getters.count | getters["moduleA/count"] |
| ミューテーション | commit("increment") | commit("moduleA/increment") |
| アクション | dispatch("increment") | dispatch("moduleA/increment") |

```js
const store = new Vuex.Store({
    modules: {
        moduleA: {
            namespaced: true,
            state: {
                count: 0
            },
            mutations: {
                increment(state) {
                    state.count++;
                }
            },
            getters: {
                count: (state) => `現在の値は${state.count}です。`;
            }
        },
        moduleB: {
            namespaced: true,
            state: {
                count: 0
            },
            mutations: {
                increment(state) {
                    state.count++;
                }
            },
            getters: {
                count: (state) => `現在の値は${state.count}です。`;
            }
        }
    }
})
```

## VuexストアとVueコンポーネント間の通信
- コンポーネントからストアにアクセスする
    - `this.$store`によるアクセス。ルートのコンポーネントのstoreオプションに渡されたストアのインスタンスが格納されている。
    - ヘルパー関数によるアクセス。mapState, mapGetters, mapMutations, mapActions

## mapState
- ステートをコンポーネントの算出プロパティにマッピングする

```js
import { mapState } from "vuex";

export default {
    computed: {
        ...mapState(["count"])
    }
}
```

## ストアにアクセスするコンポーネントを必要最小限にする
- 変化に強くなる。
- ストアにアクセスできるコンポーネントを減らすことで実現できる
- 具体的な手法
    - Presentational ComponentとContainer Componentに分割する
    - Atomic Designの考え方を取り入れる

## Atmoic Designとストア

| Atomic Design | Vuex |
|:--|:--|
| Atoms | ストアにアクセスしない |
| Molecules | ストアにアクセスする |
| Organisms | ストアにアクセスする |
| Templates | ストアにアクセスしない |
| Pages | ストアにアクセスしない |

※一例。Organismsのみも一般的。

## VuexとVue Routerの連携

```js
import Vue from "vue";
import VueRouter from "vue-router";
import Vuex from "vuex";

import { sync } from "vuex-router-sync";

Vue.use(Vuex);
Vue.use(VueRouter);


const store = new Vuex.Store({
    state: {
        count: 0
    },
    mutations: {
        increment(state) {
            state.count++;
        }
    },
    getters: {
        count: (state) => `現在の値は${state.count}です。`;
    }
});

const router = new VueRouter({
    routes: [
        {
            path: "/",
            component: {
                template: "<div>トップページです。</div>"
            }
        },
        {
            path: "/other",
            component: {
                template: "<div>別のページです。</div>"
            }
        }
    ]
});

sync(store, router);

console.log(store.state.route);
```