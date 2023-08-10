# 非同期処理

## JSでの非同期処理の実現方法
- ブラウザのAPIにタスクを投げることで実現している
    👆※JSはシングルスレッドなので、同時に複数の処理を実行することができない
- 下記の要素を使うことで非同期を実現している
    - コールスタック：普通の使い方。関数を実行するのに使う
        1. 関数を実行
        2. コールスタックに積む
        3. 処理が終わる前に別の関数実行
        4. コールスタックに積む
        5. 処理が終了したら、コールスタックから取り出す
    - タスクキュー：普通の使い方。タスクをためて、タスクを始めることで、コールスタックを使用して実行
    - Web API(ブラウザのAPI)：非同期処理を実現するためのAPIなど、様々なAPIを提供。これはJSの機能ではないというがポイント。Web APIで処理が終了したら、タスクキューに積む
        - setTimeout：WebAPIに投げることによって、他の処理を実行できてる。
        - fetch
        - DOM API ...etc

## 非同期処理の実装方法
- Promise
- async/await

## Promise
- Promiseは非同期処理を表すオブジェクト
- Promiseの状態
  - pending: 処理中
  - fulfilled: 成功
  - rejected: 失敗
- Promiseでの非同期処理の構成要素
    - .then & .catch
    - resolve & reject
- .then()＆.catch()
    - Promiseの状態が変化すると、then()やcatch()が呼び出される
    - .then()で成功時の処理を記述する
    - catch()で失敗時の処理を記述する
- resolve()＆reject()
    - Promiseが処理を完了したときに呼び出されるコールバック関数
    - resolve()
        - 成功時の処理に渡す値を引数に渡す。
        - .then()のコールバック関数の引数に渡される
    - reject()
        - 失敗時の処理に渡す値を引数に渡す
        - 基本的にはエラーオブジェクトを渡す
        - .catch()のコールバック関数の引数に渡される

### Promiseのサンプルコード
```ts
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('成功')
  }, 1000)
})

promise
  .then((result) => {
    console.log(result)
  })
  .catch((error) => {
    console.error(error)
  })
```
👆 resolve

## async/await
- async/awaitはPromiseをより簡潔に記述するための構文
- async/awaitの実装方法
    - async function
    - await
- async functionはPromiseを返す
- awaitはasync function内でのみ使用可能
- awaitはPromiseが完了するまで待機する

```ts
// async/awaitパターン
async function main() {

  const result = await promise

  result.then((result) => {
    console.log(result)
  })
    .catch((error) => {
        console.error(error)
    })
}

main()
```