# トランザクションアニメーション

## transitionラッパーコンポーネント
- transitionコンポーネントは、要素がDOMに挿入されたり、削除されたり、更新されたりするときに、トランジションを適用するために使用されます。

## transitionコンポーネントで使うディレクティブ
| ディレクティブ名 | 説明 |
|:--|:--|
| v-enter | 要素がDOMに挿入される前の状態 |
| v-enter-active | 要素がDOMに挿入されるときの状態 |
| v-enter-to | 要素がDOMに挿入された後の状態 |
| v-leave | 要素がDOMから削除される前の状態 |
| v-leave-active | 要素がDOMから削除されるときの状態 |
| v-leave-to | 要素がDOMから削除された後の状態 |

## transitionコンポーネントの仕組み
1. v-enterが適用される
2. v-enter-activeが適用される
3. v-entaerが削除＆v-enter-toが適用される
4. アニメーションの終了＆transitionendイベントが発火
5. v-enter-toの削除＆v-enter-activeの削除

## プリフィックスを変更する
```html
<!-- fade-enterなどになる👇 -->
<transition name="fade">
    <div v-if="show">Fade</div>
</transition>
```

```css
.fade-enter-active,
.fade-leave-active {
    transition: opacity 1s;
}
.fade-enter,
.fade-leave-to {
    opacity: 0;
}
```

## Vue Routerのトランザクション
- Vue Routerのトランザクションは、ルートの遷移時に適用されるトランザクションです。
- トランザクションの適用は、transitionコンポーネントを使って行います。
```html
<transition name="fade">
    <router-view></router-view>
</transition>
```

## カスタムトランザクションクラス
- transitionコンポーネントには、カスタムトランザクションクラスを指定することができます。
- 外部ライブラリと連携する場合、renameした方がいい時もあるので、便利。

## 代表的なカスタムトランザクションクラス名
| クラス名 | 説明 |
|:--|:--|
| enter-class | 要素がDOMに挿入される前の状態 |
| enter-active-class | 要素がDOMに挿入されるときの状態 |
| enter-to-class | 要素がDOMに挿入された後の状態 |
| leave-class | 要素がDOMから削除される前の状態 |
| leave-active-class | 要素がDOMから削除されるときの状態 |
| leave-to-class | 要素がDOMから削除された後の状態 |


## JSフック
- transitionコンポーネントには、JSフックを使って、トランザクションの開始や終了時に処理を実行することができます。

| イベント名 | タイミング |
|:--|:--|
| before-enter | 要素がDOMに挿入される前 |
| enter | 挿入されて、アニメーションされる前 |
| after-enter | 挿入されて、アニメーションされた後 |
| enter-cancelled | 挿入されて、アニメーションがキャンセルされた後 |
| before-leave | 削除アニメーションが実行される前 |
| leave | 削除アニメーションが実行される前でbefore-leaveの後 |
| after-leave | 要素が削除された後 |
| leave-cancelled | 削除アニメーションがキャンセルされた後 |

## イベントリスナーの設定
```html
<transtion
    @before-enter="beforeEnter"
    @enter="enter"
    @after-enter="afterEnter"
    @enter-cancelled="enterCancelled"
    @before-leave="beforeLeave"
    @leave="leave"
    @after-leave="afterLeave"
    @leave-cancelled="leaveCancelled"
>