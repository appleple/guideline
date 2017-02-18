基本的なファイル構成
------
* top.html
* index.html
* entry.html
* 404.html


基本的なフォルダ構成
------
* /admin/・・・管理画面で使用しているファイル
* /include/・・・インクルード機能を使用して読み込まれているファイル
* /vars/ ・・・ テンプレートの変数化（Set_Template、Set_Rendered）

### テンプレートの分岐の際に使用するIDとコードについて
テンプレートを分岐する際、ブログコードやブログIDなどを使用しますが、予測のしやすさを重視し、基本的に使用するものはコードとします。

例）カテゴリーコードの例
```html
<!-- 各カテゴリー別 -->
<!--#include file="/admin/category/ccd_%{CCD}.html" -->
```

ただし、以下のような場合はIDを使用する
* 頻繁にコードを変更する可能性がある場合
* ブログコードに「/」が混ざっている場合

コメント
------

インクルード文や、変数化したテンプレートを読み込む際は予測しやすいようにコメントを記述する

例）インクルードの例
```html
<!-- ヘッダー -->
<!--#include file="/include/header.html" -->
```
例）変数化したテンプレートの例
```html
<!-- お知らせ -->
<!-- GET_Template id="headline" module_id="news" -->
```

変数名
------
変数名は「_（アンダーバー）」を使って単語を区切る

* モジュールID名
* カスタムフィールド名

モジュールIDの記述
```html
<!-- お知らせ -->
<!-- BEGIN_MODULE Entry_Summary id="summary_news" -->
```
カスタムフィールドの記述
```html
<input type="text" name="summary_title" value="{summary_title}"/>
<input type="hidden" name="field[]" value="summary_title" />
```
