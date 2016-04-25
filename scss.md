基本的にはこのコーディングガイドラインはプロジェクトを円滑に進めるためのガイドラインとして作成されています。
もし、プロジェクトの制作方法に合わない・メンテナンス性が落ちる場合はプロジジェクトごとにガイドラインを別途作成します。

ファイル構成
------

* _normalize.scss ... 規準化
* _variables.scss ... 変数集
* _mixins.scss ... mixin集
* _extends.scss ... extend集

###ベース
* _base.scss ... 全体のベースとなるスタイル。body、aタグなど

###レイアウト
* _layout.scss ... レイアウト

###パーツ
* _type.scss ... 見出し、リスト、段落など
* _button.scss ... ボタン
* _table.scss ... テーブル
* _navbar.scss ... ナビゲーション
* _label.scss ... ラベル

###モジュール
* _header.scss ... ヘッダー
* _footer.scss ... フッター

* _module.scss ... モジュール
* _list.scss ... リスト
* _summary.scss ... サマリー
* _headline.scss ... ヘッドライン

###コンテンツ
* _entry.scss ... エントリー作成画面、ユニット
* _form.scss ... お問い合わせフォームなど

* _edit_page.scss ... CMSの編集画面

基本的には、パーツ、モジュール、コンテンツごとにファイルを作成する

コメント
--
基本的な場合は以下のようにコメントを記述する
```scss
// ------------------------------ 
//  大見出し
// ------------------------------

// 中見出し
//===============================

// 小見出し
```
CSSに出力すべきものは以下のようにコメントを記述する
```scss
/* ------------------------------ 
  大見出し
 ------------------------------ */

/* 中見出し
=============================== */

/* 小見出し */
```
CSSのみになってもメンテナンス性・可読性をよくするための最低限の対応として、各SCSSファイルの冒頭には必ずCSS出力用の大見出しを記述すること。

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

メディアクエリー
--
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

if文、each文、for文などの使用注意
------
プログラム的な書き方はメンテナンスをよくするのに効率が良くなりますが、後々ノンプラグラマーの人間が管理する可能性もあります。
わかりやすくコメントを書くよう気をつけて使用してください。

extendの使用注意
------
extendを使うのは悪いことではありませんが、extendの中にextendを使用しないこと。
階層が深くなってしまうと、効率が悪くなってしまう可能性があります。

