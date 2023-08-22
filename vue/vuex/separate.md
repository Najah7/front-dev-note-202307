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