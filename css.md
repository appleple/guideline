#CSS

## 1 エントリー内のタグのCSS 
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

## 2 (CSS / JS) 必要なCSS 
読み込むスタイルファイル `acms-admin.css` `acms.css`（ユニット表示しない場合は読み込まなくてもOK）acms.cssは使用テーマ内にコピーして持ってくるsassを使っている場合は acms.scss をimportすること。acms.scssでは下記をimportする。

```scss
@import "../../../../system/scss/functions.scss";
@import "../../../../system/scss/variable.scss";
@import "../../../../system/scss/mixins.scss";
@import "../../../../system/scss/grid.scss";
@import "../../../../system/scss/unit.scss";
```
> acms-admin.css にユニットのスタイルも入っているが、アップデートされるファイルなのでacms.cssも読み込んでおく必要がある。

## 3 コメント
### 3.1 基本的な場合は以下のようにコメントを記述する
```scss
// ------------------------------ 
//  大見出し
// ------------------------------

// 中見出し
//===============================

// 小見出し
```
### 3.2 CSSに出力すべきものは以下のようにコメントを記述する
```scss
/* ------------------------------ 
  大見出し
 ------------------------------ */

/* 中見出し
=============================== */

/* 小見出し */
```
### 3.3 各SCSSファイルの冒頭には必ずCSS出力用の大見出しを記述すること。
もしCSSファイルのみになってもメンテナンス性・可読性をよくするための最低限の対応です。

例）ヘッダー
```scss
/* ------------------------------
　　ヘッダー
------------------------------ */
.head-wrapper {
	padding: 40px 0 0 0; 
}
/* サイト名 */
.header-logo {
	float: left;
	margin: 0 0 10px 0; 
}
...
```
## 4 メディアクエリー
メディアクエリーは変数で管理すること。少しでも数値にずれがあれば一部のデバイスでは意図しない表示になる恐れがあるため。

例）variables.scss
```scss
//min-width指定
$breakpoint-sm-min : 480px;
$breakpoint-md-min : 768px;
$breakpoint-lg-min : 1024px;
$breakpoint-xl-min : 1440px;

//max-width指定
$breakpoint-sm-max: ($breakpoint-sm-min - 1); //479px
$breakpoint-md-max: ($breakpoint-md-min - 1); //767px
$breakpoint-lg-max: ($breakpoint-lg-min - 1); //1023px
$breakpoint-xl-max: ($breakpoint-xl-min - 1); //1439px
```
例）使用例
```scss

// max-widthの例
@media (max-width : $breakpoint-md-max) {
  .header {
   ...
  }
}
@media (max-width : $breakpoint-sm-max) {
  .header {
   ...
  }
}

// min-widthの例
@media screen and (min-width: $breakpoint-sm-min){
  .header {
   ...
  }
}
@media (min-width : $breakpoint-md-min) {
  .header {
   ...
  }
}
```

## 5 if文、each文、for文などの使用注意
プログラム的な書き方はメンテナンスをよくするのに効率が良くなりますが、後々ノンプラグラマーの人間が管理する可能性もあります。
使用する際はわかりやすくコメントを書くよう気をつけて使用してください。

## 6 extendの使用注意
extendを使うのは悪いことではありませんが、extendの中にextendを使用しないこと。
階層が深くなってしまうと、効率が悪くなり、メンテナンスがやりにくくなる可能性があります。