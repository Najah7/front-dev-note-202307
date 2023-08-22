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