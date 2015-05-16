ファイル構成
------

* normalize.less ... 規準化
* variable.less ... 変数集
* mixin.less ... mixin集
* acms.less ... エントリー作成画面、ユニット
* grid.less ... グリッドシステム
* button.less ... ボタン
* type.less ... 見出し、リスト、段落など
* code.less ... コード
* form.less ... フォーム
* table.less ... テーブル
* navbar.less ... ナビゲーション
* sidebar.less ... サイドナビゲーション
* label.less ... ラベル
* topicpath.less ... トピックパス
* pager.less ... ページャー
* alert.less ... アラート
* dropdown.less ... ドラップダウン
* progress-bar.less ... プログレスバー
* tab-select.less ...タブセレクト
* fonts.less ... フォント

変数
--

文字列に@をつける

```less
@color-link: #333333;
@img-path: '../images/';
```

コメント
----

2種類ある

```less
// 書き出しても残らない 開発用のメモ書きなど

/* 書き出しても残る */
```

ネスト
---

モジュール単位で入れ子にして書きます。

```less
.acms-form{
	font-size: 1.4em;
	select{
		border: solid 1px #CCCCCC;
	}
}
```

### 隣接セレクタ

.acms-form select + lable

```less
.acms-form{
	font-size: 1.4em;
	select{
		border: solid 1px #CCCCCC;
		+ lable{
			margin-right: 10px;
		}
	}
}
```

### 子セレクタ

.acms-form lable > input

```less
.acms-form{
	font-size: 1.4em;
	lable{
		display: block;
		> input{
			margin-right: 10px;
		}
	}
}
```

### 親セレクタを参照

a:hover

```less
a{
	color: #333333;
	&:hover{
		color: #CCCCCC;
	}
}
```

### メディアクエリ

メディアクエリしたいセレクタにネストする

```less
.acms-form{
	width: 100%;
	@media screen and (max-width: 640px;){
		width: auto;
	}
}
```

四則演算
----

+ - * / が使えます。

mixin
-----

よく使うプロパティをまとめることができます。引数を設定して値を上書きもできます。ベンダープレフィックスも一行にまとめれる

.mixin名（引数: 値, 引数: 値...）{ プロパティ }

```less
.gradient(@color: #F5F5F5, @start: #EEEEEE, @stop: #FFFFFF) {
	background: @color;
	background: -webkit-gradient(linear,left bottom,left top,color-stop(0, @start),color-stop(1, @stop));
	background: -ms-linear-gradient(bottom,@start,@stop);
	background: -moz-linear-gradient(center bottom,@start 0%, @stop 100%);
	background: -o-linear-gradient(@stop, @start);
	filter: e(%("progid:DXImageTransform.Microsoft.gradient(startColorstr='%d', endColorstr='%d', GradientType=0)",@stop,@start));
}

.acms-btn{
	.gradient(#FFFFFF, #FFFFFF, #DDDDDD);
}
```

* http://lesselements.com/
* http://gihyo.jp/design/serial/01/less/0006
* http://markdotto.com/bootstrap/
* http://lessprefixer.com/
* http://takahiro.me/archives/257
* http://www.yoheim.net/blog.php?q=20130411
* http://clearleft.github.io/clearless/


関数
--

### round()：小数点を四捨五入

### ceill()：小数点を切り上げ

### floor()：小数点を切り捨て

```less
@width: 250px;

.acms-form-width-medium{
	width: round(@width / 3); // 小数点を四捨五入
	width: ceill(@width / 3); // 小数点を切り上げ
	width: floor(@width / 3); // 小数点を切り捨て
}
```

### rgba()：カラーの16進数をrgbに変換

```less
.acms-form input[type="text"]:focus{
	box-shadow: rgba(#333333, 0.5); // rgba(51, 51, 51, 0.5);
}
```

カラー関数
-----

### 
```less
// 明度
lighten(@color, 10%);
darken(@color, 10%);

// 彩度
saturate(@color, 10%);
desaturate(@color, 10%);

// 透明度
fadein(@color, 10%);
fadeout(@color, 10%);
fade(@color, 50%);

// 色相
spin(@color, 10);
spin(@color, -10);

// 色をミックス
mix(@color1, @color2);
```

フラグ
---

### !optional

コンパイル後に警告を出さなくする

### !デフォルト

コンパイル後に警告を出さなくする