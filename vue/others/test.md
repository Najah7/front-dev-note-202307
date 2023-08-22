# テスト

## コンポーネントの単体テスト
- karma + mocha + power-assertパターン
    - karma: テストランナー
    - mocha: テストフレームワーク
    - power-assert: アサーションライブラリ

### karmaのインストール
```bash
$ npm install -g karma-cli
```

### karmaの設定
```bash
$ karma init
```

### karmaの起動
```bash
$ karma start
```

### karmaの設定ファイル
```js
module.exports = function(config) {
  config.set({
    // テストランナー
    frameworks: ['mocha'],
    // テスト対象のファイル
    files: [
      'test/**/*.js'
    ],
    // テスト対象のファイルをブラウザで実行する前に、webpackでバンドルする
    preprocessors: {
      'test/**/*.js': ['webpack']
    },
    // webpackの設定
    webpack: {
      module: {
        loaders: [
          {
            test: /\.js$/,
            exclude: /node_modules/,
            loader: 'babel-loader'
          }
        ]
      }
    },
    // テスト結果の出力
    reporters: ['progress'],
    // テスト対象のファイルをブラウザで実行する
    browsers: ['Chrome'],
    // テスト対象のファイルをブラウザで実行する際のオプション
    customLaunchers: {
      Chrome_travis_ci: {
        base: 'Chrome',
        flags: ['--no-sandbox']
      }
    },
    // テスト対象のファイルをブラウザで実行する際のオプション
    singleRun: true
  });

  // Travis CIでのテスト実行時にChromeが起動するようにする
  if (process.env.TRAVIS) {
    config.browsers = ['Chrome_travis_ci'];
  }
};
```

### mochaのインストール
```bash
$ npm install --save-dev mocha
```

### mochaの設定
```js
// package.json
{
  "scripts": {
    "test": "mocha --compilers js:babel-core/register"
  }
}
```

### power-assertのインストール
```bash
$ npm install --save-dev power-assert
```

### power-assertの設定
```js
// .babelrc
{
  "presets": [
    "es2015"
  ],
  "plugins": [
    "transform-runtime"
  ],
  "env": {
    "test": {
      "plugins": [
        "babel-plugin-espower"
      ]
    }
  }
}
```

## テストのサンプルコード

### テスト対象のコンポーネント
```js
// src/components/Counter.js

export default {
  template: `
    <div>
      <span class="count">{{ count }}</span>
      <button @click="increment">+</button>
    </div>
  `,
  data() {
    return {
      count: 0
    };
  },
  methods: {
    increment() {
      this.count++;
    }
  }
};
```

### テスト対象のコンポーネントのテストコード
```js
// test/components/Counter.spec.js

import assert from 'power-assert';
import Vue from 'vue';
import Counter from '../../src/components/Counter';

describe('Counterコンポーネント', () => {
  let vm;

  beforeEach(() => {
    const targetComponent = Vue.extend(Counter);
    vm = new targetComponent().$mount();
  });

  it('初期値は0である', () => {
    assert.equal(vm.count, 0);
  });

  it('ボタンをクリックするとカウントアップする', () => {
    vm.increment();
    assert.equal(vm.count, 1);
  });
});
```
