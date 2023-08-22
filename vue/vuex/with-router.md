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