# インポートについて

## import vs require
- require
    - どっちかというと、古い
    - CommonJS形式のインポート
    - Node.jsで導入された構文
    - 同期である
    - キャッシュされる
    - Node.js では CommonJS を利用しているためモジュールを読み込む際に require を利用する。
    ```ts
    const foo = require('foo')
    ```
- import
    - どっちかというと、新しい
    - ECMAScript形式のインポート
    - ES6から導入された構文
    - 非同期である
    ```ts
    import { foo } from 'foo'
    ```

