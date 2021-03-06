# a-blog cms

## 目次

1. 命名規則
2. テーマの作り方
3. 入力系UIや管理用パーツ等


## 1.命名規則

### 1.1 a-blog cmsの変数名
変数名の単語の接続はスネークケース（ `_` ）で行う
```
<p>{ogp_image@path}</p>
```

### 1.2 ブログ、カテゴリーコードの命名
カテゴリーやブログコードの単語の接続はケバブケース（ `-` ）。
> URLに反映されるときに `_` だと見にくくなるので `-` を使うようにする。

### 1.3 カスタムフィールドグループの命名
CFGのときは `group_〇〇` にする単純な名前はつけない（絶対に `_` をつけるようにする）
> 単純な命名規則である場合、他の箇所と変数名がかぶる可能性があるため。

### 1.4. グローバル変数の命名
カスタマイズしたグローバル変数は全部大文字で書く。単語の接続はスネークケース（ `_` ）かつ、 `CUSTOM` を接頭辞につける
> a-blog cmsの公式の命名規則に合わせる。 `CUSTOM_` とつけることで、拡張したグローバル変数か判断するため。

NG
```
%{NEXT_MONTH}
```

OK
```
%{CUSTOM_NEXT_MONTH}
```
### 1.5 校正オプションの命名
カスタマイズした校正オプションは全部小文字で書く単語をつなげるときはキャメルケースかつ、 `custom` を接頭辞につける
> a-blog cmsの公式の命名規則に合わせる。 `custom` とつけることで、拡張した校正オプションか判断するため。

NG
```
{date}[next_month]
```

OK
```
{date}[customNextMonth]
```
### 1.6 ファイル名の命名
ファイル名やフォルダ名の単語の接続はケバブケース（ `-` ）で書く。（モジュール名が入っていてもハイフンにする、画像もハイフン）
> URLに反映されるときに `_` だと見にくくなるので `-` を使うようにする。

### 1.7 HTMLで検索されたくないファイル名の命名
直接表示したくないテンプレートは、ファイル名の最初にアンダーバーをつける（`include/_entry.html`, `_layouts/`）
> 意図しないテンプレートを表示させないため。

### 1.8 モジュールIDの命名

#### 1.8.1 モジュールには基本的にIDをつける

NG
```
<!-- BEGIN_MODULE Entry_Body -->

<!-- END_MODULE Entry_Body -->
```

OK
```
<!-- BEGIN_MODULE Entry_Body id="body_common" -->

<!-- END_MODULE Entry_Body -->
```


#### 1.8.2 全般
モジュールIDは モジュール名_使用場所名（コンテンツの種類） のように命名する。基本的に全て小文字。

お知らせブログ（ブログコード「news」）で使用されるEntry_Bodyの場合
```
<!-- BEGIN_MODULE Entry_Body id="body_news" -->
```

#### 1.8.3 エントリー系
Entry系の時は、「entry_」を省略する。

#### 1.8.4 フィールドモジュール系
フィールドモジュール表示用のモジュールIDは、モジュールフィールド `MF_〇〇` 、カテゴリフィールド `CF_〇〇` 、ブログフィールド `BF_〇〇` 、のように命名する。
> モジュールID名だけで何のモジュールでどこに使われているかわかるようにするため。機能名を含める理由は、他のモジュール使用時に被らないようにするため。



## 2. テーマの作り方

### 2.1 includeファイルなどの設置場所
管理テンプレートやインクルードファイルは理由がない限りルートテーマに作成する
> テンプレートの探しやすさを上げることと、1つのテンプレートを応用しやすくするため

### 2.2 ルートテーマのカスタマイズ
BID1の時は例えば、 `root@site2019` のようなテーマを用意する
> ルートテーマを継承する子テーマを使用した場合、意図しないカテゴリーのテンプレートが表示されてしまうため。

### 2.3 テンプレートの継承
`_layouts` にベーステンプレートを置いて、継承するやり方で作っていく
> レイアウトの変更に強くなるため

### 2.4 モジュールIDのテンプレート変数化
インクルードファイル化したテンプレートで、モジュールIDはインクルード変数で指定するようにする。
```js
@include("/_include/entry/summary.html", { module_id: "entry_common" })
```
> 同じモジュールを使い回すときでも、モジュールIDが変更される可能性は高いので、モジュールIDの依存性をテンプレートから除外するため

### 2.5 カスタムフィールドの記述にはedit.htmlを使わない
`/admin/xxx/field.html` か `/admin/xxx/field_foot.html` にカスタムフィールドの記述をする。（旧 `edit.html` は使わない）

### 2.6 テンプレートの分岐
テンプレートを分岐する時は、IFブロックではなくグローバル変数を使う
> IFブロックは実行順序があとになるので、表示速度が遅くなってしまう可能性がある

NG
```
<!-- BEGIN_IF [%{BCD}/eq/news] -->
@include("/include/field/bcd/news.html")
<!-- END_IF -->
```

OK
```
@include("/include/field/bcd/%{BCD}.html")
```
### 2.7 カスタムユニット
カスタムユニットを作る時は `extend.html` で作成する（ `custom.html` は非推奨）
> 拡張でないカスタムユニットは1つしか作れないので

### 2.8 Entry系モジュールの使用について
`Entry_Body` ではなくなるべく `Entry_Summary` をつかう
> Entry_Body は表示速度が遅くなるので。

### 2.9 Set_Template 非推奨
インクルードで対応できる場合は、Set_Template は使わない


### 2.10 カスタムフィールドの設置場所

#### 2.10.1 モジュールのカスタムフィールド
モジュールのカスタムフィールドは以下のように読み込むようにする。
```
@include("/admin/module/id_%{MODULE_ID}.html")
```
> モジュールIDに対するカスタムフィールドの設定がどこに書かれているかわかりやすくするため

#### 2.10.2 その他のカスタムフィールド
特定のブログ・カテゴリー・エントリーのカスタムフィールドを読み込むときは、コードの種類をカテゴリにし、コード名を含めてファイルを分岐する。
```
@include("/admin/blog/bcd/%{BCD}.html")
@include("/admin/category/rccd/%{RCCD}.html")
@include("/admin/category/ccd/%{CCD}.html")
@include("/admin/entry/ecd/%{ECD}")
```

ブログコードで階層化している場合には、その分フォルダを作ることになる。

階層化により、ブログコードが「root/child」だった場合のフォルダ構成の例：

/themes/〇〇/admin/blog/root/child.html


> ID名よりコード名のほうが、ファイル名だけで内容がわかりやすいため。

#### 2.10.3 共通のカスタムフィールド設置場所
共通のカスタムフィールドは `field-〇〇.html` にする
```
@include("/admin/category/field-ogp.html")
```
> ファイルの一覧を揃えるため

### 2.11 systemテーマ
systemテーマはアップデート時に更新される可能性があるので極力書き換えないようにする



## 3. 入力系UIや管理用パーツ等

### 3.1 優しさボタン
特別な理由がない限り、更新者が更新できる箇所は閲覧画面から変更ボタンを設置する。納品時にそのボタンを残すかは案件ごとに判断する。
`@include("/admin/module/setting.html")` という名前で空ファイルを設置すれば消せるようにしておく。

### 3.2 アクションボックス
納品前に管理ボックス内に設置する必要な編集ボタンをディレクターに確認する

### 3.3 SEO設定ボックス
SEO設定のカスタムフィールド、SEO確認用テンプレートを全てのページで読み込む。

### 3.4 画像のリサイズ
表示側の校正オプションで `resizeImg` を使うときは推奨サイズを記入する

例）〇〇x〇〇推奨

### 3.5 テキスト入力
テキストエリアのカスタムフィールドはデフォルトか `LiteEditor` で統一する
> お客さんが入力方法を混乱してしまうため。
