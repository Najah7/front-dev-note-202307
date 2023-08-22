# Composition API
- Vue.js 3.0で導入されたComposition APIは、Vue.jsのコンポーネントを構築するための新しい手法
- 以前までのAPIはOptional APIを使っていた
- より柔軟性があり、再利用性が高く、コードの把握が容易になるよう設計されている
- Composition APIの場合、`<script>`タグ内でsetup関数し、その中の値にtemplate内からアクセスすることが可能
- `<template setup>`をsetUp関数の代わりに使える

## Composition APIの特徴
- setupの中で`data() { return {} }`を定義する必要がない(ただreturnで返す)
- dataやmethodsの代わりに、setup関数の中でrefやreactiveを使って変数を定義する
- methodsで関数を定義する必要がない(ただreturnで返す)

## setup([props, context])関数
- Composition APIのエントリーポイント
- Vue.jsのコンポーネントの初期化時に呼び出される
- setup関数の中で定義された変数や関数は、template内からアクセスすることが可能
- `<template setup>`をsetUp関数の代わりに使える
- 関数の場合、引数にpropsとcontextを受け取ることができる
    - props: 親コンポーネントから渡された値
- context: コンポーネントのライフサイクルや、スロット、カスタムイベントなどの機能を提供するオブジェクト
- 関数なので、returnが必要な点に注意
- thisは使えない

```ts
import { ref } from 'vue'

export default {
  setup() {
    const count = ref(0)

    const increment = () => {
      count.value++
    }

    return {
      count,
      increment
    }
  }
}
```

## ref
- リアクティブな値を作成する
- Vue.js内で状態を管理するために使用されるリアクティブな変数を作成するための関数
- 主に単一の値（プリミティブ型やオブジェクト）を保持するのに使用されます
- その変数の値が変更されたときに、Vue.jsは関連するコンポーネントを再描画するなどの反応を示すことができ
- 値の変更は.valueで行う

```ts
import { ref } from 'vue'

const count: Ref<number> = ref(0)

const increment = () => {
  count.value++
}
```

## reactive
- リアクティブなオブジェクトを作成する
- Vue.jsにおいて複雑なオブジェクトやネストされたデータ構造をリアクティブにするために使用される関数
- この関数を使用すると、オブジェクト全体が監視対象となり、その中のプロパティの変更も追跡される
- オブジェクト内のプロパティが変更されると、関連するコンポーネントが再描画されるなどの動作が可能になる

```ts
import { reactive } from 'vue'

const state = reactive({
  count: 0
})

const increment = () => {
  state.count++
}
```

## computed([getter, setter])
- 計算された値を返す
- Optional APIのcomputedと同じ
- Vue.jsにおいて、複雑な計算を行うために使用される関数
- この関数を使用すると、計算結果をキャッシュすることができ、その値が変更されない限り、再計算されることはない

```ts
import { computed } from 'vue'

export default {
  setup() {
    const count = ref(0)

    const double = computed(() => count.value * 2)

    return {
      count,
      double
    }
  }
}
```

## watch([source, callback, options])
- Vue.jsにおいて、リアクティブな値の変更を監視し、コールバック関数を実行するために使用される関数
- Optional APIのwatchと同じ

```ts
import { watch } from 'vue'

export default {
  setup() {
    const count = ref(0)

    watch(count, (newValue, oldValue) => {
      console.log(newValue, oldValue)
    })

    return {
      count
    }
  }
}
```

