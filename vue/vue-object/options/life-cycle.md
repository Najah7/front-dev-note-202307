# ライフサイクル
- [ライフサイクルの図（公式）](https://vuejs.org/guide/essentials/lifecycle.html#lifecycle-diagram)

## ライフサイクルフックの使いどころ
- Authrication
  - ログインしていないユーザーがアクセスできないページにアクセスしたときに、ログインページにリダイレクトする
- API Calls
  - ページを表示する前に、APIを呼び出してデータを取得する
- Creating or Removing Event Listeners
  - ページを表示する前に、イベントリスナーを登録する

# ライフサイクルフック
- Vueインスタンスのライフサイクルに沿って呼び出される関数
- 流れ
  1. Vueインスタンスの生成
  1. イベントとライフサイクル初期化
  1. beforeCreate
  1. 依存関係とリアクティブ関連の初期化
  1. created
  1. テンプレートのコンパイル
  1. beforeMount
  1. elの置き換え
  1. マウント(mounted)
  1. 再描画(beforeUpdate → updated)
  1. watcher・子コンポーネント・イベントリスナーの停止
  1. 破棄

## フックとタイミング
| フック名 | フックが呼び出されるタイミング |
|:--|:--|
| beforeCreate | Vueインスタンスが生成された後、データの監視やイベントの購読が行われる前 |
| created | Vueインスタンスが生成された後、データの監視やイベントの購読が行われた後<br>Vuexを導入していな小規模アプリで、Web APIと通信する処理を開始したり、setIntervalやsetTimeoutで繰り返し実行したりタイマー処理を開始するポイント。<br>DOM要素はインスタンスと結びついてないので、DOM APIの要素は取得できない |
| beforeMount | Vueインスタンスがマウントされる前 |
| mounted | Vueインスタンスがマウントされた後。<br>DOM操作やイベントリスナーの登録が必要な場合に必要なフック。 |
| beforeUpdate | データが変更され、DOMに適用される前 |
| updated | データが変更され、DOMに適用された後 |
| beforeDestroy | Vueインスタンスが破棄される前。<br>後処理をここで記述する。 |
| destroyed | Vueインスタンスが破棄された後 |