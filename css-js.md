## コード全般 CSS / JS

CSS / JSについてはルールを書いても忘れてしまうので、できれば `Node.js` の環境を整備すること。`Node.js` 製のツールで強制的にルールを適応できる<br/>
詳しくはこちらのレポジトリを参照<br/>
https://github.com/appleple/a-starter-kit


## editorconfig使用 

a-starter-kit の .editorconfig に準ずる　・html/css/js インデントはスペース2つ　・php インデントはスペース4つ</td>

> 記述方法の共通化のため

## stylelint使用 

CSSはa-starter-kitのstylelintrcに準ずる 同梱されているwebpackで自動で適応される

## eslint使用 

JSはa-starter-kitのeslintrcに準ずる 同梱されているwebpackで自動で適応される

## `js-`の接頭辞 

jsが適用される要素には`js-`の接頭辞をつける


## エントリー内のタグのCSS 

エントリー内のHTMLタグ自体にスタイルを適用する。

### NG

```css
.acms-entry p.paragraph {

}
.acms-entry h1.title {

}
```

### OK
```css
.acms-entry p {

}
.acms-entry h1 {

}
```

> マークダウンや、WYSIWYGで投稿されても使えるようにするため。エントリー内のHTML要素のスタイルはマークダウンで投稿されたことを考慮する。

## (CSS / JS) 必要なCSS 

読み込むスタイルファイル `acms-admin.css` `acms.css`（ユニット表示しない場合は読み込まなくてもOK）acms.cssは使用テーマ内にコピーして持ってくるsassを使っている場合は acms.scss をimportすること。acms.scssでは下記をimportする。

```scss
@import "../../../../system/scss/functions.scss";
@import "../../../../system/scss/variable.scss";
@import "../../../../system/scss/mixins.scss";
@import "../../../../system/scss/grid.scss";
@import "../../../../system/scss/unit.scss";
```

> acms-admin.css にユニットのスタイルも入っているが、アップデートされるファイルなのでacms.cssも読み込んでおく必要がある。

# }