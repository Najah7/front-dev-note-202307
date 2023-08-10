## Atomic Design
- 元々はデザイン（デザインシステム）を構築するための方法論
- Atomic Design とは、コンポーネントを分類するための考え方
- コンポーネントの分割時の指標として使える
- デザインを５つの階層で定義することで、一貫性を保ち、管理しやすくする
- Reactのコンポーネント開発と相性がいい。

### Atomic Design の階層
| 階層名 | 説明 | コンポーネントの例 |
| --- | --- | --- |
| Atoms | 最小の要素。これ以上分解できない | ボタン、テキストボックス、ラベル、アイコン |
| Molecules | Atomsを組み合わせたもの | ラベル付きのテキストボックス |
| Organisms | AtomsやMoleculesを組み合わせたもの | ヘッダー、フッター、ナビゲーションバー、入力フォーム |
| Templates | Organismsを組み合わせたもの | ページ全体のレイアウト |
| Pages | Templatesを組み合わせたもの | ページ |

### 自分流の覚え方
- Atoms: 最小要素
- Molecules: 最小機能のUI
- Organisms: 最小機能
- Templates: ページのUI（レイアウトメイン）
- Pages: ページ with 機能