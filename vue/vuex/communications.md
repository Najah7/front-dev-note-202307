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