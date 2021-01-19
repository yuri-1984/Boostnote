## 用語説明
---
#### webpack
* モジュールバンドラ　
* 依存関係を考慮しながらjsを1ファイルにまとめることができる

#### typescript
* コンパイラを使用
* typescriptで書いたコードをjsに変換
* 新しい構文を古いブラウザでも動かせる


#### typescript build の仕組み
* .tsファイルをtsでコンパイルする->.jsファイルへと変換される->webpackが一つのファイルにバンドルする（これをwebアプリとして読み込んでいる）

#### 各パケージの役割
* typescript :ts構文をjs構文に変換するコンパイラ
* ts-loader  :webpackと連動してtsコンパイラを起動
* webpack :複数のファイルを一つにまとめる
* wbpack-cli :コマンドラインでwebpackを使用
* webpack-dev-werver :webpackのビルド、開発用webサーバーの起動,ホットリロード（ファイル変換の自動検知と再読み込み）

#### tsconginの基本的な設定項目

| 設定項目名 | 初期値 | 意味 |
| ---------- | ------ | ---- |
| target | es5(IE11で動く) | コンパイル後のjsバージョン(allowはes6から) |
| module | commonjs(node.jsでモジュール扱える) | どの方式でモジュール関連のコードを扱うか |
| strict | true | tsの基本的なチェックを全てtureにするか |
| esModuleInterop | true | import文を使って読み込め流ようにするか |
| forceConsistentCasingInFileNames | true | ファイル名の大小を区別するか |
| allowjs | true | jsファイルを許容するか |
| jsx | preserve | jsxファイルをどうコンパイルするか |
| lib | [] | 使用するjsライブラリ |
| outDir | ./ | ビルド結果の出力先 |
| baseUrl | ./ | import分のベースパス(絶対パスを使える) |

## node環境の構築
---
1. `node -v` でバージョンを確認する(表示されない場合はnodeインストールする必要あり)
1. `brew --version` (homebrewを確認するなければインストール )
1.` brew install nodebrew `:インストール
1. `nodebrew -v` :バージョン確認(currentが現在使用しているバージョン)-> `nodebrew install stable`でインストールできる ->nodebrew use v8.9.4 で使用することができる
1. bashでnodeのパスを通す（`echo 'export PATH=$HOME/.nodebrew/current/bin:$PATH' >> ~/.bash_profile`）->ターミナルを再起動する
1. `node -v` ,`npm-v`でバージョンを確認する

## typescript環境の構築
1. 開発環境用のディレクトリに移動する
1. 開発用のファイルに移動したら `npm init` でnpmパッケージの初期化を行う(全てy)
1. 関連パッケージをインストール`npm install --save-dev typescript ts-loader webpack webpack-cli webpack-dev-server`:--save-dev開発環境でしか使わない場合はこのオプションを使う
1. webpack.config.jsを作成
```
//{}を書くとこの中の記述がwebpackの設定になる
const path = require("path");
module.exports = {
  entry: {
    //エントリポイントはwebpackの起点になる場所なので記述が必要
    bundle: "./src/index.ts",
  },
  //一つにまとめたファイルをどこに出力するかの設定
  output: {
    path: path.join(__dirname, "dist"),
    //bundleと紐付ける
    filename: "[name].js",
  },
  resolve: {
    extensions: [".ts", ".js"],
  },
  //開発用のサーバの設定
  devServer: {
    contentBase: path.join(__dirname, "dist"),
    //勝手にブラウザを開いてくれる
    open: true,
  },
  module: {
    rules: [
      {
        loader: "ts-loader",
        test: /\.ts$/,
      },
    ],
  },
};
```
1.package.jsonを変更
1. `tsc --init` 実行(typescript　コンパイルを初期化)
