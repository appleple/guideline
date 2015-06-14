#JavaScript コーディングガイドライン

##項目

  1. [変数](#変数)
  1. [セミコロン](#セミコロン)
  1. [インデント](#インデント)
  1. [演算子](#演算子)
  1. [for文](#for文)
  1. [オブジェクト](#オブジェクト)
  1. [コンストラクタ](#コンストラクタ)
  1. [jQuery](#jQuery)

##変数

 - [1.1](#1.1)なるべくグローバル変数を使用しない
変数同士が衝突して思わぬバグにつながる可能性があります。
変数を宣言する時は必ず```var```をつけてください。

 - [1.2](#1.2)変数名はローワーキャメル形式で宣言
CSSやHTMLのコーディングルールとあわせて統一性をもたせる

##セミコロン

 - [2.1](#2.1)セミコロンがないと、jsファイルを圧縮した際に致命的なバグが発生する場合があります。



##インデント
 - [3.1](#3.1)インデントはタブで4文字分
CSSやHTMLのコーディングルールとあわせて統一性を持たせる


例

```javascript
var isActive = false;
```

##演算子
 - [4.1](#4.1)数字や文字列の比較では厳密等価演算子を使う
厳密等価演算子の方が等価演算子

例
```javascript
if(string === "hoge"){
	//処理
}
```
##for文
 - [5.1](#5.1)for文で、配列を使う場合は最初に配列の長さを変数に格納しておく。
arrayのlengthプロパティに何回もアクセスすると処理速度に影響が出るため

悪い例
```javascript
for(var i = 0; i < array.length; i++){
	//処理
}
```
良い例
```javascript
for(var i = 0, length = array.length; i < length; i++){
	//処理
}
```

##オブジェクト

 - [6.1](#6.1)オブジェクトの指定方法
オブジェクトの指定は見やすいように下の「良い例」のように記述するようにしましょう

良い例
```javascript
var map = {
	hoge: "hogehoge",
	test: "testtest"
}
```

悪い例
```javascript
var map = {hoge: "hogehoge",
test: "testtest"}
```

 - [6.2](#6.2)プロパティの削除にdeleteは使わない
プロパティの削除より、nullを代入する方が処理が速いため

良い例
```javascript
obj.hoge = null;
```

悪い例

```javascript
delete obj.hoge
```

##コンストラクタ
 - [7.1](#7.1)コンストラクタの後には()をつける

良い例
```javascript
var obj = new Hoge();
```

悪い例

```javascript
var obj = new Hoge;
```

 - [7.2](#7.2)ただしObjectとArrayは例外
newをつけずに{}や[]で宣言します。


悪い例

```javascript
var obj = new Object();
var arr = new Array();
```

良い例

```javascript
var obj = {};
var arr = [];
```

##jQuery

 - [8.1](#8.1)jQueryの変数はなるべく$をつける
一般的な変数と区別するため

例

```javascript
$table = $("table");
```

 - [8.2](#8.2)プロトタイプチェーンをなるべくつなげる

要素を既に取得済みのため処理が早くなるから

例

```javascript
$(".hoge").addClass("active")
		.removeClass("disable")
		.hide();
```

 - [8.3](#8.3)複数回要素を使用する場合は最初に変数にデータを格納しておく
$(セレクタ)の処理に時間がかかるため

例
```javascript
var $hoge = $(".hoge");
$hoge.func();
/*処理*/
```

