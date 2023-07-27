# プロジェクトのセットアップ

## プロジェクトの作成
```bash
$ npx create-next-app <project-name>

# TypeScriptの場合
$ npx create-next-app <project-name> --typescript (--ts)
```

## プロジェクトの起動
```bash
$ npm run dev
```

## プロジェクトのビルド
```bash
$ npm run build
```

## プロジェクトの起動
```bash
$ npm run start
```

# プロジェクトの基本的な構成
|--node_modules
|--pages
|  |--about.tsx
|  |--api
|  |  |--index.tsx
|--public
|  |--favicon.ico
|  |--vercel.svg
|--styles
|  |--globals.css
|--|--Home.module.css
|--.gitignore
|--next.config.js
|--package.json
|--README.md
|--tsconfig.json

# React/Next.jsのバージョン
- 互換性はしっかり確認すべき
- Reactは最新版が常に安定版
- バージョンで互換性がない場合の対策
    - 互換性のあるバージョンにダウングレードする
    - 互換性のあるバージョンのパッケージをインストールする
    - 自前で対応する