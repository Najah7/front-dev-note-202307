# Nuxt3

## ディレクトリ構成()

### デフォルトで作成される
- app.vue
    - ルートコンポーネント
- nuxt.config.ts
    - Nuxtの設定ファイル
- package.json
    - プロジェクトの設定ファイル
- package-lock.json
    - パッケージのバージョンを固定するためのファイル
- public
    - 静的ファイルを配置するディレクトリ
- server
    - サーバーサイドのコードを配置するディレクトリ
- tsconfig.json
    - TypeScriptの設定ファイル

### 自分で作成する
- components
    - コンポーネントを配置するディレクトリ
- layouts
    - レイアウトを配置するディレクトリ
- pages
    - ページコンポーネントを配置するディレクトリ

## ツリー
.
├── Dockerfile
├── README.md
├── app.vue
├── components
├── layouts
│   └── default.vue
├── nuxt.config.ts
├── package-lock.json
├── package.json
├── pages
│   └── index.vue
├── public
│   └── favicon.ico
├── server
│   └── tsconfig.json
└── tsconfig.json

## 自動ルーティング（pagesディレクトリ）の使いかた
- pagesを作成する（`npx nuxi add page <ページ名>` or 手動）
- app.vueに`<NuxtPage />`を記述する or app.vueを削除する

## レイアウト（layoutsディレクトリ）の使いかた
- layoutsを作成する（`npx nuxi add layout <レイアウト名>` or 手動）
- default.vueでデフォルトのレイアウトを定義できる
    - app.vueを削除した場合は、default.vueがデフォルトのレイアウトになる。
    - 削除してない場合は、`<NuxtLayout>`を記述することで、default.vueを使用することができる。
    - 動的にレイアウトを変えたい場合は、`setPageLayout('<レイアウト名>')`を使用する。(jsを使ってトリガーは設定)
    ```vue
    <!-- default.vue -->
    <template>
        <Nuxt />
        <slot />
    </template>

    <!-- app.vue -->
    <template>
        <!-- <NuxtLayout name=<任意のレイアウト名> -->
        <NuxtLayout >
            <NuxtPage />
        </NuxtLayout>
    ```
- デフォルトの無効化
    ```vue
    <template>
        <Nuxt />
    </template>

    <script>
    export default {
        layout: false
    }
    </script>
    ```

## Lazy Loading
- ページコンポーネントの読み込みを遅らせることができる
- ページコンポーネントの読み込みを遅らせることで、ページコンポーネントの読み込みにかかる時間を短縮することができる
```vue
<template>
  <div>
    <h1>Main Page</h1>
    <button @click="handleClick">Coupon Get</button>
    <Coupon v-if="show" />
  </div>
</template>
<script setup>
  const show = ref(false);

  const handleClick = () => {
    show.value = true;
  };
</script>
```

## NxutLink
- ページ遷移を行うためのコンポーネント
- `<a>`タグと同じように使用することができる
- `<NuxtLink>`を使用することで、ページの中で更新が必要な箇所だけ更新が行われるようになる
```vue
<template>
  <div>
    <h1>Main Page</h1>
    <NuxtLink to="/coupon">Coupon Get</NuxtLink>
  </div>
</template>
```

## CSSの設定
- CSSの設定は、`nuxt.config.ts`で行う

```ts
// nuxt.config.ts
export default defineNuxtConfig({
  css: [
    // プロジェクト全体で使用するCSS
    '~/assets/css/common.css'
  ],
  styleResources: {
    // 全てのSCSSファイルで使用できる変数を定義する
    scss: [
      '~/assets/css/variables.scss'
    ]
  }
})
```

## CSSのインポート
- importを使用する
- import するだけでファイルの中身がコンパイルされ、適用される
- `scoped`を使用することで、スコープを限定することができる
```vue
<style lang="scss">
@import '~/assets/css/common.scss';
</style>
```

## Metaタグの設定
- metaというkeyのvalueにオブジェクトの配列を渡すことで、metaタグを設定することができる。
- configで設定した場合、グローバルに設定される
- ページによってmetaタグを変えたい場合は、`head()`を使用する

```ts
// nuxt.config.ts
export default defineNuxtConfig({
  head: {
    title: 'Nuxt3',
    meta: [
      { charset: 'utf-8' },
      { name: 'viewport', content: 'width=device-width, initial-scale=1' },
      { link: { rel: 'icon', type: 'image/x-icon', href: '/favicon.ico' } }
    ]
  }
})
```

```ts
// pages/index.vue
<script setup>
import { defineHead } from '@nuxtjs/composition-api'

defineHead({
  meta: [
    { hid: 'description', name: 'description', content: 'Nuxt.js project' }
  ]
})
```

## composablesディレクトリ
- ページコンポーネントで使用するロジックを切り出すことができる
- Reactでのカスタムフックのようなもの
- Auto importを有効にすることで、`use`を使用することで、composablesディレクトリの中身を使用することができる

```ts
// composables/useCounter.ts
import { ref } from '@nuxtjs/composition-api'

export const useCounter = () => {
  const count = ref(0)

  const increment = () => {
    count.value++
  }

  const decrement = () => {
    count.value--
  }

  return {
    count,
    increment,
    decrement
  } 
}

export default defineNuxtConfig({
  return {
    provide: {
      counter: useCounter()
    }
  }
})
```

```vue
<script setup>
const { $counter } = useNuxtApp()
</script>
```

## pluginsディレクトリ
- プラグインを配置するディレクトリ
- plugins ディレクトリを作成してプラグインファイルを作成するとアプケーションの起動時に Nuxt が作成したプラグインを自動で登録を行ってくれるため登録作業を行う必要がありません
- `useNuxtApp()`を使用することで、プラグインを取得することができる

```js
// plugins/logger.js
export default {
  install: (app) => {
    app.config.globalProperties.$log = (message) => {
      console.log(`[Custom Logger]: ${message}`);
    };
  },
};
```

```js
<template>
  <div>
    <button @click="logMessage">ログを出力</button>
  </div>
</template>

<script>
export default {
  methods: {
    logMessage() {
      this.$log('これはカスタムログメッセージです！');
    },
  },
};
</script>
```

```js
const { $log } = useNuxtApp()
$log('これはカスタムログメッセージです！')
```

## pluginsの設定
- pluginsの設定は、`nuxt.config.ts`で行う

```ts
// nuxt.config.ts
export default defineNuxtConfig({
  plugins: [
    '~/plugins/logger.ts'
  ]
})
```

## middlewareディレクトリ
- ミドルウェアを配置するディレクトリ
- ミドルウェアは、ページコンポーネントの描画前に実行される
- `defineMiddleware()`を使用することで、ミドルウェアを定義することができる。fromとtoが渡される。
    - `from`で、ミドルウェアを使用するページを指定することができる
    - `to`で、ミドルウェアを使用するページを指定することができる

```ts
// middleware/redirect.ts
import { defineMiddleware } from '@nuxtjs/composition-api'

export default defineMiddleware(({ from, to }) => {
  if (from.path === '/redirect') {
    return '/redirected'
  }
})
```

```ts
// nuxt.config.ts
export default defineNuxtConfig({
  router: {
    middleware: ['redirect']
  }
})
```

```vue
<!--  pages/redirect.vue -->
<script setup>
definePageMeta({
  middleware: 'redirect'
})
</script>
```

## Page Transitions
- ページ遷移時のアニメーションを設定することができる

```ts
// nuxt.config.ts
export default defineNuxtConfig({
  pageTransition: {
    name: 'fade',
    mode: 'out-in'
  }
})
```

```css
/* assets/css/transitions.css */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
```

```vue
<!-- layouts/default.vue -->
<template>
  <div>
    <h1>Main Page</h1>
    <NuxtLink to="/coupon">Coupon Get</NuxtLink>
  </div>
</template>

<style lang="scss">
@import '~/assets/css/transitions.scss';
</style>
```

## Data Fetching
- ページコンポーネントの描画前にデータを取得することができる
- Nuxt3でのFetch関係の関数
    - useFetch：データを取得するための関数(useAsyncFetch関数と$fetchを便利にしたWrapper関数)
        - `useFetch('https://jsonplaceholder.typicode.com/posts')`のように使用する
        - `useFetch(url, options)`のようにオプションを渡すことができる
        - options：オブジェクトでoptionsを指定する
            - headers：リクエストヘッダーを設定する（オブジェクト）
            - method：リクエストメソッドを設定する（GET, POST, PUT, DELETE）
            - params：クエリパラメータを設定する（オブジェクト）
            - body：リクエストボディを設定する（オブジェクト）
        - 戻り値
          - data：取得したデータ
          - pending：データ取得中かどうか
          - error：エラーが発生したかどうか
          - execute：データを取得する関数
          - refresh：データを再取得する関数
          
      ```ts
      function useFetch(
        url: string | Request | Ref<string | Request> | () => string | Request,
        options?: UseFetchOptions<DataT>
      ): Promise<AsyncData<DataT>>

      type UseFetchOptions = {
        key?: string
        method?: string
        query?: SearchParams
        params?: SearchParams
        body?: RequestInit['body'] | Record<string, any>
        headers?: Record<string, string> | [key: string, value: string][] | Headers
        baseURL?: string
        server?: boolean
        lazy?: boolean
        immediate?: boolean
        default?: () => DataT
        transform?: (input: DataT) => DataT
        pick?: string[]
        watch?: WatchSource[]
      }
      ```
    - useAsyncFetch：データを取得するための関数（非同期）
      - keyは、キャッシュのキーになる(省略可能。その場合はテキトウなキーが設定される)
      - ```ts
          function useAsyncData(
            handler: (nuxtApp?: NuxtApp) => Promise<DataT>,
            options?: AsyncDataOptions<DataT>
          ): AsyncData<DataT>

          function useAsyncData(
            key: string,
            handler: (nuxtApp?: NuxtApp) => Promise<DataT>,
            options?: AsyncDataOptions<DataT>
          ): Promise<AsyncData<DataT>>

          type AsyncDataOptions<DataT> = {
            server?: boolean
            lazy?: boolean
            default?: () => DataT | Ref<DataT> | null
            transform?: (input: DataT) => DataT
            pick?: string[]
            watch?: WatchSource[]
            immediate?: boolean
          }

          type AsyncData<DataT, ErrorT> = {
            data: Ref<DataT | null>
            pending: Ref<boolean>
            refresh: (opts?: AsyncDataExecuteOptions) => Promise<void>
            execute: (opts?: AsyncDataExecuteOptions) => Promise<void>
            error: Ref<ErrorT | null>
            status: Ref<AsyncDataRequestStatus>
          };

          interface AsyncDataExecuteOptions {
            dedupe?: boolean
          }

          type AsyncDataRequestStatus = 'idle' | 'pending' | 'success' | 'error'
        ```
    - useLazyFetch
      - データを取得するための関数（遅延読み込み、非同期）。
      - つまり、Lazyをつける、とfetchが完了する前に次のページが描画される。
      - useFetchのオプションで`{ lazy: true }`を指定することで、useLazyFetchと同じように使用することができる。
    - useLazyAsyncFetch：useAsyncFetchのLazy版
    - $fetch：使い方はほぼ、fetch APIと同じ。すこし便利になっている。
      - ofetchライブラリを内部で使っている
        - ofetchは、Node, ブラウザ、ワーカー上で利用できる fetch API のラッパー
        - responseをjsonに変換してくれる（`response.json()`を呼び出す必要がない）
  


## Molules
- モジュールを使用することで、簡単に機能を追加することができる
- https://nuxt.com/modules
- モジュールの設定は、`nuxt.config.ts`で行う

```ts
// nuxt.config.ts
export default defineNuxtConfig({
  modules: [
    '@nuxtjs/axios',
    '@nuxtjs/pwa',
    '@nuxtjs/sitemap'
  ],
  axios: {
    baseURL: 'https://jsonplaceholder.typicode.com'
  },
  sitemap: {
    hostname: 'https://example.com'
  }
})
```

## Nuxt TailwindCSS
- TailwindCSSを使用するためのモジュール
- https://tailwindcss.nuxtjs.org/
- モジュールの設定は、`nuxt.config.ts`で行う


### インストール
```bash
npm install --save-dev @nuxtjs/tailwindcss tailwindcss@latest postcss@latest autoprefixer@latest
```

### 適用

```bash
npx tailwindcss init
```

```ts
// nuxt.config.ts
export default defineNuxtConfig({
  buildModules: [
    '@nuxtjs/tailwindcss'
  ]
})
```

## useState
- 状態管理を行うための関数
- `useState()`を使用することで、状態管理を行うことができる
- コンポーネントの状態を管理するための関数
- refだと、値の変更を検知できないが、useStateだと、値の変更を検知できる。
- また、ページを移動しても同じコンポーネントが利用されている場合、refだと、値が初期化されるが、useStateだと、値が初期化されない。

```vue
<template>
  <div>
    <h1>Main Page</h1>
    <button @click="increment">Increment</button>
    <button @click="decrement">Decrement</button>
    <p>count: {{ count }}</p>
  </div>
</template>

<script setup>
import { useState } from '@nuxtjs/composition-api'

const [count, setCount] = useState(0)

const increment = () => {
  setCount(count.value + 1)
}

const decrement = () => {
  setCount(count.value - 1)
}
</script>
```

## エラーハンドリング

### NuxtErrorBoundary
- クライアント側で発生するエラーをキャッチして事前に設定したエラー内容をブラウザ上に表示させたいときに利用できるコンポーネント

```html
<template>
  <NuxtErrorBoundary>
    <Nuxt />
    <template #error="{ error }">
      <div v-if="error.statusCode === 404">
        <h1>404 - Page not found</h1>
      </div>
      <div v-else>
        <h1>Oops.. Something went wrong</h1>
      </div>
  </NuxtErrorBoundary>
</template>

```

### createError
- エラーを作成する関数
- NuxtErrorBoundaryを使用する場合は、フルスクリーンのエラーページは表示されない。
- サーバサイドでエラーを作成する場合によく使用する。
```ts
thorw createError({
  statusCode: 404,
  statusMessage: 'Not Found',
  message: 'Not Found'
  fatal: true // default: false
})
```

### showError
- エラーを表示する関数
- NuxtErrorBoundaryを使用する場合でもフルスクリーンのエラーページが
```ts
showError({
  statusCode: 404,
  statusMessage: 'Not Found',
  message: 'Not Found'
  fatal: true // default: false
})
```

## error.vue(プロジェクト直下に作成)
- フルスクリーン表示されたエラーページをカスタマイズすることができる。
- useErrorを使うことで、エラー情報を取得することができる。

```vue
<template>
  <div>
    <h1>Error Page</h1>
    <p>{{ error.message }}</p>
  </div>

</template>

<script setup>
import { useError } from '@nuxtjs/composition-api'
const { error } = useError()
</script>
```

## clearError
- エラーをクリアする関数
- error.vueにボタンなどをトリガーにして、エラーをクリアすることができる。

```vue
<template>
  <div>
    <h1>Error Page</h1>
    <p>{{ error.message }}</p>
    <button @click="clearError">Clear Error</button>
  </div>
</template>

<script setup>
import { useError } from '@nuxtjs/composition-api'
const { error, clearError } = useError()
</script>
```

## vueApp.config.errorHandler
- エラーハンドラーを設定することができる
- エラーハンドラーを設定することで、エラーが発生したときに、エラー情報を取得することができる。

```ts
// plugins/vueAppErrorHandler.ts
import { defineNuxtPlugin } from '@nuxtjs/composition-api'

export default defineNuxtPlugin(({ vueApp }) => {
  vueApp.config.errorHandler = (err, vm, info) => {
    console.log(err)
    console.log(vm)
    console.log(info)
  }
})
```

## レンダリングモード
- レンダリングモードを設定することができる
- `nuxt.config.ts`で設定することができる
- 種類
  - Universal Mode：CSR＋SSRを組み合わせたもの。Nuxtのデフォルト。SSRで見た目を送信し、CSRでインタラクティブな部分を生成する。（Hydration）
  - CSR Mode：CSRのモード
    - ```ts
      // nuxt.config.ts
      export default defineNuxtConfig({
        routeRules: [
          {
            name: 'index',
            path: '/',
            render: 'csr'
          }
        ]
      })
      ```