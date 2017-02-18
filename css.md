## インデント

タブのサイズは4  
タブとスペースを混在させる避ける

```
"tab_size": 4
```

## プロパティの記述順

プロパティの順番は[CSScomb](https://github.com/csscomb/csscomb.js)で設定できる、.csscomb.jsonの順番に従う。
[gulp-csscomb](https://www.npmjs.com/package/gulp-csscomb)というgulpのプラグインをつかって対応します。
（※.csscomb.jsonはアップルップルのスターターキットレポジトリ（近日作成予定）を参照します）

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

```css
// NG
.hoge{
    color: #FFFFFF;
}

// OK
.hoge{
    color: #FFF;
}
```

## コメントの書き方

### 大見出し
```css
/* ------------------------------
　　コメント
------------------------------ */
```

### 中見出し
```css
/*  コメント
------------------------------ */
```

### 小見出し
```css
/* コメント */
```

## 命名規則

* 意味のある名前にすること
* 「-（ハイフン）」繋ぎで命名すること
* 英数字で記述し、ローワーキャメル方式（複合語の先頭を、小文字で書き始める）は使用しないこと。（IE6対応のみアンダーバーを許可）
* 数字は先頭に使用しないこと。

### 通常
```css
// OK ハイフン
.item-name {}

// NG ローワーキャメル
.itemName {}
```

### a-blog cmsのCSSフレームワーク

クラス名の別々の単語はハイフンで繋ぐ。

既にあるCSSのclass名と衝突を防ぐために「.acms-個別名」にします。

```css
.acms-btn {}
```

## CSSに要素を書かない

極力、要素に依存せず汎用背の高い書き方にしましょう。
（その要素にしか適用したくない、という特別な理由がある場合は例外です）

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

ユーザー側がCSSを上書きしやすいように、使わないプロパティは最低限書かないようにしてください。

```css
// 左右のpaddingを指定しないときは書かないようにしてください。
// まとめてしまうと後から上書きできなくなってしまいます。
div{
    padding-top: 0;
    padding-bottom: 2em;
}
```

## 値が0のときは単位を省略する

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

メディクエリーは該当する要素が属しているコンポーネントごとのセクションの最後に記述する。

コンポーネントごとにメディクエリーの数値にバラツキがないようにするため。

基本的にはスマートフォンを基準に「min-width」で指定する（対応ブラウザにIE8が含まれていたら要注意）。
例外：「max-width」を使用したほうがCSSの上書きが少なくなる場合

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
