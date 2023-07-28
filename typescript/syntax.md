# TypeScriptの基本文法

## TypeScriptの基本文法
- 型定義
- インタフェースとクラス
- null/undefined安全
- 汎用的なクラスやメソッドの方を実現するジェネリクス
- エディタによる入力補完
- そのほかのECMAで定義されているJavaScriptの最新機能

## サンプルコード
```ts
function sayHello(name: string): void {
    console.log(`Hello ${name}`);
}
```

## Optional Chaining
- オブジェクトのプロパティが存在しない場合にエラーを発生させずにundefinedを返す
- プロパティが存在するかの条件分岐を簡単に記述できる
```ts
const tmp_obj: { name: string, age?: number } = { name: 'Taro' };

console.log(tmp_obj.age?.toString()); // undefined
```

## Non-null Assertion Operator
- プロパティがnull/undefinedである可能性があることを明示的に示す
- TypeScriptの型システムを無効化できる
```ts
const tmp_obj: { name: string, age?: number } = { name: 'Taro' };

console.log(tmp_obj.age!.toString()); // undefined
```

## 型ガード
- 型を絞り込むことで、型の安全性を高める
- if文やswitch文の条件分岐にて型のチャックを行った際、その条件分岐ブロック以降の変数の型を絞り込むことができる
```ts
function addOne(value: number | string): number | string {
    if (typeof value === 'number') {
        return value + 1;
    } else {
        return value + '1';
    }
}
```

## keyof演算子
- オブジェクトのプロパティ名を文字列リテラル型として取得する
```ts
interface Person {
    name: string;
    age: number;
}

type PersonKey = keyof Person; // 'name' | 'age'
```
## readonly修飾子
- オブジェクトのプロパティを読み取り専用にする
```ts
type Person = {
    readonly name: string;
    age: number;
}
```

## unknown型
- すべての型のスーパータイプ
- anyと違い、代入された値はそのまま任意の関数やプロパティにアクセスすることができない
- 代入された値の型を絞り込むことで、anyと同様のことができる
```ts
let tmp: unknown = 1;
tmp = 'hoge';
tmp = true;

// 代入された値の型を絞り込む
if (typeof tmp === 'string') {
    tmp.toUpperCase();
}
```

## Async/Await
```ts
fuction fetchServer(id:string): Promise<{success: boolean}>{
    return new Promise((resolve) => {
        setTimeout(() => {
            resolve({ success: true });
        }, 1000);
    });
}

async function fetchServerAsync(id: string): Promise<{ success: boolean }> {
    const result = await fetchServer(id);
    return result;
}
```


## 型定義ファイル
- JavaScriptのライブラリをTypeScriptで利用するために必要なファイル
- 型定義ファイルは、型定義ファイルの管理ツールであるDefinitelyTypedから取得することができる

### 導入方法
- @typesに代表される公開されている型定義ファイルを利用する
- 型定義ファイルを自作する
```sh
npm install --save-dev @types/ライブラリ名
```

### 型定義ファイルの作成
- 型定義ファイルは、.d.tsという拡張子を付けたファイルに記述する
- 型定義ファイルは、JavaScriptのコードをTypeScriptのコードに変換することができる
```ts
export function addOne(value: number): number;
```

### 型のインポート
- 型定義ファイルを利用する際は、import文を利用して型をインポートする
```ts
import { addOne } from 'ライブラリ名';
```