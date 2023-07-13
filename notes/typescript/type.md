# TypeScriptの型

## 基本的な型の機能
- 型推論：明示的な変数の初期化を行うと、その変数の型は推論される
- 型アサーション：型を明示的に指定することができる
    - `変数名 as 型`
    - 型アサーションが認められるのは、対象となる型に対してより具体的になる型かまたあｈ、汎用化される方に変換するケースのみ
    - 複雑なアサーションで行いたい型変換が上手くできない場合の技
        - `(変数名 as any) as 型`
- 型エイリアス：型指定の別名（エイリアス）をもうける機能
    - `type 型名 = 型`
    - 型エイリアスは型の別名を定義するだけで、新しい型を作るわけではない
    - オブジェクトの型エイリアス
        ```ts
        type User = {
            name: string;
            age: number;
        };

        const user: User = {
            name: 'Taro',
            age: 20
        };
        ```
    - 関数の型エイリアス
        ```ts
        type SayHello = (name: string) => void;

        const outerfuc = (func: SayHello) => {
            func('Taro');
        };
        ```
    - インデックス型：オブジェクトのキー名を明記せず、keyに型エイリアスを定義すること
        - ```ts
            type Label = {
                [key: string]: string;
            };
        ```

## プリミティブ型
- stiring
- number
- boolean

## 型定義
```ts
const 変数: 型 = 値;
```

## 配列
```ts
const 変数: 型[] = 値;
```

## オブジェクト型
```ts
const 変数: { キー1: 型, キー2: 型 } = オブジェクト;
```
```ts
const tmp_obj: { name: string, age: number } = { name: 'Taro', age: 20 };
```

## 省略可能なプロパティを使ったオブジェクト型

👇?が付いたプロパティは省略可能

```ts
const 変数: { キー1: 型, キー2?: 型 } = オブジェクト;
```
```ts
const tmp_obj: { name: string, age?: number } = { name: 'Taro' };
```

## any型
- 型を指定しない場合はany型となる
- すべての型を許容する

## 関数
```ts
function 関数名(引数1: 型 = デフォルト値, 引数2: 型 = デフォルト値): 戻り値の型 {
    return 戻り値;
}
```
```ts
function sayHello(name: string): void {
    console.log(`Hello ${name}`);
}
```

## アロー関数
```ts
const 関数名 = (引数1: 型 = デフォルト値, 引数2: 型 = デフォルト値): 戻り値の型 => {
    return 戻り値;
}
```
```ts
const sayHello = (name: string): void => {
    console.log(`Hello ${name}`);
}
```

## コールバック関数（高階関数）の型
```ts
const 関数名 = (引数1: 型 = デフォルト値, コールバック関数: (引数1: 型, 引数2: 型) => 戻り値の型): 戻り値の型 => {
    return 戻り値;
}
```
```ts
const outerfuc = (func: (name: string) => void) => {
    func('Taro');
};
```

## インタフェース
- 型エイリアスと似ているが、より柔軟な型定義が可能
- オーバーライド可能：同じ名前のインタフェースを定義すると、後から定義したインタフェースの値も含めた型となる（同じプロパティの場合は上書きされる）
- インタフェースも型エイリアスもオブジェクト対して使うときは機能的にはほぼ同じ。ただ、クラスに対してはよくインタフェースが用いられる

```ts
interface インタフェース名 {
    プロパティ: 型;
    プロパティ: 型;
}
```
```ts
interface User {
    name: string;
    age: number;
}
```

## クラスへのインタフェースの実装
```ts
interface インタフェース名 {
    プロパティ: 型;
    プロパティ: 型;
}

class クラス名 implements インタフェース名 {
    プロパティ: 型;
    プロパティ: 型;
}
```
```ts
interface User {
    name: string;
    age: number;
}

class User implements User {
    name: string;
    age: number;
}
```
👆?(オプショナル)を使うことも可能

## インタフェースの継承
```ts
interface インタフェース名1 {
    プロパティ: 型;
    プロパティ: 型;
}

interface インタフェース名2 extends インタフェース名1 {
    プロパティ: 型;
    プロパティ: 型;
}
```
```ts
interface User {
    name: string;
    age: number;
}

interface SuperUser extends User {
    isAdmin: boolean;
}
```

## クラス
- 型に関しては今までの変数への型定義と関数に対する型定義をまとめただけ
- 加えて、アクセス演算子を使える
- アクセス演算子
    - public：どこからでもアクセス可能（デフォルト値）
    - private：クラス内からのみアクセス可能
    - protected：クラス内と継承したクラス内からのみアクセス可能

```ts
class クラス名 {
    プロパティ: 型;
    プロパティ: 型;

    constructor(引数1: 型 = デフォルト値, 引数2: 型 = デフォルト値) {
        this.プロパティ = 引数1;
        this.プロパティ = 引数2;
    }

    メソッド名(引数1: 型 = デフォルト値, 引数2: 型 = デフォルト値): 戻り値の型 {
        return 戻り値;
    }
}
```
```ts
class User {
    name: string;
    age: number;

    constructor(name: string, age: number) {
        this.name = name;
        this.age = age;
    }

    sayHello(): void {
        console.log(`Hello ${this.name}`);
    }
}
```

## Enum型
- 列挙型
- 定数の集合を表す型。（書き換え不可）
```ts
enum 列挙型名 {
    プロパティ1 = 値1,
    プロパティ2 = 値2,
    プロパティ3 = 値3,
}
```
```ts
enum Direction {
    Up = 1,
    Down,
    Left,
    Right,
}
// 👆Emum型指定されなかった場合、順番に沿って0からの連番が割り振られる（上記の場合、1から指定している。）

```

## ジェネリック型（ジェネリクス）
- クラスや関数において、その中で使う方を抽象化し、外部から具体的な型を指定できる機能。
- 型を引数として受け取ることができる
- 型引数は複数指定することも可能
- 型引数は、関数の引数や戻り値の型としても使える
```ts
class クラス名<型引数1, 型引数2> {
    プロパティ: 型引数1;
    プロパティ: 型引数2;

    constructor(引数1: 型引数1 = デフォルト値, 引数2: 型引数2 = デフォルト値) {
        this.プロパティ = 引数1;
        this.プロパティ = 引数2;
    }

    メソッド名(引数1: 型引数1 = デフォルト値, 引数2: 型引数2 = デフォルト値): 戻り値の型 {
        return 戻り値;
    }
}
```
```ts
class Pair<T, U> {
    constructor(public first: T, public second: U) {}
}

const pair = new Pair('Taro', 18);
```

## Union型
- 複数の型を指定することができる型
- 型の指定は、`|`で区切る
- 型の指定は、`()`で囲むこともできる
```ts
let 変数名: 型1 | 型2 | 型3;
```
```ts
let value: string | number | boolean;
```

## Intersection型
- 複数の型を結合した型
- 型の指定は、`&`で区切る
```ts
let 変数名: 型1 & 型2 & 型3;
```
```ts
let value: { name: string } & { age: number };
```

## リテラル型
- 型の値を指定することができる型
- 決まった文字列や数値しか入らない型という制御ができる
- 型の指定は、`:`で区切る
```ts
let 変数名: 型1 | 型2 | 型3;
```
```ts
let value: 'Taro' | 'Jiro' | 'Saburo';
```

## never型
- 何も返さない関数の戻り値の型として使う
- 例外を投げる関数の戻り値の型として使う
- 無限ループをする関数の戻り値の型として使う
```ts
function 関数名(): never {
    throw new Error();
}
```
```ts
function 関数名(): never {
    while (true) {
        console.log('Hello');
    }
}
```

