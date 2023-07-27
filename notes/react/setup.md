# プロジェクトの作成
```bash
npx create-react-app <プロジェクト名> --template typescript
```

# ディレクトリ構成
```bash
├── README.md：プロジェクトの説明
├── node_modules：パッケージのインストール先
├── package.json：パッケージの管理
├── public
│   ├── favicon.ico：favicon
│   ├── index.html：アプリケーションのエントリーポイント
│   └── manifest.json：PWAの設定
├── src
│   ├── App.css：アプリケーションのスタイル
│   ├── App.test.tsx：テスト
│   ├── App.tsx：アプリケーションのエントリーポイント
│   ├── index.css：アプリケーションのスタイル
│   ├── index.tsx：アプリケーションのエントリーポイント
│   ├── logo.svg：ロゴ
│   ├── react-app-env.d.ts：環境変数の型定義
│   ├── reportWebVitals.ts：パフォーマンスの計測
│   └── setupTests.ts：テストの設定
└── tsconfig.json：TypeScriptの設定
```