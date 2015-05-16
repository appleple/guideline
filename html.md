## 外部ファイルの読み込む

//から読み込む。https://のときにパスの変換回避

```html
    // OK
    <script src="//www.example.com/hoge.js"></script>

    // NG
    <script src="http://www.example.com/hoge.js"></script>
```

## HTMLの要素やプロパティはすべて小文字で記述する

```html
    <img src="demo.png" alt="Demo">
```

## 属性の優先度

その要素が何の情報もっているか優先して順番に書きます

1.  src属性、href属性
2.  width属性
3.  height属性
4.  id属性（省略可）
5.  class属性（省略可）
6.  alt属性
7.  title属性（省略可）
8.  target属性（省略可）
9.  rel属性（省略可）


```html
    <img src="demo.png" width="400" height="200" id="demo" class="banner" alt="Demo">

    <a href="download.html" id="demo" class="btn" title="ダウンロード" target="_blank" rel="download">ダウンロード</a>
```

## 文字コードはUTF-8にする

```html
    <meta charset="utf-8">
```

## CSSとJavaScriptのtype属性は省略する

type="text/css"、type="text/javascript"です。

```html
    // OK
    <link href="//www.example.com/css/hoge.css" rel="stylesheet">
    <script src="//www.example.com/js/hoge.js"></script>
```

## HTMLバリデート

- [Nu Html Checker](http://validator.w3.org/nu/)