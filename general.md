# コード全般 

CSS / JSについてはルールを書いても忘れてしまうので、できれば `Node.js` の環境を整備すること。`Node.js` 製のツールで強制的にルールを適応できる<br/>
詳しくはこちらのレポジトリを参照<br/>
https://github.com/appleple/a-starter-kit

## 1. a-starter-kitのルール適応方法

1.1 テーマフォルダに移動

開発したいテーマに移動します。<br/>
例）`themes/original-theme`など

1.1 git clone
その場で `git clone`します。
```bash
$ git clone git@github.com:appleple/a-starter-kit.git .
```
`npm install`で必要なツールをインストールします。

1.2 npm install
```
$ cd ./path/to/a-starter-kit
$ npm install
```

1.3 開発
以下のコマンドを入力して開発を始めましょう。
```
$ npm run dev
```
