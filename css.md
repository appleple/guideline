## インデント

タブのサイズは4  
タブとスペースを混在させる避ける

```
"tab_size": 4
```

## プロパティの記述順

プロパティの順番は[CSScomb](https://github.com/csscomb/csscomb.js)の順番にする

[実際の順番はこのように](https://github.com/csscomb/csscomb.js/blob/master/config/csscomb.json)なっています。

[Sublime text 2のプラグイン](http://dev.classmethod.jp/tool/csscomb/)もあるようです

## ブラウザのベンダープレフィックスの順番

1.  -moz-
2.  -webkit-
3.  -o-
4.  -ms-

```css
-moz-border-radius: 4px;
-webkit-border-radius: 4px;
-o-border-radius: 4px;
-ms-border-radius: 4px;
border-radius: 4px;
```

## カラーコード

英語は大文字で記述してください。

\#FFFFFFは#FFFに省略できるのですが、3桁に省略できないコードは6桁にします。  
Fireworksは英語が大文字です。

```css
// OK
.hoge{
    color: #FFFFFF;
}

// NG
.hoge{
    color: #fff;
}
```

## コメントの書き方

### 大見出し
```css
/* ---------------
コメント
--------------- */
```

### 小見出し
```css
/* コメント */
```

## 命名規則

* 文章構造上、意味のある名前にすること。
* ローワーキャメル方式（複合語の先頭を、小文字で書き始める）で命名すること。
* 英数字で記述し、ハイフン、アンダーバーは使用しないこと。（IE6対応のみアンダーバーを許可）
* 数字は先頭に使用しないこと。

### 通常
```css
// OK ローワーキャメル
.itemName {}

// NG ハイフン
.item-name {}

// NG アンダーバー
.item_name {}
```

### a-blog cmsのCSSフレームワーク

クラス名の別々の単語はハイフンで繋ぐ。

既にあるCSSのclass名と衝突を防ぐために「.acms-個別名」にします。

```css
.acms-btn {}
```

## CSSに要素を書かない

要素に依存せず汎用背の高い書き方にしましょう。

```css
// OK
.error {}

// NG
p.error {}
```

## プロパティの値はまとめる

プロパティの書く順番：上 - 右 - 下 - 左

```css
// OK
div{
    padding: 0 1em 2em 1em;
}

// NG
div{
    padding-top: 0;
    padding-right: 1em;
    padding-bottom: 2em;
    padding-left: 1em;
}
```

### a-blog cmsのCSSフレームワーク

上書きしやすいように使わないプロパティは最低限書かないようにしてください。

```css
// 左右のpaddingを指定しないときは書かないようにしてください。
// まとめてしまうと後から上書きできなくなってしまいます。
div{
    padding-top: 0;
    padding-bottom: 2em;
}
```

## 値が0のときは単位を省力する

```css
// OK
padding: 0;

// NG
padding: 0px;
```

## プロパティの値の後ろにセミコロン（;）を入れる

```css
// OK
display: block;
```

## プロパティの後ろにコロン（:）のあとに半角スペースを入れる

```css
// OK
font-weight: bold;

// NG
font-weight:bold;
```

## セレクタを複数書くときは改行する

```css
// OK
h1,
h2 {}

// NG
h1, h2 {}
```

## !importantは基本的に利用しない

## レスポンシブ

メディクエリーは該当する要素のすぐ後ろに記述する

どの要素にメディアクエリを当てているか明確にするため。

スマートフォンを基準にする（対応ブラウザにIE8が含まれていたら要注意）

```css
/* 480px以上のとき */
@media screen and (min-width: 480px) {
	.entry{
		width: 440px;
		margin: 0 0 20px;
	}
}
/* 980px以上のとき */
@media screen and (min-width: 980px){
	.entry{
		width: 940px;
	}
}
```