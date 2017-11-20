# CSS

## 使用 inline js 延遲載入 css

#### 1. 設定 link style 的 media 為 `none`

```html
<link rel="stylesheet" href="css.css" media="none">
```

#### 2. css 載入中置換 media 屬性為 `all`

```html
<link rel="stylesheet" href="css.css" media="none" onload="if(media!='all')media='all'">
```

#### 3. 在不支援 js 延遲載入的瀏覽器，使用預設方式載入（選擇性支援）


## 使用 js 延遲載入 css

```javascript
var resource = document.createElement('link');
resource.setAttribute("rel", "stylesheet");
resource.setAttribute("href","path/to/cssfile.css");
resource.setAttribute("type","text/css");
var head = document.getElementsByTagName('head')[0];
head.appendChild(resource);
```

```html
<link rel="stylesheet" href="css.css" media="none" onload="if(media!='all')media='all'"><noscript><link rel="stylesheet" href="css.css"></noscript>
```


## 使用不存在的 media 預先載入 css

```html
<head>
  <!-- unimportant nonsense -->
  <link rel="stylesheet" href="style.css" media="none"/>
</head>
<body>
  <!-- other unimportant nonsense, such as content -->
  <link rel="stylesheet" href="style.css"/>
</body>
```

瀏覽器在遇到不存在的 media 時，不會將頁面 block 住，還是會在背景預先載入此 css，避免在使用者操作過程中，旋轉了瀏覽裝置，導致需要像是 `media="(min-width:500px)"` 與 `media="print"` 情境的 css，所以就算目前不需要此 css 渲染畫面，但還是會預先載入。

可以運用這個特性，在 `<head>` 使用不存在的 `media` 屬性，預先載入此 css。

在 `body` 結尾時，再正式告訴瀏覽器，請使用這個 css 去渲染畫面，而此 css 在先前就已經在背景偷偷載入了，所以在渲染畫面時，就可以立即渲染，不需要再等待載入的時間，達到非同步預先載入 css 的效果。



## 參考資料
* [html - How to load CSS Asynchronously - Stack Overflow](https://stackoverflow.com/questions/32759272/how-to-load-css-asynchronously)
* [“Async” CSS without JavaScript by Taylor Hunt on CodePen](https://codepen.io/tigt/post/async-css-without-javascript)
* [Programmatically disable or enable a CSS stylesheet with JS | Code Chewing Guides](https://guides.codechewing.com/js/disable-enable-stylesheet-javascript)