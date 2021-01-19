## 用語説明

---

#### CI

- Continuous Integration の略で、継続的インテグレーションと呼ばれる.
- 開発者が自分のコード変更を頻繁にセントラルリポジトリにマージし、その度に自動化されたビルドとテストを実行します.
- 要は commit ごとに build 検証していく.

#### ESLint

- js のための静的検証ツール(ソースコードをみて正しいか検証する)
- ファイル内のバグチェックやコーディングスタイルの一貫性を保つ

#### Prettier

- コードフォーマッター

## パッケージインストール

`npm install --save-dev eslint eslint-config-prettier prettier @typescript-eslint/parser @typescript-eslint/eslint-plugin husky lint-staged`
