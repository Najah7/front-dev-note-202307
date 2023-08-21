# Vue CLI

## Vue CLIとは
- Vue.jsの開発を効率化するためのツール
- Vue.jsの開発に必要なツールをインストールしてくれる
- Vue.jsの開発に必要なツールを設定してくれる
- Vue.jsの開発に必要なツールを起動してくれる
- Vue.jsの開発に必要なツールをアップデートしてくれる

## Vue CLIのインストール
- Vue CLIのインストール
    - `npm install -g @vue/cli`
- Vue CLIのバージョン確認
    - `vue --version`

## Vue CLIのプロジェクトの作成
- Vue CLIのプロジェクトの作成
    - `vue create プロジェクト名`
- Vue CLIのプロジェクトの作成時の設定
    - プリセットの選択
        - `default (babel, eslint)`
        - `Manually select features`
    - プリセットの選択時の設定
        - `Babel`
        - `Router`
        - `Vuex`
        - `CSS Pre-processors`
        - `Linter / Formatter`
        - `Unit Testing`
        - `E2E Testing`
    - プリセットの選択時の設定の詳細
        - `Babel`
            - `Use Babel alongside TypeScript (required for modern mode, auto-detected polyfills, transpiling JSX)`
            - `Use history mode for router? (Requires proper server setup for index fallback in production)`
        - `Router`
            - `Use history mode for router? (Requires proper server setup for index fallback in production)`
        - `Vuex`
            - `Use history mode for router? (Requires proper server setup for index fallback in production)`
        - `CSS Pre-processors`
            - `Sass/SCSS (with dart-sass)`
            - `Less`
            - `Stylus`
        - `Linter / Formatter`
            - `ESLint with error prevention only`
            - `ESLint + Airbnb config`
            - `ESLint + Standard config`
            - `ESLint + Prettier`
            - `TSLint (deprecated)`
            - `Lint on save`
            - `Lint and fix on commit`
        - `Unit Testing`
            - `Mocha + Chai`
            - `Jest`
        - `E2E Testing`
            - `Cypress (Chrome only)`
            - `Nightwatch (Selenium-based)`

