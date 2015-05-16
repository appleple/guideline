#JavaScript コーディングガイドライン

##グローバル変数を使用しない

変数同士が衝突して思わぬバグにつながる可能性があるから。
変数を宣言する時は必ず```var```をつけてください。

##なるべく無名関数でソースを括る

例

```javascript
(function(){
	//処理
})(jQuery);

```

##インデントはタブで4文字分
CSSやHTMLのコーディングルールとあわせて統一性を持たせる

##変数名はlower camelで宣言
CSSやHTMLのコーディングルールとあわせて統一性をもたせる

例

```javascript
var isActive = false;
```

##数字や文字列の比較では厳密等価演算子を使う
厳密等価演算子の方が等価演算子

例
```javascript
if(string === "hoge"){
	//処理
}
```
##for文で、配列を使う場合は最初に配列の長さを変数に格納しておく
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
##jQuery

###プロトタイプチェーンをなるべくつなげる

要素を既に取得済みのため処理が早くなるから

例

```javascript
$(".hoge").addClass("active")
		.removeClass("disable")
		.hide();
```

###複数回要素を使用する場合は最初に変数にデータを格納しておく
$(セレクタ)の処理に時間がかかるため

例

```javascript
var $hoge = $(".hoge");
$hoge.func();
/*処理*/
$hoge.func();
```

