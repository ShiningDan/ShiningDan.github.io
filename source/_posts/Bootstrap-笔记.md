﻿---
title: Bootstrap 笔记
date: 2017-01-14 14:52:11
categories: coding
tags:
  - Bootstrap
---
#  Bootstrap 笔记

本系列的是参考[慕课网 大漠](http://www.imooc.com/u/104044/courses?sort=publish)老师的视频，仅供个人查阅使用，具体讲解推荐参考视频。

在 Bootstrap 的发展中，有一些样式发生了改变，在本文中分析的是较新的 Bootstrap 样式。

## 使用 Bootstrap

使用 Bootstrap，可以将文件下载到本地使用，或者使用 Bootstrap 提供的 CDN。

下面是 Bootstrap 的 CDN，最新的 CDN 可以在 [Bootstrap 官网](http://getbootstrap.com) 上下载。：

```
<!-- Latest compiled and minified CSS -->
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">

<!-- Optional theme -->
<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap-theme.min.css" integrity="sha384-rHyoN1iRsVXV4nD0JutlnGaslCJuC7uwjduW9SVrLvRYooPp2bWYgmgJQIXwl/Sp" crossorigin="anonymous">

<!-- Latest compiled and minified JavaScript -->
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js" integrity="sha384-Tc5IQib027qvyjSMfHjOMaLkfuWVxZxUPnCJA7l2mCWNIpG9mGCD8wGNIcPD7Txa" crossorigin="anonymous"></script>
```

下载的 Bootstrap 的内容格式如下，包括一些 CSS 样式和 js 文件，和一些字体文件。：

```
bootstrap/
├── css/
│   ├── bootstrap.css
│   ├── bootstrap.css.map
│   ├── bootstrap.min.css
│   ├── bootstrap.min.css.map
│   ├── bootstrap-theme.css
│   ├── bootstrap-theme.css.map
│   ├── bootstrap-theme.min.css
│   └── bootstrap-theme.min.css.map
├── js/
│   ├── bootstrap.js
│   └── bootstrap.min.js
└── fonts/
    ├── glyphicons-halflings-regular.eot
    ├── glyphicons-halflings-regular.svg
    ├── glyphicons-halflings-regular.ttf
    ├── glyphicons-halflings-regular.woff
    └── glyphicons-halflings-regular.woff2
```

** Bootstrap所有的 JS 插件都依赖于 jQuery，因此 jQuery 要在 Bootstrap 之前使用**，下面为使用 Bootstrap 的一个模板：

<!--more-->

```HTML
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">//在 IE 浏览器中运行最新的渲染模式
    <meta name="viewport" content="width=device-width, initial-scale=1">//初始化移动浏览器的显示 移动浏览器把文件放在一个虚拟的视口 viewport 中，width 用来设置 viewport 的大小为移动浏览器的大小，initial-scale 为设置页面初始缩放比例为 1 （不缩放）。一般针对移动浏览器浏览都会预先设置这一段代码。
    <!-- The above 3 meta tags *must* come first in the head; any other head content must come *after* these tags -->
    <title>Bootstrap 101 Template</title>

    <!-- Bootstrap -->
    <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <link href="css/bootstrap.min.css" rel="stylesheet">

    <!-- HTML5 shim and Respond.js for IE8 support of HTML5 elements and media queries -->
    <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
    <!--[if lt IE 9]>
    
    // 浏览器的版本低于 IE9 的浏览器兼容 HTML5 需要添加的标签
      <script src="https://oss.maxcdn.com/html5shiv/3.7.3/html5shiv.min.js"></script>
      
      // 浏览器版本低于 IE9 的浏览器兼容 CSS3 需要添加的标签
      <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
    <![endif]-->
  </head>
  <body>
    <h1>Hello, world!</h1>

    <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
    <!-- <script src="http://apps.bdimg.com/libs/jquery/2.1.4/jquery.min.js"></script> -->
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script> // jquery 在 Bootstrap 之前加载
    <!-- Include all compiled plugins (below), or include individual files as needed -->
    <!-- <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script> -->
    <script src="js/bootstrap.min.js"></script>
  </body>
</html>
```

下面是使用 Bootstrap 和不使用 Bootstrap 显示的差异：

使用 Bootstrap：

![](http://ofjjubwp5.bkt.clouddn.com/image/png/img84.png)

不使用 Bootstrap：

![](http://ofjjubwp5.bkt.clouddn.com/image/png/img85.png)

## Bootstrap 全局样式

Bootstrap 的全局样式是基于 [normalize.css](http://necolas.github.io/normalize.css/)的，并且在此基础上实现了一些改良，具体的内容如下：

* 移除body的margin声明
* 设置body的背景色为白色
* 为排版设置了基本的字体、字号和行高
* 设置全局链接颜色，且当链接处于悬浮“:hover”状态时才会显示下划线样式

在 Bootstrap 的 CSS 样式中关于全局样式的部分有：

```CSS
html {
  font-family: sans-serif;
  -webkit-text-size-adjust: 100%;
      -ms-text-size-adjust: 100%;
}
body {
  margin: 0;
}
article,
aside,
details,
figcaption,
figure,
footer,
header,
hgroup,
main,
nav,
section,
summary {
  display: block;
}
audio,
canvas,
progress,
video {
  display: inline-block;
  vertical-align: baseline;
}
audio:not([controls]) {
  display: none;
  height: 0;
}
[hidden],
template {
  display: none;
}
a {
  background: transparent;
}
a:active,
a:hover {
  outline: 0;
}
abbr[title] {
  border-bottom: 1px dotted;
}
b,
strong {
  font-weight: bold;
}
dfn {
  font-style: italic;
}
h1 {
  margin: .67em 0;
  font-size: 2em;
}
mark {
  color: #000;
  background: #ff0;
}
small {
  font-size: 80%;
}
sub,
sup {
  position: relative;
  font-size: 75%;
  line-height: 0;
  vertical-align: baseline;
}
sup {
  top: -.5em;
}
sub {
  bottom: -.25em;
}
img {
  border: 0;
}
svg:not(:root) {
  overflow: hidden;
}
figure {
  margin: 1em 40px;
}
hr {
  height: 0;
  -moz-box-sizing: content-box;
       box-sizing: content-box;
}
pre {
  overflow: auto;
}
code,
kbd,
pre,
samp {
  font-family: monospace, monospace;
  font-size: 1em;
}
button,
input,
optgroup,
select,
textarea {
  margin: 0;
  font: inherit;
  color: inherit;
}
button {
  overflow: visible;
}
button,
select {
  text-transform: none;
}
button,
html input[type="button"],
input[type="reset"],
input[type="submit"] {
  -webkit-appearance: button;
  cursor: pointer;
}
button[disabled],
html input[disabled] {
  cursor: default;
}
button::-moz-focus-inner,
input::-moz-focus-inner {
  padding: 0;
  border: 0;
}
input {
  line-height: normal;
}
input[type="checkbox"],
input[type="radio"] {
  box-sizing: border-box;
  padding: 0;
}
input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  height: auto;
}
input[type="search"] {
  -webkit-box-sizing: content-box;
     -moz-box-sizing: content-box;
          box-sizing: content-box;
  -webkit-appearance: textfield;
}
input[type="search"]::-webkit-search-cancel-button,
input[type="search"]::-webkit-search-decoration {
  -webkit-appearance: none;
}
fieldset {
  padding: .35em .625em .75em;
  margin: 0 2px;
  border: 1px solid #c0c0c0;
}
legend {
  padding: 0;
  border: 0;
}
textarea {
  overflow: auto;
}
optgroup {
  font-weight: bold;
}
table {
  border-spacing: 0;
  border-collapse: collapse;
}
td,
th {
  padding: 0;
}
@media print {
  * {
    color: #000 !important;
    text-shadow: none !important;
    background: transparent !important;
    box-shadow: none !important;
  }
  a,
  a:visited {
    text-decoration: underline;
  }
  a[href]:after {
    content: " (" attr(href) ")";
  }
  abbr[title]:after {
    content: " (" attr(title) ")";
  }
  a[href^="javascript:"]:after,
  a[href^="#"]:after {
    content: "";
  }
  pre,
  blockquote {
    border: 1px solid #999;

    page-break-inside: avoid;
  }
  thead {
    display: table-header-group;
  }
  tr,
  img {
    page-break-inside: avoid;
  }
  img {
    max-width: 100% !important;
  }
  p,
  h2,
  h3 {
    orphans: 3;
    widows: 3;
  }
  h2,
  h3 {
    page-break-after: avoid;
  }
  select {
    background: #fff !important;
  }
  .navbar {
    display: none;
  }
  .table td,
  .table th {
    background-color: #fff !important;
  }
  .btn > .caret,
  .dropup > .btn > .caret {
    border-top-color: #000 !important;
  }
  .label {
    border: 1px solid #000;
  }
  .table {
    border-collapse: collapse !important;
  }
  .table-bordered th,
  .table-bordered td {
    border: 1px solid #ddd !important;
  }
}
```

## Bootstrap 排版

### 标题

#### 使用方法

定义标题都是使用标签`<h1>`到`<h6>`，也可以使用 `class="h1"`来让非标题元素和标题使用相同的样式。

```HTML
<h1>Bootstrap标题一</h1>
<div class="h1">Bootstrap标题一</div>
```

#### CSS分析

Bootstrap 中标题的配置统计如下表：

![](http://img.mukewang.com/53acce330001429807730337.jpg)

Bootstrap标题样式进行了以下显著的优化重置：

1. 重新设置了margin-top和margin-bottom的值，  h1~h3重置后的值都是20px；h4~h6重置后的值都是10px。
2. 所有标题的行高都是1.1（也就是font-size的1.1倍）。所有的标题文本颜色和字体都继承父元素的颜色和字体。
3. 固定不同级别标题字体大小，h1=36px，h2=30px，h3=24px，h4=18px，h5=14px和h6=12px。

**小标题**

我们在Web的制作中，常常会碰到在一个标题后面紧跟着一行小的副标题。在Bootstrap中他也考虑了这种排版效果，使用了`<small>`标签来制作副标题。其 CSS 效果是：

1. 行高都是1，而且font-weight设置了normal变成了常规效果（不加粗），同时颜色被设置为灰色（#777）。
2. 由于`<small>`内的文本字体在h1~h3内，其大小都设置为当前字号的65%；而在h4~h6内的字号都设置为当前字号的75%；

```CSS
h1 small,
h2 small,
h3 small,
h4 small,
h5 small,
h6 small,
.h1 small,
.h2 small,
.h3 small,
.h4 small,
.h5 small,
.h6 small,
h1 .small,
h2 .small,
h3 .small,
h4 .small,
h5 .small,
h6 .small,
.h1 .small,
.h2 .small,
.h3 .small,
.h4 .small,
.h5 .small,
.h6 .small {
  font-weight: normal;
  line-height: 1;
  color: #777;
}
h1 small,
.h1 small,
h2 small,
.h2 small,
h3 small,
.h3 small,
h1 .small,
.h1 .small,
h2 .small,
.h2 .small,
h3 .small,
.h3 .small {
  font-size: 65%;
}
h4 small,
.h4 small,
h5 small,
.h5 small,
h6 small,
.h6 small,
h4 .small,
.h4 .small,
h5 .small,
.h5 .small,
h6 .small,
.h6 .small {
  font-size: 75%;
}
```

### 段落

#### 使用方法

使用`<p>` 标签将段落包括起来

#### CSS 分析

Bootstrap 对正文文本设置了一个全局样式：
```CSS
body {
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  font-size: 14px;
  line-height: 1.42857143; // 20/14
  color: #333;
  background-color: #fff;
}
```

1. 全局文本字号为14px(font-size)。
2. 行高为1.42857143（line-height），大约是20px(大家看到一串的小数或许会有疑惑，其实他是通过LESS编译器计算出来的，当然Sass也有这样的功能)。
3. 颜色为深灰色（#333）；
4. 字体为"Helvetica Neue", Helvetica, Arial, sans-serif;（font-family），或许这样的字体对我们中文并不太合适，但在实际项目中，大家可以根据自己的需求进行重置，在此我们不做过多阐述，我们回到这里。该设置都定义在<body>元素上，由于这几个属性都是继承属性，所以Web页面中文本（包括段落p元素）如无重置都会具有这些样式效果。

```CSS
p {
  margin: 0 0 10px;
}
```

在Bootstrap中，为了让段落p元素之间具有一定的间距，便于用户阅读文本，特意**设置了p元素的margin值**（默认情况之下，p元素具有一个上下外边距，并且保持一个行高的高度）：

#### 段落强调

##### 使用方法

使用 `<p class="lead">` 来让一个段落突出显示。

##### CSS 分析

```CSS
.lead {
  margin-bottom: 20px;
  font-size: 16px;
  font-weight: 300;
  line-height: 1.4;
}
@media (min-width: 768px) {/*大中型浏览器字体稍大*/
  .lead {
    font-size: 21px;
  }
}
```
针对大中型浏览器，将字体的大小放大到 21px。

Bootstrap还通过元素标签:`<small>`和`<strong>`给文本做突出样式处理。

```CSS
small,
.small {
  font-size: 85%; /*标准字体的85%,也就是14px * 0.85px，差不多12px*/
}
```

其中还有 small 的 font-size 为 80% 的样式被覆盖掉了。

```CSS
b,
strong {
  font-weight: bold;/*文本加粗*/
}
```

这个样式实现的是文本**粗体**。

**粗体可以使用`<strong>`样式来实现，斜体可以使用`<em>`或者`<i>`样式来实现。不过斜体的实现使用的是浏览器自带的实现方法，Bootstrp没有进行 CSS 的修改。**

#### 通过颜色进行强调

Bootstrap还定义了一套类名，这里称其为强调类名（类似前面说的“.lead”）,这些强调类都是通过颜色来表示强调，具本说明如下：

* .text-muted：提示，使用浅灰色（#999）
* .text-primary：主要，使用蓝色（#428bca）
* .text-success：成功，使用浅绿色(#3c763d)
* .text-info：通知信息，使用浅蓝色（#31708f）
* .text-warning：警告，使用黄色（#8a6d3b）
* .text-danger：危险，使用褐色（#a94442）

显示效果如下：

![](http://ofjjubwp5.bkt.clouddn.com/image/png/img86.png)

##### 使用方法

可以对所有的标签添加对应的类实现文字颜色的改变。当对 `<a>` 标签添加该类的时候，还有自带的 :hover 颜色改变。

##### CSS 分析

CSS 代码如下：

```CSS
.text-muted {
  color: #777;
}
.text-primary {
  color: #337ab7;
}
.text-success {
  color: #3c763d;
}
.text-info {
  color: #31708f;
}
.text-warning {
  color: #8a6d3b;
}
.text-danger {
  color: #a94442;
}
```
#### 段落对齐方法

在CSS中常常使用text-align来实现文本的对齐风格的设置。其中主要有四种风格，在CSS中常常使用text-align来实现文本的对齐风格的设置。其中主要有四种风格：

* .text-left：左对齐
* .text-center：居中对齐
* .text-right：右对齐
* .text-justify：两端对齐

**目前两端对齐在各浏览器下解析各有不同，特别是应用于中文文本的时候。所以项目中慎用。**

##### 使用方法

在段落中使用相关的类即可。

##### CSS 分析

```CSS
.text-left {
  text-align: left;
}
.text-right {
  text-align: right;
}
.text-center {
  text-align: center;
}
.text-justify {
  text-align: justify;
}
```

通过 text-align 实现。

#### 其他文本样式

```CSS
.text-nowrap {
  white-space: nowrap; /*段落中的文本不想允许换行*/
}
.text-lowercase {
  text-transform: lowercase; /*段落中的文字全部小写*/
}
.text-uppercase {
  text-transform: uppercase; /*段落中的文字全部大写*/
}
.text-capitalize {
  text-transform: capitalize; /*段落中所有的单词进行首字母大写*/
}
```

### 列表

在HTML文档中，列表结构主要有三种：有序列表、无序列表和定义列表。

Bootstrap根据平时的使用情形提供了六种形式的列表：
* 普通列表
* 有序列表
* 去点列表
* 内联列表
* 描述列表
* 水平描述列表

#### 有序列表和无序列表

##### 使用方法

使用`ul`标签表示无序列表，使用`ol`标签表示有序列表，和普通表示方法一样。

##### CSS 分析

```CSS
ul,
ol {
  margin-top: 0;
  margin-bottom: 10px;
}
ul ul,
ol ul,
ul ol,
ol ol {
  margin-bottom: 0;
}
```

Bootstrap对于列表，只是在margin上做了一些调整。

#### 去点列表

##### 使用方法

通过对列表添加一个类名“.list-unstyled”,这样就可以去除默认的列表样式的风格。

##### CSS 分析

```CSS
.list-unstyled {
  padding-left: 0;
  list-style: none;
}
```

该效果除了清除项目编号之外，还将列表默认的左边内距也清０了。

**注意：**

如果是对`<ul>`标签添加该类，则`<ul>`标签下所有的`<li>`都没有点，同时所有的`<li>`显示都会提前，因为`<ul>`标签会给其子元素默认添加 padding-left:40px，如下图：

![](http://ojt6zsxg2.bkt.clouddn.com/59414748c29df3f72c47077c27cee106.png)

如果是对单个`<li>`标签使用取点，则该标签前面没有点，但是不会提前，因为此时 padding-left 本来就等于0。如下图：

![](http://ojt6zsxg2.bkt.clouddn.com/413216e4860b7455b45b9dcf529291ad.png)

**所以要分清楚是要给 `<li>` 还是给 `<ul>` 添加 .list-unstyled**

#### 内联列表

通过添加类名“.list-inline”来实现内联列表，简单点说就是把垂直列表换成水平列表，而且去掉项目符号（编号），保持水平显示。

显示效果如下：

![](http://ojt6zsxg2.bkt.clouddn.com/7231e37af375e269dd0d39f11852c1d3.png)

#### 使用方法

在`<ul>` 或 `<ol>` 标签添加类 .list-inline

#### CSS 分析

```CSS
.list-inline {
  padding-left: 0;
  margin-left: -5px;
  list-style: none;
}
.list-inline > li {
  display: inline-block;
  padding-right: 5px;
  padding-left: 5px;
}
```

#### 定义列表

##### 使用方法

定义列表 dl（声明定义列表）、dt（定义列表中的项目）、dd（描述列表中的项目） 使用方法和平常无异。

##### CSS 分析

```CSS
dl {
  margin-top: 0;
  margin-bottom: 20px;
}
dt,
dd {
  line-height: 1.42857143;
}
dt {
  font-weight: bold;
}
dd {
  margin-left: 0;
}
```
只是调整了行间距，外边距和字体加粗效果。

#### 水平定义列表

是定义列表的水平显示，显示效果如下：

![](http://ojt6zsxg2.bkt.clouddn.com/fbdf0471607acb7979a414f7267b4859.png)

##### 使用方法

水平定义列表就像内联列表一样，Bootstrap可以给<dl>添加类名“.dl-horizontal”给定义列表实现水平显示效果

##### CSS 分析

```css
@media (min-width: 768px) {
  .dl-horizontal dt {
    float: left;
    width: 160px;
    overflow: hidden;
    clear: left;
    text-align: right;
    text-overflow: ellipsis; //当发生文本溢出的时候，显示省略符号来代表被修剪的文本。
    white-space: nowrap; // 文本不会换行，文本会在在同一行上继续
  }
  .dl-horizontal dd {
    margin-left: 180px;
  }
}
```

只有屏幕大于768px的时候，添加类名“.dl-horizontal”才具有水平定义列表效果，当屏幕小于768px的时候，定义列表又变为原本的形式。水平列表的修改点有：

1. 将dt设置了一个左浮动，并且设置了一个宽度为160px
2. 将dd设置一个margin-left的值为180px，达到水平的效果
3. 当标题宽度超过160px时，将会显示三个省略号

### 代码

Bootstrap主要提供了三种代码风格：
1. 使用`<code></code>`来显示单行内联代码，一般是针对于单个单词或单个句子的代码
2. 使用`<pre></pre>`来显示多行块代码，一般是针对于多行代码（也就是成块的代码
3. 使用`<kbd></kbd>`来显示用户输入代码，一般是表示用户要通过键盘输入的内容

显示效果如下：

![](http://ojt6zsxg2.bkt.clouddn.com/f9924efb7cc82d6228ad33c43117d0ac.png)

**不管使用哪种代码风格，在代码中碰到小于号（<）要使用硬编码“`&lt;`”来替代，大于号(>)使用“`&gt;`”来替代。**

`<pre>`元素一般用于显示大块的代码，并保证原有格式不变。但有时候代码太多，而且不想让其占有太大的页面篇幅，只需要在pre标签上添加类名“.pre-scrollable”，就可以控制代码块区域最大高度为340px，一旦超出这个高度，就会在Y轴出现滚动条。

#### CSS 分析

```css
.pre-scrollable {
  max-height: 340px;
  overflow-y: scroll;
}
```

### 表格

####  表格的初始化

Boostrap 对表格进行了一些初始化，方便在通过 class 引入自定义的类有一致的显示效果：

```css
table {
  background-color: transparent;
}
table {
  border-spacing: 0; //设置相邻单元格的边框间的距离（仅用于“边框分离”模式）。
  border-collapse: collapse;  //设置表格的边框是否被合并为一个单一的边框，会忽略 border-spacing 和 empty-cells 属性。
}
td,
th {
  padding: 0;
}
```

Bootstrap为表格不同的样式风格提供了不同的类名，主要包括：
1. .table：基础表格
2. .table-striped：斑马线表格
3. .table-bordered：带边框的表格
4. .table-hover：鼠标悬停高亮的表格
5. .table-condensed：紧凑型表格
6. .table-responsive：响应式表格

使用方法是 `<table>` 标签添加上面的类来实现不同样式的标签。**也可以将多个类添加在一起组成显示效果更好的表格**

比较推荐的表格样式显示效果如下：

![](http://ojt6zsxg2.bkt.clouddn.com/626daf1428fbca5e1437b1787c2f1720.png)

![](http://ojt6zsxg2.bkt.clouddn.com/c13aba0c87d66f619a8d220183aaf045.png)

其对应的代码为：

```css
<h1>基础表格</h1>
<table class="table">
   <thead>
     <tr>
       <th>表格标题</th>
       <th>表格标题</th>
       <th>表格标题</th>
     </tr>
   </thead>
   <tbody>
     <tr>
       <td>表格单元格</td>
       <td>表格单元格</td>
       <td>表格单元格</td>
     </tr>
     <tr>
       <td>表格单元格</td>
       <td>表格单元格</td>
       <td>表格单元格</td>
     </tr>
   </tbody>
 </table>
<h1>斑马线表格</h1>
<table class="table table-striped">
   <thead>
     <tr>
       <th>表格标题</th>
       <th>表格标题</th>
       <th>表格标题</th>
     </tr>
   </thead>
   <tbody>
     <tr>
       <td>表格单元格</td>
       <td>表格单元格</td>
       <td>表格单元格</td>
     </tr>
     <tr>
       <td>表格单元格</td>
       <td>表格单元格</td>
       <td>表格单元格</td>
     </tr>
     <tr>
       <td>表格单元格</td>
       <td>表格单元格</td>
       <td>表格单元格</td>
     </tr>
     <tr>
       <td>表格单元格</td>
       <td>表格单元格</td>
       <td>表格单元格</td>
     </tr>
   </tbody>
 </table>
<h1>带边框的表格</h1>
 <table class="table table-bordered">
   <thead>
     <tr>
       <th>表格标题</th>
       <th>表格标题</th>
       <th>表格标题</th>
     </tr>
   </thead>
   <tbody>
     <tr>
       <td>表格单元格</td>
       <td>表格单元格</td>
       <td>表格单元格</td>
     </tr>
     <tr>
       <td>表格单元格</td>
       <td>表格单元格</td>
       <td>表格单元格</td>
     </tr>
     <tr>
       <td>表格单元格</td>
       <td>表格单元格</td>
       <td>表格单元格</td>
     </tr>
     <tr>
       <td>表格单元格</td>
       <td>表格单元格</td>
       <td>表格单元格</td>
     </tr>
   </tbody>
 </table>
<h1>鼠标悬浮高亮的表格</h1>
<table class="table table-striped table-bordered table-hover">
   <thead>
     <tr>
       <th>表格标题</th>
       <th>表格标题</th>
       <th>表格标题</th>
     </tr>
   </thead>
   <tbody>
     <tr>
       <td>表格单元格</td>
       <td>表格单元格</td>
       <td>表格单元格</td>
     </tr>
     <tr>
       <td>表格单元格</td>
       <td>表格单元格</td>
       <td>表格单元格</td>
     </tr>
     <tr>
       <td>表格单元格</td>
       <td>表格单元格</td>
       <td>表格单元格</td>
     </tr>
     <tr>
       <td>表格单元格</td>
       <td>表格单元格</td>
       <td>表格单元格</td>
     </tr>
   </tbody>
 </table>
 <h1>紧凑型表格</h1>
  <table class="table table-condensed">
   <thead>
     <tr>
       <th>表格标题</th>
       <th>表格标题</th>
       <th>表格标题</th>
     </tr>
   </thead>
   <tbody>
     <tr>
       <td>表格单元格</td>
       <td>表格单元格</td>
       <td>表格单元格</td>
     </tr>
     <tr>
       <td>表格单元格</td>
       <td>表格单元格</td>
       <td>表格单元格</td>
     </tr>
     <tr>
       <td>表格单元格</td>
       <td>表格单元格</td>
       <td>表格单元格</td>
     </tr>
     <tr>
       <td>表格单元格</td>
       <td>表格单元格</td>
       <td>表格单元格</td>
     </tr>
   </tbody>
 </table>
 <h1>响应式表格</h1>
 <div class="table-responsive">
   <table class="table table-bordered">
   <thead>
     <tr>
       <th>表格标题</th>
       <th>表格标题</th>
       <th>表格标题</th>
     </tr>
   </thead>
   <tbody>
     <tr>
       <td>表格单元格</td>
       <td>表格单元格</td>
       <td>表格单元格</td>
     </tr>
     <tr>
       <td>表格单元格</td>
       <td>表格单元格</td>
       <td>表格单元格</td>
     </tr>
     <tr>
       <td>表格单元格</td>
       <td>表格单元格</td>
       <td>表格单元格</td>
     </tr>
     <tr>
       <td>表格单元格</td>
       <td>表格单元格</td>
       <td>表格单元格</td>
     </tr>
   </tbody>
 </table>
```

#### 表格的类

只需要在`<tr>`元素中添加上表对应的类名，可以使用不同的颜色表示不同的意义：

![](http://ojt6zsxg2.bkt.clouddn.com/69f7b0ee848d406f6fdce773c4971673.png)

除了”.active”之外，其他四个类名和”.table-hover”配合使用时，Bootstrap针对这几种样式也做了相应的**悬浮状态的样式**设置，所以如果需要给tr元素添加其他颜色样式时，在”.table-hover”表格中也要做相应的调整。

注意要实现悬浮状态，需要在`<table>`标签上加入table-hover类。

#### 基础表格

**不管制作哪种表格都离不开类名“table”。所以大家在使用Bootstrap表格时，千万注意，你的`<table>`元素中一定不能缺少类名“table”。**

##### 使用方法

通过对`<table>`标签添加 .table 类来实现。

##### CSS 分析

“.table”主要有三个作用：
1. 给表格设置了margin-bottom:20px以及设置单元内距
2. 在thead底部设置了一个2px的浅灰实线
3. 每个单元格顶部设置了一个1px的浅灰实线

#### 斑马线表格

其效果与基础表格相比，仅是在tbody隔行有一个浅灰色的背景色。

##### 使用方法

在`<table class="table">`的基础上增加类名“.table-striped”即可：

```css
<table class="table table-striped">
…
</table>
```

##### CSS分析

```css
.table-striped > tbody > tr:nth-of-type(odd) {
  background-color: #f9f9f9;
}
```

#### 带边框的表格

##### 使用方法

在基础表格`<table class="table">`基础上添加一个“.table-bordered”类名即可：

```css
<table  class="table table-bordered">
  …
</table>
```

##### CSS分析

```css
.table-bordered {
  border: 1px solid #ddd;/*整个表格设置边框*/
}
.table-bordered > thead > tr > th,
.table-bordered > tbody > tr > th,
.table-bordered > tfoot > tr > th,
.table-bordered > thead > tr > td,
.table-bordered > tbody > tr > td,
.table-bordered > tfoot > tr > td {
  border: 1px solid #ddd;/*每个单元格设置边框*/
}
.table-bordered > thead > tr > th,
.table-bordered > thead > tr > td {
  border-bottom-width: 2px;/*表头底部边框*
}
```

#### 鼠标悬浮高亮的表格

##### 使用方法

仅需要`<table class="table">`元素上添加类名“table-hover”即可：

```css
<table class="table table-hover">
…
</table>
```

当你鼠标悬浮在某一单元格上时，单元格所在行的背景色都会变成浅灰色。

##### CSS 分析

```css
.table-hover > tbody > tr:hover {
  background-color: #f5f5f5;
}
```

同时也针对不同类型的表格（.active .success .info .warning .error）的 hover 动作设计了不同的颜色

#### 紧凑型表格

##### 使用方法

只是需要在`<table class="table">`基础上添加类名“table-condensed”：

```css
<table class="table table-condensed">
…
</table>
```

##### CSS 分析

```css
.table-condensed > thead > tr > th,
.table-condensed > tbody > tr > th,
.table-condensed > tfoot > tr > th,
.table-condensed > thead > tr > td,
.table-condensed > tbody > tr > td,
.table-condensed > tfoot > tr > td {
  padding: 5px;
}
```

Bootstrap中紧凑型的表格与基础表格差别不大，因为只是将单元格的内距由8px调至5px。

#### 应式表格

##### 使用方法

Bootstrap提供了一个容器，并且此容器设置类名“.table-responsive”,此容器就具有响应式效果，然后将`<table class="table">`置于这个容器当中，这样表格也就具有响应式效果。

````css
<div class="table-responsive">
<table class="table table-bordered">
   …
</table>
</div>
```

##### CSS分析

```css
.table-responsive {
  min-height: .01%;
  overflow-x: auto;
}
@media screen and (max-width: 767px) {
  .table-responsive {
    width: 100%;
    margin-bottom: 15px;
    overflow-y: hidden;
    -ms-overflow-style: -ms-autohiding-scrollbar;
    border: 1px solid #ddd;
  }
  ...
}
```
当你的浏览器可视区域小于768px时，表格底部会出现水平滚动条。当你的浏览器可视区域大于768px时，表格底部水平滚动条就会消失。

## 表单

表单中常见的元素主要包括：**文本输入框、下拉选择框、单选按钮、复选按钮、文本域和按钮**等

Bootstrap并未对其做太多的定制性效果设计，仅仅对表单内的fieldset、legend、label标签进行了定制。如：

```css
fieldset {
  min-width: 0;
  padding: 0;
  margin: 0;
  border: 0;
}
legend {
  display: block;
  width: 100%;
  padding: 0;
  margin-bottom: 20px;
  font-size: 21px;
  line-height: inherit;
  color: #333;
  border: 0;
  border-bottom: 1px solid #e5e5e5;
}
label {
  display: inline-block;
  max-width: 100%;
  margin-bottom: 5px;
  font-weight: bold;
}
```
当然表单除了这几个元素之外，还有input、select、textarea等元素。在Bootstrap框架中，通过定制了一个类名`form-control`，如果这几个元素使用了类名“form-control”，将会实现一些设计上的定制效果：

1. 宽度变成了100%
2. 设置了一个浅灰色（#ccc）的边框
3. 具有4px的圆角
4. 设置阴影效果，并且元素得到焦点之时，阴影和边框效果会有所变化
5. 设置了placeholder的颜色为#999

代码如下：

```css
.form-control {
  display: block;
  width: 100%;
  height: 34px;
  padding: 6px 12px;
  font-size: 14px;
  line-height: 1.42857143;
  color: #555;
  background-color: #fff;
  background-image: none;
  border: 1px solid #ccc;
  border-radius: 4px;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, .075);
          box-shadow: inset 0 1px 1px rgba(0, 0, 0, .075);
  -webkit-transition: border-color ease-in-out .15s, -webkit-box-shadow ease-in-out .15s;
       -o-transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
          transition: border-color ease-in-out .15s, box-shadow ease-in-out .15s;
}
.form-control:focus {
  border-color: #66afe9;
  outline: 0;
  -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, .6);
          box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, .6);
}
.form-control::-moz-placeholder {
  color: #999;
  opacity: 1;
}
.form-control:-ms-input-placeholder {
  color: #999;
}
.form-control::-webkit-input-placeholder {
  color: #999;
}
```

### 基础表单

下面给的是基础表单的样式与代码：

```css
<form role="form">
  <div class="form-group">
    <label for="exampleInputEmail1">邮箱：</label>
    <input type="email" class="form-control" id="exampleInputEmail1" placeholder="请输入您的邮箱地址">
  </div>
  <div class="form-group">
    <label for="exampleInputPassword1">密码</label>
    <input type="password" class="form-control" id="exampleInputPassword1" placeholder="请输入您的邮箱密码">
  </div>
  <div class="checkbox">
    <label>
      <input type="checkbox"> 记住密码
    </label>
  </div>
  <button type="submit" class="btn btn-default">进入邮箱</button>
</form>
```

![](http://ojt6zsxg2.bkt.clouddn.com/47472e45e9aef5bfd8b0cd933ce40f25.png)

### 水平表单

#### 使用方法

在Bootstrap框架中要实现水平表单效果，必须满足以下两个条件：
1. 在`<form>`元素是使用类名“form-horizontal”。
2. 配合Bootstrap框架的网格系统。因为网格系统带有 float:left 属性，可以自动浮动

下面是一个水平表单的显示示例：

```css
<form class="form-horizontal" role="form">
  <div class="form-group">
    <label for="inputEmail3" class="col-sm-2 control-label">邮箱</label> //添加 col-sm-x 类的对象都是默认 float:left;
    <div class="col-sm-10">
      <input type="email" class="form-control" id="inputEmail3" placeholder="请输入您的邮箱地址">
    </div>
  </div>
  <div class="form-group">
    <label for="inputPassword3" class="col-sm-2 control-label">密码</label>
    <div class="col-sm-10">
      <input type="password" class="form-control" id="inputPassword3" placeholder="请输入您的邮箱密码">
    </div>
  </div>
  <div class="form-group">
    <div class="col-sm-offset-2 col-sm-10">
      <div class="checkbox">
        <label>
          <input type="checkbox"> 记住密码
        </label>
      </div>
    </div>
  </div>
  <div class="form-group">
    <div class="col-sm-offset-2 col-sm-10">
      <button type="submit" class="btn btn-default">进入邮箱</button>
    </div>
  </div>
</form>
```
![](http://ojt6zsxg2.bkt.clouddn.com/a8271bf5e0859bfa7aea5f9d2fc365dd.png)

#### CSS 分析

在`<form>`元素上使用类名“form-horizontal”主要有以下几个作用：

1. 设置表单控件padding和margin值。
2. 改变“form-group”的表现形式，类似于网格系统的“row”。


```css
.form-horizontal .radio,
.form-horizontal .checkbox,
.form-horizontal .radio-inline,
.form-horizontal .checkbox-inline {
  padding-top: 7px;
  margin-top: 0;
  margin-bottom: 0;
}
.form-horizontal .radio,
.form-horizontal .checkbox {
  min-height: 27px;
}
.form-horizontal .form-group {
  margin-right: -15px;
  margin-left: -15px;
}
@media (min-width: 768px) {
  .form-horizontal .control-label {
    padding-top: 7px;
    margin-bottom: 0;
    text-align: right; /*水平的表单，文字右对齐*/
  }
}
.form-horizontal .has-feedback .form-control-feedback {
  right: 15px;
}
@media (min-width: 768px) {
  .form-horizontal .form-group-lg .control-label {
    padding-top: 11px;
    font-size: 18px;
  }
}
@media (min-width: 768px) {
  .form-horizontal .form-group-sm .control-label {
    padding-top: 6px;
    font-size: 12px;
  }
}
```

### 内联表单

#### 使用方法

如果你要在input前面添加一个label标签时，会导致input换行显示。如果你必须添加这样的一个label标签，并且不想让input换行，你需要将label标签也放在容器“form-group”中

只需要在`<form>`元素中添加类名“form-inline”即可。

下面是一个内联表单的示例：

```css
<form class="form-inline" role="form">
  <div class="form-group">
    <label class="sr-only" for="exampleInputEmail2">邮箱</label>
    <input type="email" class="form-control" id="exampleInputEmail2" placeholder="请输入你的邮箱地址">
  </div>
  <div class="form-group">
    <label class="sr-only" for="exampleInputPassword2">密码</label> // 使用 sr-only 将 label 隐藏。
    <input type="password" class="form-control" id="exampleInputPassword2" placeholder="请输入你的邮箱密码">
  </div>
  <div class="checkbox">
    <label>
      <input type="checkbox"> 记住密码
    </label>
  </div>
  <button type="submit" class="btn btn-default">进入邮箱</button>
</form>
```

![](http://ojt6zsxg2.bkt.clouddn.com/44cbe75503c5284b5662b111293cbb3f.png)


#### CSS 分析

```css
@media (min-width: 768px) {
  .form-inline .form-group {
    display: inline-block;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .form-control {
    display: inline-block;
    width: auto;
    vertical-align: middle;
  }
  .form-inline .form-control-static {
    display: inline-block;
  }
  .form-inline .input-group {
    display: inline-table;
    vertical-align: middle;
  }
  .form-inline .input-group .input-group-addon,
  .form-inline .input-group .input-group-btn,
  .form-inline .input-group .form-control {
    width: auto;
  }
  .form-inline .input-group > .form-control {
    width: 100%;
  }
  .form-inline .control-label {
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .radio,
  .form-inline .checkbox {
    display: inline-block;
    margin-top: 0;
    margin-bottom: 0;
    vertical-align: middle;
  }
  .form-inline .radio label,
  .form-inline .checkbox label {
    padding-left: 0;
  }
  .form-inline .radio input[type="radio"],
  .form-inline .checkbox input[type="checkbox"] {
    position: relative;
    margin-left: 0;
  }
  .form-inline .has-feedback .form-control-feedback {
    top: 0;
  }
}
```

内联表单实现原理非常简单，欲将表单控件在一行显示，就需要将表单控件设置成内联块元素（display:inline-block）。

### 输入框 input

#### 使用方法

单行输入框，常见的文本输入框，也就是input的type属性值为text。在Bootstrap中使用input时也必须添加type类型，如果没有指定type类型，将无法得到正确的样式。

为了让控件在各种表单风格中样式不出错，需要添加类名“form-control”

```css
<form role="form">
<div class="form-group">
<input type="email" class="form-control" placeholder="Enter email">
</div>
</form>
```

#### CSS 分析

对 form-control 的分析可以参考表单开始部分

有input、select、textarea等元素。在Bootstrap框架中，通过定制了一个类名`form-control`，如果这几个元素使用了类名“form-control”，将会实现一些设计上的定制效果：

1. 宽度变成了100%
2. 设置了一个浅灰色（#ccc）的边框
3. 具有4px的圆角
4. 设置阴影效果，并且元素得到焦点之时，阴影和边框效果会有所变化
5. 设置了placeholder的颜色为#999

### 下拉选择列表 select

#### 使用方法

Bootstrap框架中的下拉选择框使用和原始的一致，多行选择设置multiple属性的值为multiple。

```css
<form role="form">
<div class="form-group">
  <select class="form-control">
    <option>1</option>
    <option>2</option>
    <option>3</option>
    <option>4</option>
    <option>5</option>
  </select>
  </div>
  <div class="form-group">
  <select multiple class="form-control">
    <option>1</option>
    <option>2</option>
    <option>3</option>
    <option>4</option>
    <option>5</option>
  </select>
</div>
</form>
```

#### CSS 分析

```css
select[multiple],
select[size] {
  height: auto;
}
```

对 select 有一些自定义的初始化设置，如果是 multiple，则height:auto。

### 文本域 textarea

#### 使用方法

文本域和原始使用方法一样，设置rows可定义其高度，设置cols可以设置其宽度。但如果textarea元素中添加了类名“form-control”类名，则无需设置cols属性。因为Bootstrap框架中的“form-control”样式的表单控件宽度为100%或auto。

```css
<form role="form">
  <div class="form-group">
    <textarea class="form-control" rows="3"></textarea>
  </div>
</form>
```

### 单选按钮和复选按钮(checkbox、radio)

#### 使用方法

![](http://ojt6zsxg2.bkt.clouddn.com/8482332185719b98381b2eee952c97e5.png)

显示效果是 checkbox 和 radio 都是竖直排列。

Bootstrap框架中checkbox和radio有点特殊，Bootstrap针对他们做了一些特殊化处理，主要是checkbox和radio与label标签配合使用会出现一些小问题（最头痛的是对齐问题）。使用Bootstrap框架，开发人员无需考虑太多，只需要按照下面的方法使用即可。

1. 不管是checkbox还是radio都使用label包起来了
2. checkbox连同label标签放置在一个名为“.checkbox”的容器内
3. radio连同label标签放置在一个名为“.radio”的容器内
在Bootstrap框架中，主要借助“.checkbox”和“.radio”样式，来处理复选框、单选按钮与标签的对齐方式。

```css
<form role="form">
  <h3>案例1</h3>
  <div class="checkbox">
    <label>
      <input type="checkbox" value="">
      记住密码
    </label>
  </div>
  <div class="radio">
    <label>
      <input type="radio" name="optionsRadios" id="optionsRadios1" value="love" checked>
      喜欢
    </label>
  </div>
    <div class="radio">
    <label>
      <input type="radio" name="optionsRadios" id="optionsRadios2" value="hate">
      不喜欢
    </label>
  </div>
</form>
```

#### CSS 分析

```css
.radio,
.checkbox {
  position: relative;
  display: block;
  margin-top: 10px;
  margin-bottom: 10px;
}
.radio label,
.checkbox label {
  min-height: 20px;
  padding-left: 20px;
  margin-bottom: 0;
  font-weight: normal;
  cursor: pointer;
}
.radio input[type="radio"],
.radio-inline input[type="radio"],
.checkbox input[type="checkbox"],
.checkbox-inline input[type="checkbox"] {
  position: absolute;
  margin-top: 4px \9;
  margin-left: -20px;
}
.radio + .radio,
.checkbox + .checkbox {
  margin-top: -5px;
}
```

#### checkbox 和 radio 水平排列

##### 使用方法

![](http://ojt6zsxg2.bkt.clouddn.com/059be45d1dc0a08186bccefc74d470e4.png)

将复选框和单选按钮需要水平排列。Bootstrap框架也做了这方面的考虑：
1. 如果checkbox需要水平排列，只需要在label标签上添加类名“checkbox-inline”
2. 如果radio需要水平排列，只需要在label标签上添加类名“radio-inline”

**注意，如果是水平排列 checkbox 和 radio，则外层不用嵌套 div.checkbox 或 div.radio，而是使用 div.form-group**

```css
<form role="form">
  <div class="form-group">
    <label class="checkbox-inline">
      <input type="checkbox"  value="option1">游戏
    </label>
    <label class="checkbox-inline">
      <input type="checkbox"  value="option2">摄影
    </label>
    <label class="checkbox-inline">
    <input type="checkbox"  value="option3">旅游
    </label>
  </div>
  <div class="form-group">
    <label class="radio-inline">
      <input type="radio"  value="option1" name="sex">男性
    </label>
    <label class="radio-inline">
      <input type="radio"  value="option2" name="sex">女性
    </label>
    <label class="radio-inline">
      <input type="radio"  value="option3" name="sex">中性
    </label>
  </div>
</form>
```

##### CSS 分析

```css
.radio-inline,
.checkbox-inline {
  position: relative;
  display: inline-block;
  padding-left: 20px;
  margin-bottom: 0;
  font-weight: normal;
  vertical-align: middle;
  cursor: pointer;
}
.radio-inline + .radio-inline,
.checkbox-inline + .checkbox-inline {
  margin-top: 0;
  margin-left: 10px;
}
```

### 表单控件（按钮）

按钮也是表单重要控件之一,制作按钮通常使用下面代码来实现：
1. `input[type=“submit”]`
2. `input[type=“button”]`
3. `input[type=“reset”]`
4. `<button>`

**在Bootstrap框架中的按钮都是采用`<button>`来实现。**

所有的按钮显示效果如下：

![](http://ojt6zsxg2.bkt.clouddn.com/3468353145788a309a05c857a49d4940.png)

#### 使用方法
可以使用 `<button>`标签或者 `<a>` 标签作为按钮，其他的方法，比如 input.btn、div.btn、span.btn 不推荐。

```css
<button class="btn btn-default" href="#">Default</button>
a href="##" class="btn btn-default">a标签按钮</a>
```

#### CSS 分析

```
.btn {
  display: inline-block;
  padding: 6px 12px;
  margin-bottom: 0;
  font-size: 14px;
  font-weight: normal;
  line-height: 1.42857143;
  text-align: center;
  white-space: nowrap;
  vertical-align: middle;
  -ms-touch-action: manipulation;
      touch-action: manipulation;
  cursor: pointer;
  -webkit-user-select: none;
     -moz-user-select: none;
      -ms-user-select: none;
          user-select: none;
  background-image: none;
  border: 1px solid transparent;
  border-radius: 4px;
}
.btn:focus,
.btn:active:focus,
.btn.active:focus,
.btn.focus,
.btn:active.focus,
.btn.active.focus {
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
.btn:hover,
.btn:focus,
.btn.focus {
  color: #333;
  text-decoration: none;
}
.btn:active,
.btn.active {
  background-image: none;
  outline: 0;
  -webkit-box-shadow: inset 0 3px 5px rgba(0, 0, 0, .125);
          box-shadow: inset 0 3px 5px rgba(0, 0, 0, .125);
}
.btn.disabled,
.btn[disabled],
fieldset[disabled] .btn {
  cursor: not-allowed;
  filter: alpha(opacity=65);
  -webkit-box-shadow: none;
          box-shadow: none;
  opacity: .65;
}

```

```css
.btn-default {
  color: #333;
  background-color: #fff;
  border-color: #ccc;
}
```

显示效果都是通过设置字体颜色，背景及边框颜色来实现的。

#### 按钮大小

##### 使用方法

使用 .btn-lg、btn-sm、btn-xs来控制按键的大小

```
<button class="btn btn-primary btn-lg" type="button">大型按钮.btn-lg</button>
    <button class="btn btn-primary" type="button">正常按钮</button>
    <button class="btn btn-primary btn-sm" type="button">小型按钮.btn-sm</button>
    <button class="btn btn-primary btn-xs" type="button">超小型按钮.btn-xs</button>
```

![](http://ojt6zsxg2.bkt.clouddn.com/67aac03db1ed3c15b03d43941d28a8c9.png)

##### CSS 分析

```
.btn-lg,
.btn-group-lg > .btn {
  padding: 10px 16px;
  font-size: 18px;
  line-height: 1.3333333;
  border-radius: 6px;
}
.btn-sm,
.btn-group-sm > .btn {
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 3px;
}
.btn-xs,
.btn-group-xs > .btn {
  padding: 1px 5px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 3px;
}
```
在Bootstrap框架中控制按钮的大小都是通过修改按钮的padding、line-height、font-size和border-radius几个属性

#### 块状按钮

每个示例中的按钮宽度都是依靠按钮文本和padding的值来决定。但有时候在制作按钮的时候需要按钮宽度充满整个父容器（width:100%），特别是在移动端的制作中。

##### 使用方法

添加 .btn-block

```
<button class="btn btn-primary btn-lg btn-block" type="button">大型按钮.btn-lg</button>
<button class="btn btn-primary btn-block" type="button">正常按钮</button>
<button class="btn btn-primary btn-sm btn-block" type="button">小型按钮.btn-sm</button>
<button class="btn btn-primary btn-xs btn-block" type="button">超小型按钮.btn-xs</button>
```
![](http://ojt6zsxg2.bkt.clouddn.com/0d46e8f4bd4669155c6d957817c111a2.png)

##### CSS 分析

```
.btn-block {
  display: block;
  width: 100%;
}
.btn-block + .btn-block {
  margin-top: 5px;
}
input[type="submit"].btn-block,
input[type="reset"].btn-block,
input[type="button"].btn-block {
  width: 100%;
}
```

#### 按钮状态

Bootstrap按钮的活动状态主要包括按钮的悬浮状态(:hover)，点击状态(:active)、焦点状态（:focus）和 disabled

##### disabled 使用方法

在Bootstrap框架中，要禁用按钮有两种实现方式：
1. 在标签中添加disabled属性
2. 在元素标签中添加类名“disabled”

```
<button class="btn btn-primary btn-lg btn-block" type="button" disabled="disabled">通过disabled属性禁用按钮</button> 
	<button class="btn btn-primary btn-block disabled" type="button">通过添加类名disabled禁用按钮</button>
	<button class="btn btn-primary btn-sm btn-block" type="button">未禁用的按钮</button>
```

同样的，其他风格按钮也具有这样的效果，只是颜色做了一定的调整

##### CSS 分析

```
.btn:focus,
.btn:active:focus,
.btn.active:focus,
.btn.focus,
.btn:active.focus,
.btn.active.focus {
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
.btn:hover,
.btn:focus,
.btn.focus {
  color: #333;
  text-decoration: none;
}
.btn:active,
.btn.active {
  background-image: none;
  outline: 0;
  -webkit-box-shadow: inset 0 3px 5px rgba(0, 0, 0, .125);
          box-shadow: inset 0 3px 5px rgba(0, 0, 0, .125);
}
```

```
.btn.disabled,
.btn[disabled],
fieldset[disabled] .btn {
  cursor: not-allowed;
  filter: alpha(opacity=65);
  -webkit-box-shadow: none;
          box-shadow: none;
  opacity: .65;
}
```

#### 按钮（按钮组）

##### 使用方法

按钮组和下拉菜单组件一样，需要依赖于button.js插件才能正常运行。不过我们同样可以直接只调用bootstrap.js文件。因为这个文件已集成了button.js插件功能。

使用一个名为“btn-group”的容器，把多个按钮放到这个容器中。

```
<div class="btn-group">
    <button type="button" class="btn btn-default"><span class="glyphicon glyphicon-step-backward"></span></button>
    <button type="button" class="btn btn-default"><span class="glyphicon glyphicon-fast-backward"></span></button>
    <button type="button" class="btn btn-default"><span class="glyphicon glyphicon-backward"></span></button>
    <button type="button" class="btn btn-default"><span class="glyphicon glyphicon-play"></span></button>
    <button type="button" class="btn btn-default"><span class="glyphicon glyphicon-pause"></span></button>
    <button type="button" class="btn btn-default"><span class="glyphicon glyphicon-stop"></span></button>
    <button type="button" class="btn btn-default"><span class="glyphicon glyphicon-forward "></span></button>
    <button type="button" class="btn btn-default"><span class="glyphicon glyphicon-fast-forward"></span></button>
    <button type="button" class="btn btn-default"><span class="glyphicon glyphicon-step-forward"></span></button>
</div>
```

![](http://ojt6zsxg2.bkt.clouddn.com/c540c9146a1b2ff1d8d9f059b8fcb891.png)

除了可以使用`<button>`元素之外，还可以使用其他标签元素，比如`<a>`标签。唯一要保证的是：不管使用什么标签，“.btn-group”容器里的标签元素需要带有类名“.btn”。

##### css 分析

```
.btn-group,
.btn-group-vertical {
  position: relative;
  display: inline-block;
  vertical-align: middle;
}
.btn-group > .btn,
.btn-group-vertical > .btn {
  position: relative;
  float: left;
}
.btn-group > .btn:hover,
.btn-group-vertical > .btn:hover,
.btn-group > .btn:focus,
.btn-group-vertical > .btn:focus,
.btn-group > .btn:active,
.btn-group-vertical > .btn:active,
.btn-group > .btn.active,
.btn-group-vertical > .btn.active {
  z-index: 2;
}
.btn-group .btn + .btn,
.btn-group .btn + .btn-group,
.btn-group .btn-group + .btn,
.btn-group .btn-group + .btn-group {
  margin-left: -1px;
}
```

从效果图上我们可以看出，按钮组四个角都是圆角，实现方法如下：
1. 默认所有按钮都有圆角
2. 除第一个按钮和最后一个按钮（下拉按钮除外），其他的按钮都取消圆角效果
3. 第一个按钮只留左上角和左下角是圆角
4. 最后一个按钮只留右上角和右下角是圆角


```
.btn-group > .btn:not(:first-child):not(:last-child):not(.dropdown-toggle) {
  border-radius: 0;
}
.btn-group > .btn:first-child {
  margin-left: 0;
}
.btn-group > .btn:first-child:not(:last-child):not(.dropdown-toggle) {
  border-top-right-radius: 0;
  border-bottom-right-radius: 0;
}
.btn-group > .btn:last-child:not(:first-child),
.btn-group > .dropdown-toggle:not(:first-child) {
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
}
.btn-group > .btn-group {
  float: left;
}
.btn-group > .btn-group:not(:first-child):not(:last-child) > .btn {
  border-radius: 0;
}
.btn-group > .btn-group:first-child:not(:last-child) > .btn:last-child,
.btn-group > .btn-group:first-child:not(:last-child) > .dropdown-toggle {
  border-top-right-radius: 0;
  border-bottom-right-radius: 0;
}
.btn-group > .btn-group:last-child:not(:first-child) > .btn:first-child {
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
}
```

#### 按钮（按钮工具栏）

在富文本编辑器中，将按钮组分组排列在一起，比如说复制、剪切和粘贴一组；左对齐、中间对齐、右对齐和两端对齐一组，如下图所示：

![](http://img.mukewang.com/53e45edc00019ad308600101.jpg)

那么Bootstrap框架按钮工具栏也提供了这样的制作方法，你只需要将按钮组“btn-group”按组放在一个大的容器“btn-toolbar”中。

##### 使用方法

```
<div class="btn-toolbar">
  <div class="btn-group btn-group-lg">
    <button type="button" class="btn btn-default"><span class="glyphicon glyphicon-align-left"></span></button>
    <button type="button" class="btn btn-default"><span class="glyphicon glyphicon-align-center"></span></button>
    <button type="button" class="btn btn-default"><span class="glyphicon glyphicon-align-right"></span></button>
    <button type="button" class="btn btn-default"><span class="glyphicon glyphicon-align-justify"></span></button>
  </div>
  <div class="btn-group">
    <button type="button" class="btn btn-default"><span class="glyphicon glyphicon-indent-left"></span></button>
    <button type="button" class="btn btn-default"><span class="glyphicon glyphicon-indent-right"></span></button>
  </div>
  <div class="btn-group btn-group-sm">
    <button type="button" class="btn btn-default"><span class="glyphicon glyphicon-font"></span></button>
    <button type="button" class="btn btn-default"><span class="glyphicon glyphicon-bold"></span></button>
    <button type="button" class="btn btn-default"><span class="glyphicon glyphicon-italic"></span></button>
  </div>
  <div class="btn-group btn-group-xs">
    <button type="button" class="btn btn-default"><span class="glyphicon glyphicon-text-height"></span></button>
    <button type="button" class="btn btn-default"><span class="glyphicon glyphicon-text-width"></span></button>
  </div>
</div>
```

![](http://ojt6zsxg2.bkt.clouddn.com/2555c89d65c66e8a40a4c2df5c088ef9.png)

按钮组的大小也可以进行修改：

1. .btn-group-lg:大按钮组
2. .btn-group-sm:小按钮组
3. .btn-group-xs:超小按钮组

##### css 分析

```
.btn-toolbar {
  margin-left: -5px;
}
.btn-toolbar .btn,
.btn-toolbar .btn-group,
.btn-toolbar .input-group {
  float: left;
}
.btn-toolbar > .btn,
.btn-toolbar > .btn-group,
.btn-toolbar > .input-group {
  margin-left: 5px;
}
```
实现原理主要是让容器的多个分组“btn-group”元素进行浮动，并且组与组之前保持5px的左外距。

```
.btn-toolbar:before,
.btn-toolbar:after｛
　display: table;
content: " ";
｝
.btn-toolbar:after{
  clear: both;
}
```

注意在”btn-toolbar”上清除浮动。

```
.btn-lg,
.btn-group-lg > .btn {
  padding: 10px 16px;
  font-size: 18px;
  line-height: 1.3333333;
  border-radius: 6px;
}
.btn-sm,
.btn-group-sm > .btn {
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 3px;
}
.btn-xs,
.btn-group-xs > .btn {
  padding: 1px 5px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 3px;
}
```

#### 按钮（嵌套分组）

##### 使用方法

使用的时候，只需要把制作下拉菜单的“dropdown”的容器换成“btn-group”，并且和普通的按钮放在同一级。

```
<div class="btn-group">
  <button class="btn btn-default" type="button">首页</button>
  <button class="btn btn-default" type="button">产品展示</button>
  <button class="btn btn-default" type="button">案例分析</button>
  <button class="btn btn-default" type="button">联系我们</button>
  <div class="btn-group">
      <button class="btn btn-default dropdown-toggle" data-toggle="dropdown" type="button">关于我们<span class="caret"></span></button>
    <ul class="dropdown-menu">
    	<li><a href="##">公司简介</a></li>
    	<li><a href="##">企业文化</a></li>
    	<li><a href="##">组织结构</a></li>
    	<li><a href="##">客服服务</a></li>
    </ul>
  </div>
```

![](http://ojt6zsxg2.bkt.clouddn.com/919f580009ab56b9af43d26669ff3d2b.png)

##### css 分析

```
.btn-group > .btn-group {
  float: left;
}
.btn-group > .btn-group:not(:first-child):not(:last-child) > .btn {
  border-radius: 0;
}
.btn-group > .btn-group:first-child:not(:last-child) > .btn:last-child,
.btn-group > .btn-group:first-child:not(:last-child) > .dropdown-toggle {
  border-top-right-radius: 0;
  border-bottom-right-radius: 0;
}
.btn-group > .btn-group:last-child:not(:first-child) > .btn:first-child {
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
}
.btn-group .dropdown-toggle:active,
.btn-group.open .dropdown-toggle {
  outline: 0;
}
.btn-group > .btn + .dropdown-toggle {
  padding-right: 8px;
  padding-left: 8px;
}
.btn-group > .btn-lg + .dropdown-toggle {
  padding-right: 12px;
  padding-left: 12px;
}
.btn-group.open .dropdown-toggle {
  -webkit-box-shadow: inset 0 3px 5px rgba(0, 0, 0, .125);
          box-shadow: inset 0 3px 5px rgba(0, 0, 0, .125);
}
.btn-group.open .dropdown-toggle.btn-link {
  -webkit-box-shadow: none;
          box-shadow: none;
}
```

#### 按钮（垂直分组）

我们只需要把水平分组的“btn-group”类名换成“btn-group-vertical”即可。

#### 按钮（等分按钮）

等分按钮的效果在移动端上特别的实用。整个按钮组宽度是容器的100%，而按钮组里面的每个按钮平分整个容器宽度。

##### 使用方法

需要在按钮组“btn-group”上追加一个“btn-group-justified”类名

```
<div class="btn-wrap">
<div class="btn-group btn-group-justified">
  <a class="btn btn-default" href="#">首页</a>
  <a class="btn btn-default" href="#">产品展示</a>
  <a class="btn btn-default" href="#">案例分析</a>
  <a class="btn btn-default" href="#">联系我们</a>
</div>
</div>
```
![](http://ojt6zsxg2.bkt.clouddn.com/9c8db632e8b3303c1b5fde76237a83f7.png)

##### css 分析

```
.btn-group-justified {
  display: table;
  width: 100%;
  table-layout: fixed;
  border-collapse: separate;
}
.btn-group-justified > .btn,
.btn-group-justified > .btn-group {
  display: table-cell;
  float: none;
  width: 1%;
}
.btn-group-justified > .btn-group .btn {
  width: 100%;
}
.btn-group-justified > .btn-group .dropdown-menu {
  left: auto;
}
```

实现原理非常简单，把“btn-group-justified”模拟成表格（display:table），而且把里面的按钮模拟成表格单元格（display:table-cell）。

**特别声明**：在制作等分按钮组时，请尽量使用`<a>`标签元素来制作按钮，因为使用`<button>`标签元素时，使用display:table在部分浏览器下支持并不友好。

#### 钮的向下向上三角形

##### 使用方法

按钮的向下三角形，我们是通过在`<button>`标签中添加一个“`<span>`”标签元素，并且命名为“caret”

```
<button class="btn btn-default dropdown-toggle" data-toggle="dropdown" type="button">按钮下拉菜单<span class="caret"></span></button>
```

##### css 分析

```
.caret {
  display: inline-block;
  width: 0;
  height: 0;
  margin-left: 2px;
  vertical-align: middle;
  border-top: 4px dashed;
  border-top: 4px solid \9;
  border-right: 4px solid transparent;
  border-left: 4px solid transparent;
}
```
这个三角形完全是通过CSS代码来实现的

如果要三角方向需要朝上显示，使用 .dropup 类（下一节会讲）

```
.dropup .caret,
.navbar-fixed-bottom .dropdown .caret {
  content: "";
  border-top: 0;
  border-bottom: 4px solid;
}
```
向上三角与向下三角的区别：其实就是改变了一个border-bottom的值。

#### 向上弹起的下拉菜单

在Bootstrap框架中专门为这种效果提代了一个类名“dropup”。使用方法正如前面所示，只需要在“btn-group”上添加这个类名（当然，如果是普通向上弹出下拉菜单，你只需要在“dropdown”类名基础上追加“dropup”类名即可）

##### 使用方法

```
<div class="btn-group dropup">
    <button class="btn btn-default dropdown-toggle" data-toggle="dropdown" type="button">按钮下拉菜单<span class="caret"></span></button>
    <ul class="dropdown-menu">
         <li><a href="##">按钮下拉菜单项</a></li>
         <li><a href="##">按钮下拉菜单项</a></li>
         <li><a href="##">按钮下拉菜单项</a></li>
         <li><a href="##">按钮下拉菜单项</a></li>
    </ul>
</div>
```

##### css 分析

```
.dropup .dropdown-menu,
.navbar-fixed-bottom .dropdown .dropdown-menu {
  top: auto;
  bottom: 100%;
  margin-bottom: 2px;
}
```
实现方法为：主要将“dropdown-menu”的top值变成了auto，而把bottom值换成了100%


### 表单控件大小

#### 控制表单控件的高度

Bootstrap框架还提供了两个不同的类名，用来控制表单控件的高度。这两个类名是：
1. input-sm:让控件比正常大小更小
2. input-lg:让控件比正常大小更大

两个类适用于表单中的**input，textarea和select**控件

##### 使用方法

```css
<input class="form-control input-lg" type="text" placeholder="添加.input-lg，控件变大">
<input class="form-control" type="text" placeholder="正常大小">
<input class="form-control input-sm" type="text" placeholder="添加.input-sm，控件变小">
```
![](http://ojt6zsxg2.bkt.clouddn.com/9acbe051a7628e9b59a13d9e1fa74b4c.png)

##### css 分析

```css
.input-sm {
  height: 30px;
  padding: 5px 10px;
  font-size: 12px;
  line-height: 1.5;
  border-radius: 3px;
}
select.input-sm {
  height: 30px;
  line-height: 30px;
}
textarea.input-sm,
select[multiple].input-sm {
  height: auto;
}
.input-lg {
  height: 46px;
  padding: 10px 16px;
  font-size: 18px;
  line-height: 1.3333333;
  border-radius: 6px;
}
select.input-lg {
  height: 46px;
  line-height: 46px;
}
textarea.input-lg,
select[multiple].input-lg {
  height: auto;
}
```
修改了 height、line-height、padding、font-size。
不管是“input-sm”还是“input-lg”仅对控件高度做了处理。

#### 控制表单空间的高度

需要控件宽度也要做一定的变化处理。这个时候就要借住Bootstrap框架的网格系统

##### 使用方法

```css
<form role="form" class="form-horizontal">
  <div class="form-group">
  <div class="col-xs-4">
    <input class="form-control input-lg" type="text" placeholder=".col-xs-4">
  </div>
  <div class="col-xs-4">
    <input class="form-control input-lg" type="text" placeholder=".col-xs-4">
  </div>
  <div class="col-xs-4">
    <input class="form-control input-lg" type="text" placeholder=".col-xs-4">
  </div>
  </div>
    …
</form>
```

### 表单控件状态

**表单有焦点的状态可以告诉用户可以输入或选择东西，禁用状态可以告诉用户不可以输入或选择东西，还有就是表单控件验证状态，可以告诉用户的操作是否正确等。**

#### 焦点状态

焦点状态是通过伪类“:focus”来实现。Bootstrap框架中表单控件的焦点状态删除了outline的默认样式，重新添加阴影效果。

#### 使用方法

要让控件在焦点状态下有上面样式效果，需要给控件添加类名“form-control”，这种方法适合 input、select、textarea 使用：

```css
<form role="form" class="form-horizontal">
  <div class="form-group">
    <div class="col-xs-6">
      <input class="form-control input-lg" type="text" placeholder="不是焦点状态下效果">
    </div>
    <div class="col-xs-6">
      <input class="form-control input-lg" type="text" placeholder="焦点点状态下效果">
    </div>
  </div>
</form>
```

![](http://ojt6zsxg2.bkt.clouddn.com/2124de1bab751578cff1fd353867aaf5.png)

file、radio和checkbox控件在焦点状态下的效果也与普通的input控件不太一样，不过不用添加类来添加 focus 效果。



##### css 分析

```css
.form-control:focus {
  border-color: #66afe9;
  outline: 0;
  -webkit-box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, .6);
          box-shadow: inset 0 1px 1px rgba(0,0,0,.075), 0 0 8px rgba(102, 175, 233, .6);
}
```
file、radio、checkbox 的 focus 效果：
```css
input[type="file"]:focus,
input[type="radio"]:focus,
input[type="checkbox"]:focus {
  outline: 5px auto -webkit-focus-ring-color;
  outline-offset: -2px;
}
```
#### 禁用状态

Bootstrap框架的表单控件的禁用状态和普通的表单禁用状态实现方法是一样的，在相应的表单控件上添加属性“disabled”。

##### 使用方法

需要在需要禁用的表单控件上加上“disabled”即可：

```css
<input class="form-control" type="text" placeholder="表单已禁用，不能输入" disabled>
```

##### css 分析

```css
.form-control[disabled],
.form-control[readonly],
fieldset[disabled] .form-control {
  background-color: #eee;
  opacity: 1;
}
.form-control[disabled],
fieldset[disabled] .form-control {
  cursor: not-allowed;
}
```

```css
input[type="radio"][disabled],
input[type="checkbox"][disabled],
input[type="radio"].disabled,
input[type="checkbox"].disabled,
fieldset[disabled] input[type="radio"],
fieldset[disabled] input[type="checkbox"] {
  cursor: not-allowed;
}
```

#### 验证状态

在Bootstrap框架中同样提供这几种效果。
1. .has-warning:警告状态（黄色）
2. .has-error：错误状态（红色）
3. .has-success：成功状态（绿色）
使用的时候只需要在form-group容器上对应添加状态类名。

##### 使用方法

```css
<form role="form">
<div class="form-group has-success">
  <label class="control-label" for="inputSuccess1">成功状态</label>
  <input type="text" class="form-control" id="inputSuccess1" placeholder="成功状态" >
</div>
<div class="form-group has-warning">
  <label class="control-label" for="inputWarning1">警告状态</label>
  <input type="text" class="form-control" id="inputWarning1" placeholder="警告状态">
</div>
<div class="form-group has-error">
  <label class="control-label" for="inputError1">错误状态</label>
  <input type="text" class="form-control" id="inputError1" placeholder="错误状态">
</div>
</form>
```
![](http://ojt6zsxg2.bkt.clouddn.com/5d880e8eb7c8914024a73926f434447f.png)

在表单验证的时候，不同的状态会提供不同的 icon，比如成功是一个对号（√），错误是一个叉号（×）等。在Bootstrap框中也提供了这样的效果。如果你想让表单在对应的状态下显示 icon 出来，只需要在对应的状态下添加类名“has-feedback”。请注意，此类名要与“has-error”、“has-warning”和“has-success”在一起

使用方法如下：

```css
<form role="form">
  <div class="form-group has-success has-feedback">
    <label class="control-label" for="inputSuccess1">成功状态</label>
    <input type="text" class="form-control" id="inputSuccess1" placeholder="成功状态" >
    <span class="glyphicon glyphicon-ok form-control-feedback"></span>
  </div>
  <div class="form-group has-warning has-feedback">
    <label class="control-label" for="inputWarning1">警告状态</label>
    <input type="text" class="form-control" id="inputWarning1" placeholder="警告状态">
    <span class="glyphicon glyphicon-warning-sign form-control-feedback"></span>
  </div>
  <div class="form-group has-error has-feedback">
    <label class="control-label" for="inputError1">错误状态</label>
    <input type="text" class="form-control" id="inputError1" placeholder="错误状态">
    <span class="glyphicon glyphicon-remove form-control-feedback"></span>  
  </div>
</form>
```

**在 Bootstrap 的小图标都是使用@font-face来制作（后面的内容中将会着重用一节内容来介绍）。而且必须在表单中添加了一个 span 元素：**

![](http://ojt6zsxg2.bkt.clouddn.com/7431975a289976c22c691d15ad5274b6.png)

##### css 分析

```css
.has-success .help-block,
.has-success .control-label,
.has-success .radio,
.has-success .checkbox,
.has-success .radio-inline,
.has-success .checkbox-inline,
.has-success.radio label,
.has-success.checkbox label,
.has-success.radio-inline label,
.has-success.checkbox-inline label {
  color: #3c763d;
}
.has-success .form-control {
  border-color: #3c763d;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, .075);
          box-shadow: inset 0 1px 1px rgba(0, 0, 0, .075);
}
.has-success .form-control:focus {
  border-color: #2b542c;
  -webkit-box-shadow: inset 0 1px 1px rgba(0, 0, 0, .075), 0 0 6px #67b168;
          box-shadow: inset 0 1px 1px rgba(0, 0, 0, .075), 0 0 6px #67b168;
}
.has-success .input-group-addon {
  color: #3c763d;
  background-color: #dff0d8;
  border-color: #3c763d;
}
.has-success .form-control-feedback {
  color: #3c763d;
}
```
主要是修改了 color、background-color和 border-color。

### 表单提示信息

#### 使用方法

使用了一个"help-block"样式，将提示信息以块状显示，并且显示在控件底部。

```html
<form role="form">
<div class="form-group has-success has-feedback">
  <label class="control-label" for="inputSuccess1">成功状态</label>
  <input type="text" class="form-control" id="inputSuccess1" placeholder="成功状态" >
  <span class="help-block">你输入的信息是正确的</span>
  <span class="glyphiconglyphicon-ok form-control-feedback"></span>
</div>
</form>
```

![](http://ojt6zsxg2.bkt.clouddn.com/e333b203d6a7d1357365ad9f65a0ae71.png)

或者使用了类名“help-inline”。一般让提示信息显示在控件的后面，也就是同一水平显示。但是这个类是在Bootstrap V2.x版本中才有。如果你想在BootstrapV3.x版本也有这样的效果，你可以添加这段代码：

```
.help-inline{
  display:inline-block;
  padding-left:5px;
  color: #737373;
}
```
 也可以使用 Bootstrap 的网格系统
 
```
<form role="form">
    <div class="form-group has-success">
        <label class="control-label" for="inputSuccess1">成功状态</label>
        <div class="row">
            <div class="col-xs-6">
                <input type="text" class="form-control" id="inputSuccess1" placeholder="成功状态">
            </div>
            <span class="col-xs-6 help-block">你输入的信息是正确的</span>
        </div>
    </div>
</form>
```
 
 ![](http://ojt6zsxg2.bkt.clouddn.com/cba154406f73590c611038c174f7097b.png)

### 图像

在Bootstrap框架中对于图像的样式风格提供以下几种风格：

1.  img-responsive：响应式图片，主要针对于响应式设计
2.  img-rounded：圆角图片
3.  img-circle：圆形图片
4.  img-thumbnail：缩略图片

#### 使用方法

```
<div class="container">
  <div class="row">
    <div class="col-sm-4">
      <img   alt="140x140" src="http://placehold.it/140x140">
        <div>默认图片</div>
    </div>
    <div class="col-sm-4">
      <img  class="img-rounded" alt="140x140" src="http://placehold.it/140x140"> 
        <div>圆角图片</div>
    </div>
    <div class="col-sm-4">
      <img  class="img-circle" alt="140x140" src="http://placehold.it/140x140">
        <div>圆形图片</div>
    </div>
      <div class="row">
        <div class="col-sm-6">
          <img  class="img-thumbnail" alt="140x140" src="http://placehold.it/140x140"> 
            <div>缩略图</div>
        </div>
        <div class="col-sm-6">
          <img  class="img-responsive" alt="140x140" src="http://placehold.it/140x140" /> 
          <div>响应式图片</div>
        </div>
      </div>
  </div>
</div>
```
![](http://ojt6zsxg2.bkt.clouddn.com/c5419c2a91dc19d384e86148d228a7b8.png)

#### css 分析

```
img {
  vertical-align: middle;
}
.img-responsive,
.thumbnail > img,
.thumbnail a > img,
.carousel-inner > .item > img,
.carousel-inner > .item > a > img {
  display: block;
  max-width: 100%;
  height: auto;
}
.img-rounded {
  border-radius: 6px;
}
.img-thumbnail {
  display: inline-block;
  max-width: 100%;
  height: auto;
  padding: 4px;
  line-height: 1.42857143;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 4px;
  -webkit-transition: all .2s ease-in-out;
       -o-transition: all .2s ease-in-out;
          transition: all .2s ease-in-out;
}
.img-circle {
  border-radius: 50%;
}
```

对于圆角图片和圆形图片效果，因为是使用了CSS3的圆角样式来实现的，所以注意对于IE8以及其以下版本不支持，是没有圆角效果的。

### 字体图标(font-face)

#### 使用方法

自定义完字体之后，需要对icon设置一个默认样式，在Bootstrap框架中是通过给元素添加“glyphicon”类名来实现，然后通过伪元素“:before”的“content”属性调取对应的icon编码。所有icon都是以”glyphicon-”前缀的类名开始，然后后缀表示图标的名称。

**所有图标可以在[这个链接](http://getbootstrap.com/components/#glyphicons)**

```
<span class="glyphicon glyphicon-search"></span>
<span class="glyphicon glyphicon-asterisk"></span>
<span class="glyphicon glyphicon-plus"></span>
<span class="glyphicon glyphicon-cloud"></span>
```
![](http://ojt6zsxg2.bkt.clouddn.com/5c45b6615fab0b56cca12a15ba3ec3ef.png)

#### css 分析

```
@font-face {
  font-family: 'Glyphicons Halflings';

  src: url('../fonts/glyphicons-halflings-regular.eot');
  src: url('../fonts/glyphicons-halflings-regular.eot?#iefix') format('embedded-opentype'), url('../fonts/glyphicons-halflings-regular.woff2') format('woff2'), url('../fonts/glyphicons-halflings-regular.woff') format('woff'), url('../fonts/glyphicons-halflings-regular.ttf') format('truetype'), url('../fonts/glyphicons-halflings-regular.svg#glyphicons_halflingsregular') format('svg');
}
.glyphicon {
  position: relative;
  top: 1px;
  display: inline-block;
  font-family: 'Glyphicons Halflings';
  font-style: normal;
  font-weight: normal;
  line-height: 1;

  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
```

## 网格系统

### 工作原理

首先：数据行(.row)必须包含在容器（.container）中，以便为其赋予合适的对齐方式和内距(padding)。如：

```
<div class="container">
<div class="row"></div>
</div>
```

其次：在行(.row)中可以添加列(.column)，但列数之和不能超过平分的总列数，比如12

```
<div class="container">
<div class="row">
  <div class="col-md-4"></div>
  <div class="col-md-8"></div>
```

然后：具体内容应当放置在列容器（column）之内，而且只有列（column）才可以作为行容器(.row)的直接子元素

最后：通过设置内距（padding）从而创建列与列之间的间距。然后通过为第一列和最后一列设置负值的外距（margin）来抵消内距(padding)的影响


![](http://img.mukewang.com/53b0f9c000018b9305540282.jpg)

上面这张图显示的是 Bootstrap 网格系统的工作原理，一共分为5步。

#### 第一步

最外边框，带有一大片白色区域，就是相当于浏览器的可视区域。在Bootstrap框架的网格系统中带有响应式效果，其带有四种类型的浏览器（超小屏(xs)，小屏(sm)，中屏(md)和大屏(lg)），其断点（像素的分界点）是768px、992px和1220px。

#### 第二步

第二个边框(1)相当于容器(.container)。针对不同的浏览器分辨率，其宽度也不一样：自动、750px、970px和1170px

```
.container {
  padding-right: 15px;
  padding-left: 15px;
  margin-right: auto;
  margin-left: auto;
}
@media (min-width: 768px) {
  .container {
    width: 750px;
  }
}
@media (min-width: 992px) {
  .container {
    width: 970px;
  }
}
@media (min-width: 1200px) {
  .container {
    width: 1170px;
  }
}
```

#### 第三步

２号横条阐述的是，将容器的行（.row）平分了12等份，也就是列。每个列都有一个“padding-left:15px”(图中粉红色部分)和一个“padding-right:15px”(图中紫色部分)。这样也导致了第一个列的padding-left和最后一列的padding-right占据了总宽度的30px，从而致使页面不美观，当然，如果你需要留有一定的间距，这个做法是不错的

```
.col-xs-1, .col-sm-1, .col-md-1, .col-lg-1, .col-xs-2, .col-sm-2, .col-md-2, .col-lg-2, .col-xs-3, .col-sm-3, .col-md-3, .col-lg-3, .col-xs-4, .col-sm-4, .col-md-4, .col-lg-4, .col-xs-5, .col-sm-5, .col-md-5, .col-lg-5, .col-xs-6, .col-sm-6, .col-md-6, .col-lg-6, .col-xs-7, .col-sm-7, .col-md-7, .col-lg-7, .col-xs-8, .col-sm-8, .col-md-8, .col-lg-8, .col-xs-9, .col-sm-9, .col-md-9, .col-lg-9, .col-xs-10, .col-sm-10, .col-md-10, .col-lg-10, .col-xs-11, .col-sm-11, .col-md-11, .col-lg-11, .col-xs-12, .col-sm-12, .col-md-12, .col-lg-12 {
  position: relative;
  min-height: 1px;
  padding-right: 15px;
  padding-left: 15px;
}
```

#### 第四步

３号横条就是行容器(.row),其定义了“margin-left”和”margin-right”值为”-15px”，用来抵消第一个列的左内距和最后一列的右内距。

```
.row {
  margin-right: -15px;
  margin-left: -15px;
}
```

#### 第五步

将行与列给合在一起就能看到横条4的效果。也就是我们期望看到的效果，第一列和最后一列与容器（.container）之间没有间距。

### 基本用法

![](http://img.mukewang.com/53e483500001c7f408770494.jpg)

上图是不同的网格大小之间的区别。

#### 使用方法

列组合简单理解就是更改数字来合并列（原则：列总和数不能超12）

```
<div class="container">
  <div class="row">
    <div class="col-md-4">.col-md-4</div>
    <div class="col-md-8">.col-md-8</div>
  </div>
  <div class="row">
    <div class="col-md-4">.col-md-4</div>
    <div class="col-md-4">.col-md-4</div>
    <div class="col-md-4">.col-md-4</div>
  </div>
  <div class="row">
    <div class="col-md-3">.col-md-3</div>
    <div class="col-md-6">.col-md-6</div>
    <div class="col-md-3">.col-md-3</div>
 </div>
</div>
```

#### css 分析

实现列组合方式非常简单，只涉及两个CSS两个特性：浮动与宽度百分比。

```
.col-md-1, .col-md-2, .col-md-3, .col-md-4, .col-md-5, .col-md-6, .col-md-7, .col-md-8, .col-md-9, .col-md-10, .col-md-11, .col-md-12 {
    float: left;
 }
 .col-md-12 {
    width: 100%;
  }
  .col-md-11 {
    width: 91.66666667%;
  }
  .col-md-10 {
    width: 83.33333333%;
  }
  .col-md-9 {
    width: 75%;
  }
  .col-md-8 {
    width: 66.66666667%;
  }
  .col-md-7 {
    width: 58.33333333%;
  }
  .col-md-6 {
    width: 50%;
  }
  .col-md-5 {
    width: 41.66666667%;
  }
  .col-md-4 {
    width: 33.33333333%;
  }
  .col-md-3 {
    width: 25%;
  }
  .col-md-2 {
    width: 16.66666667%;
  }
  .col-md-1 {
    width: 8.33333333%;
  }
```

### 列偏移

我们不希望相邻的两个列紧靠在一起，但又不想使用margin或者其他的技术手段来。这个时候就可以使用列偏移（offset）功能来实现。

#### 使用方法

需要在列元素上添加类名“col-md-offset-*”(其中星号代表要偏移的列组合数)，那么具有这个类名的列就会向右偏移。例如，你在列元素上添加“col-md-offset-4”，表示该列向右移动4个列的宽度。

```
<h4>列向右移动四列的间距</h4>
<div class="container">
  <div class="row">
    <div class="col-md-4">.col-md-4</div>
    <div class="col-md-2 col-md-offset-4">列向右移动四列</div>
    <div class="col-md-2">.col-md-3</div>
  </div>
  <div class="row">
    <div class="col-md-4">.col-md-4</div>
    <div class="col-md-4 col-md-offset-4">列向右移动四列</div>
  </div>
</div>
<br />
<h4>发生行断裂</h4>
<div class="container">
  <div class="row">
    <div class="col-md-4">.col-md-4</div>
    <div class="col-md-2 col-md-offset-4">列向右移动四列</div>
    <div class="col-md-2">.col-md-3</div>
  </div>
  <div class="row">
    <div class="col-md-4">.col-md-4</div>
    <div class="col-md-4 col-md-offset-4">列向右移动四列</div>
  </div>
  <div class="row">
    <div class="col-md-3">.col-md-3</div>
    <div class="col-md-3 col-md-offset-3">col-md-offset-3</div>
    <div class="col-md-4">col-md-4</div>
  </div>
</div>
```
![](http://ojt6zsxg2.bkt.clouddn.com/76565b67a3141c8042fbb2f62510c024.png)

**使用”col-md-offset-*”对列进行向右偏移时，要保证列与偏移列的总数不超过12，不然会致列断行显示**

#### css 分析

```
.col-md-offset-12 {
   margin-left: 100%;
}
  .col-md-offset-11 {
    margin-left: 91.66666667%;
  }
  .col-md-offset-10 {
    margin-left: 83.33333333%;
...
  .col-md-offset-2 {
    margin-left: 16.66666667%;
  }
  .col-md-offset-1 {
    margin-left: 8.33333333%;
  }
  .col-md-offset-0 {
    margin-left: 0;
  }
```
### 列排序

列排序其实就是改变列的方向，就是改变左右浮动，并且设置浮动的距离。在Bootstrap框架的网格系统中是通过添加类名“col-md-push-*”和“col-md-pull-*”

#### 使用方法

```
<div class="container">
  <div class="row">
    <div class="col-md-4 col-md-push-8">.col-md-4</div>
    <div class="col-md-8 col-md-pull-4">.col-md-8</div>
  </div>
</div>
```

![](http://ojt6zsxg2.bkt.clouddn.com/9a4c9d5d466ed9a0927c400db0774dd9.png)

将左边的列右移到8个位置（col-md-push-8），同时将右边的列左移到4个位置（col-md-pull-4）。如果只移动一个列而不移动另一个列，则会导致位置的重叠而成为两行。

#### css 分析

```
  .col-sm-pull-2 {
    right: 16.66666667%;
  }
  .col-sm-pull-1 {
    right: 8.33333333%;
  }
  .col-sm-pull-0 {
    right: auto;
  }
  ...
    .col-sm-push-2 {
    left: 16.66666667%;
  }
  .col-sm-push-1 {
    left: 8.33333333%;
  }
  .col-sm-push-0 {
    left: auto;
  }
```

### 列的嵌套

Bootstrap框架的网格系统还支持列的嵌套。你可以在一个列中添加一个或者多个行（row）容器，然后在这个行容器中插入列（像前面介绍的一样使用列）。但在列容器中的行容器（row），宽度为100%时，就是当前外部列的宽度。

注意：嵌套的列总数也需要遵循不超过12列。不然会造成末位列换行显示。

#### 使用方法

```
<div class="container">
  <div class="row">
    <div class="col-md-8">
      我的里面嵌套了一个网格
      <div class="row">
        <div class="col-md-6">col-md-6</div>
        <div class="col-md-6">col-md-6</div>
      </div>
    </div>
    <div class="col-md-4">col-md-4</div>
  </div>
  <div class="row">
    <div class="col-md-4">.col-md-4</div>
    <div class="col-md-8">
      我的里面嵌套了一个网格
      <div class="row">
        <div class="col-md-4">col-md-4</div>
        <div class="col-md-4">col-md-4</div>
        <div class="col-md-4">col-md-4</div>
      </div>
    </div>
  </div>
</div>
```

![](http://ojt6zsxg2.bkt.clouddn.com/720dd563a4271d42612b02b680de309e.png)

### 下拉菜单

在使用Bootstrap框架的下拉菜单时，必须调用Bootstrap框架提供的bootstrap.js文件。

注意：因为Bootstrap的组件交互效果都是依赖于jQuery库写的插件，所以在使用bootstrap.min.js之前一定要先加载jquery.min.js才会生效果。

```
<script src="http://apps.bdimg.com/libs/jquery/2.1.4/jquery.min.js"></script>
 <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>
```

#### 基本用法

```
<div class="dropdown">
  <button class="btn btn-default dropdown-toggle" type="button" id="dropdownMenu1" data-toggle="dropdown">
    下拉菜单
    <span class="caret"></span>
  </button>
  <ul class="dropdown-menu" role="menu" aria-labelledby="dropdownMenu1">
    <li role="presentation"><a role="menuitem" tabindex="-1" href="#">下拉菜单项</a></li>
    <li role="presentation"><a role="menuitem" tabindex="-1" href="#">下拉菜单项</a></li>
    <li role="presentation"><a role="menuitem" tabindex="-1" href="#">下拉菜单项</a></li>
    <li role="presentation"><a role="menuitem" tabindex="-1" href="#">下拉菜单项</a></li>
  </ul>
</div> 
```
**`<li>`标签中一定要包裹 `<a>`  标签**

首先：使用一个名为“dropdown”的容器包裹了整个下拉菜单元素:

```
<div class="dropdown"></div>
```

其次：使用了一个`<button>`按钮做为父菜单，并且定义类名“dropdown-toggle”和自定义“data-toggle”属性，且值必须和最外容器类名一致

```
<button class="btn btn-default dropdown-toggle" type="button" id="dropdownMenu1" data-toggle="dropdown">
```

最后：下拉菜单项使用一个ul列表，并且定义一个类名为“dropdown-menu”

```
<ul class="dropdown-menu" role="menu" aria-labelledby="dropdownMenu1">
```

#### 原理分析

下拉菜单项默认是**隐藏**的：

```
.dropdown-menu {
  position: absolute; /*设置绝对定位，相对于父元素div.dropdown*/
  top: 100%; /*让下拉菜单项在父菜单项底部，如果父元素不设置相对定位，该元素相对于body元素*/
  left: 0;
  z-index: 1000;/*让下拉菜单项不被其他元素遮盖住*/
  display: none;/*默认隐藏下拉菜单项*/
  float: left;
  min-width: 160px;
  padding: 5px 0;
  margin: 2px 0 0;
  font-size: 14px;
  text-align: left;
  list-style: none;
  background-color: #fff;
  -webkit-background-clip: padding-box;
          background-clip: padding-box;
  border: 1px solid #ccc;
  border: 1px solid rgba(0, 0, 0, .15);
  border-radius: 4px;
  -webkit-box-shadow: 0 6px 12px rgba(0, 0, 0, .175);
          box-shadow: 0 6px 12px rgba(0, 0, 0, .175);
}
```

通过js技术手段，给父容器“div.dropdown”添加或移除类名“open”来控制下拉菜单显示或隐藏。也就是说，默认情况，“div.dropdown”没有类名“open”，当用户第一次点击时，“div.dropdown”会添加类名“open”；当用户再次点击时，“div.dropdown”容器中的类名“open”又会被移除。open 可以控制下拉菜单的显示。

```
.open > .dropdown-menu {
  display: block;
}
```

#### 下拉菜单（下拉分隔线）

在Bootstrap框架中的下拉菜单还提供了下拉分隔线，假设下拉菜单有两个组，那么组与组之间可以通过添加一个空的`<li>`，并且给这个`<li>`添加类名“divider”来实现添加下拉分隔线的功能。

##### 使用方法

```
 <div class="dropdown">
  <button class="btn btn-default dropdown-toggle" type="button" id="dropdownMenu1" data-toggle="dropdown">
    下拉菜单
    <span class="caret"></span>
  </button>
  <ul class="dropdown-menu" role="menu" aria-labelledby="dropdownMenu1">
    <li role="presentation"><a role="menuitem" tabindex="-1" href="#">下拉菜单项</a></li>
    <li role="presentation"><a role="menuitem" tabindex="-1" href="#">下拉菜单项</a></li>
    <li role="presentation"><a role="menuitem" tabindex="-1" href="#">下拉菜单项</a></li>
    <li class="divider"></li>
    <li role="presentation"><a role="menuitem" tabindex="-1" href="#">下拉菜单项</a></li>
  </ul>
</div> 
```

![](http://ojt6zsxg2.bkt.clouddn.com/c19ebabaaf55c3e11f52e1944c6113d6.png)

##### css 分析

```
.dropdown-menu .divider {
  height: 1px;
  margin: 9px 0;
  overflow: hidden;
  background-color: #e5e5e5;
}
```

#### 下拉菜单（菜单标题）


##### 使用方法

通过 li.dropdown-header 来添加菜单头部

```
<div class="dropdown">
  <button class="btn btn-default dropdown-toggle" type="button" id="dropdownMenu1" data-toggle="dropdown">
    下拉菜单
    <span class="caret"></span>
  </button>
  <ul class="dropdown-menu" role="menu" aria-labelledby="dropdownMenu1">
    <li role="presentation" class="dropdown-header">第一部分菜单头部</li>
    <li role="presentation"><a role="menuitem" tabindex="-1" href="#">下拉菜单项</a></li>
    <li role="presentation"><a role="menuitem" tabindex="-1" href="#">下拉菜单项</a></li>
    <li role="presentation"><a role="menuitem" tabindex="-1" href="#">下拉菜单项</a></li>
    <li role="presentation" class="divider"></li>
    <li role="presentation" class="dropdown-header">第二部分菜单头部</li>
    <li role="presentation"><a role="menuitem" tabindex="-1" href="#">下拉菜单项</a></li>
    <li role="presentation"><a role="menuitem" tabindex="-1" href="#">下拉菜单项</a></li>
    <li role="presentation"><a role="menuitem" tabindex="-1" href="#">下拉菜单项</a></li>
  </ul>
</div>
```
![](http://ojt6zsxg2.bkt.clouddn.com/275161340348be49f9d6e8d17e84be61.png)

##### css 分析

```
.dropdown-header {
  display: block;
  padding: 3px 20px;
  font-size: 12px;
  line-height: 1.42857143;
  color: #777;
  white-space: nowrap;
}
```

#### 下拉菜单（对齐方式）

##### 使用方法

Bootstrap框架中下拉菜单默认是左对齐，如果你想让下拉菜单相对于父容器右对齐时，可以在“dropdown-menu”上添加一个“pull-right”或者“dropdown-menu-right”类名

同时一定要为.dropdown添加float:leftcss样式。

```
.dropdown{
  float: left;
}
```

```
<ul class="dropdown-menu dropdown-menu-right" role="menu" aria-labelledby="dropdownMenu1">
    <li role="presentation"><a role="menuitem" tabindex="-1" href="#">下拉菜单项</a></li>
    <li role="presentation"><a role="menuitem" tabindex="-1" href="#">下拉菜单项</a></li>
    <li role="presentation"><a role="menuitem" tabindex="-1" href="#">下拉菜单项</a></li>
    <li role="presentation" class="divider"></li>
    <li role="presentation"><a role="menuitem" tabindex="-1" href="#">下拉菜单项</a></li>
  </ul>
```

![](http://ojt6zsxg2.bkt.clouddn.com/17d2810d3f9456a8d6e38fbd0565b1e2.png)

##### css 分析

```
.dropdown-menu-right {
  right: 0;
  left: auto;
}
.dropdown-menu-left {
  right: auto;
  left: 0;
}
```

#### 下拉菜单（菜单项状态）

下拉菜单项的默认的状态（不用设置）有悬浮状态（:hover）和焦点状态（:focus)

```
.dropdown-menu > li > a:hover,
.dropdown-menu > li > a:focus {
  color: #262626;
  text-decoration: none;
  background-color: #f5f5f5;
}
```

下拉菜单项除了上面两种状态，还有当前状态（.active）和禁用状态（.disabled）。这两种状态使用方法只需要在对应的菜单项上添加对应的类名

##### 使用方法

```
<div class="dropdown">
  <button class="btn btn-default dropdown-toggle" type="button" id="dropdownMenu1" data-toggle="dropdown">
  下拉菜单
  <span class="caret"></span>
  </button>
  <ul class="dropdown-menu" role="menu" aria-labelledby="dropdownMenu1">
    <li role="presentation" class="active"><a role="menuitem" tabindex="-1" href="#">下拉菜单项</a></li>
    ….
    <li role="presentation" class="disabled"><a role="menuitem" tabindex="-1" href="#">下拉菜单项</a></li>
  </ul>
</div>
```

![](http://ojt6zsxg2.bkt.clouddn.com/faaff4d29d07e5f0651541e6a9d1c41b.png)

##### css 分析

```
.dropdown-menu > .active > a,
.dropdown-menu > .active > a:hover,
.dropdown-menu > .active > a:focus {
  color: #fff;
  text-decoration: none;
  background-color: #337ab7;
  outline: 0;
}
.dropdown-menu > .disabled > a,
.dropdown-menu > .disabled > a:hover,
.dropdown-menu > .disabled > a:focus {
  color: #777;
}
.dropdown-menu > .disabled > a:hover,
.dropdown-menu > .disabled > a:focus {
  text-decoration: none;
  cursor: not-allowed;
  background-color: transparent;
  background-image: none;
  filter: progid:DXImageTransform.Microsoft.gradient(enabled = false);
}
```

### 导航

Bootstrap框架中制作导航条主要通过“.nav”样式。默认的“.nav”样式不提供默认的导航样式，必须附加另外一个样式才会有效，比如“nav-tabs”、“nav-pills”之类。

#### 导航（基础样式）

##### 使用方法

为ul标签加入.nav和nav-tabs两个类样式。

```
<ul class="nav nav-tabs">
    <li><a href="##">Home</a></li>
    <li><a href="##">CSS3</a></li>
 	<li><a href="##">Sass</a></li>
 	<li><a href="##">jQuery</a></li>
 	<li class="disabled"><a href="##">Responsive</a></li>
</ul>
```

![](http://ojt6zsxg2.bkt.clouddn.com/aab5bff0f3480978a343259974d21ef6.png)

##### css 分析

```
.nav {
  padding-left: 0;
  margin-bottom: 0;
  list-style: none;
}
.nav > li {
  position: relative;
  display: block;
}
.nav > li > a {
  position: relative;
  display: block;
  padding: 10px 15px;
}
.nav > li > a:hover,
.nav > li > a:focus {
  text-decoration: none;
  background-color: #eee;
}
.nav > li.disabled > a {
  color: #777;
}
.nav > li.disabled > a:hover,
.nav > li.disabled > a:focus {
  color: #777;
  text-decoration: none;
  cursor: not-allowed;
  background-color: transparent;
}
.nav .open > a,
.nav .open > a:hover,
.nav .open > a:focus {
  background-color: #eee;
  border-color: #337ab7;
}
.nav .nav-divider {
  height: 1px;
  margin: 9px 0;
  overflow: hidden;
  background-color: #e5e5e5;
}
.nav > li > a > img {
  max-width: none;
}
```


.nav-tabs 的样式如下：

```
.nav-tabs {
  border-bottom: 1px solid #ddd;
}
.nav-tabs > li {
  float: left;
  margin-bottom: -1px;
}
.nav-tabs > li > a {
  margin-right: 2px;
  line-height: 1.42857143;
  border: 1px solid transparent;
  border-radius: 4px 4px 0 0;
}
.nav-tabs > li > a:hover {
  border-color: #eee #eee #ddd;
}
.nav-tabs > li.active > a,
.nav-tabs > li.active > a:hover,
.nav-tabs > li.active > a:focus {
  color: #555;
  cursor: default;
  background-color: #fff;
  border: 1px solid #ddd;
  border-bottom-color: transparent;
}
```

实现原理是：菜单项（li）按块显示，并且让他们在同一水平上排列，然后定义非高亮菜单的样式和鼠标悬浮效果。

#### 导航（胶囊形(pills)导航）

当前项高亮显示，并带有圆角效果。并且在导航栏下部没有横线。

##### 使用方法

```
<ul class="nav nav-pills">
    <li class="active"><a href="##">Home</a></li>
 	<li><a href="##">CSS3</a></li>
 	<li><a href="##">Sass</a></li>
 	<li><a href="##">jQuery</a></li>
 	<li class="disabled"><a href="##">Responsive</a></li>
</ul>
```

![](http://ojt6zsxg2.bkt.clouddn.com/67408f21974791ce1b13d43f9c3cae33.png)

##### css 分析

```
.nav-pills > li {
  float: left;
}
.nav-pills > li > a {
  border-radius: 4px;
}
.nav-pills > li + li {
  margin-left: 2px;
}
.nav-pills > li.active > a,
.nav-pills > li.active > a:hover,
.nav-pills > li.active > a:focus {
  color: #fff;
  background-color: #337ab7;
}
```

#### 导航（垂直堆叠的导航）

##### 使用方法

在实际运用当中，除了水平导航之外，还有垂直导航，就类似前面介绍的垂直排列按钮一样。制作垂直堆叠导航只需要在“nav-pills”的基础上添加一个“nav-stacked”类名即可

```
<ul class="nav nav-pills nav-stacked">
    <li class="active"><a href="##">Home</a></li>
 	<li><a href="##">CSS3</a></li>
 	<li><a href="##">Sass</a></li>
 	<li><a href="##">jQuery</a></li>
    <li class="nav-divider"></li>
 	<li class="disabled"><a href="##">Responsive</a></li>
</ul>
```

![](http://ojt6zsxg2.bkt.clouddn.com/4596333ed5d2cdba7b66e49aa93f6e39.png)

**nav-stacked 最好不要和 nav-tabs 一起使用，效果不好。**

也可以使用 nav-devider 添加一个分割线。

##### css 分析

```
.nav-stacked > li {
  float: none;
}
.nav-stacked > li + li {
  margin-top: 2px;
  margin-left: 0;
}
```
因为 li 默认就是竖直排列的，所以只需要将原有的 float:left 删除即可。

```
.nav .nav-divider {
  height: 1px;
  margin: 9px 0;
  overflow: hidden;
  background-color: #e5e5e5;
}
```

分界线就是一个高度为1px，带有背景颜色的li。分界线在横向排列的导航栏中没有显示效果。

#### 自适应导航（使用）

自适应导航指的是导航占据容器全部宽度，而且菜单项可以像表格的单元格一样自适应宽度。自适应导航和前面使用“btn-group-justified”制作的自适应按钮组是一样的。只不过在制作自适应导航时更换了另一个类名“nav-justified”。当然他需要和“nav-tabs”或者“nav-pills”配合在一起使用。

##### 使用方法

```
<ul class="nav nav-tabs nav-justified">
  <li class="active"><a href="##">Home</a></li>
  <li><a href="##">CSS3</a></li>
  <li><a href="##">Sass</a></li>
  <li><a href="##">jQuery</a></li>
  <li><a href="##">Responsive</a></li>
</ul>
```

![](http://ojt6zsxg2.bkt.clouddn.com/02ed771ade8a34785b71494e392e8723.png)

##### css 分析

实现原理并不难，列表（`<ul>`）上设置宽度为“100%”，然后每个菜单项(`<li>`)设置了“display:table-cell”，让列表项以模拟表格单元格的形式显示

```
.nav-tabs.nav-justified {
  width: 100%;
  border-bottom: 0;
}
.nav-tabs.nav-justified > li {
  float: none;
}
.nav-tabs.nav-justified > li > a {
  margin-bottom: 5px;
  text-align: center;
}
.nav-tabs.nav-justified > .dropdown .dropdown-menu {
  top: auto;
  left: auto;
}
@media (min-width: 768px) {
  .nav-tabs.nav-justified > li {
    display: table-cell;
    width: 1%;
  }
  .nav-tabs.nav-justified > li > a {
    margin-bottom: 0;
  }
}
.nav-tabs.nav-justified > li > a {
  margin-right: 0;
  border-radius: 4px;
}
.nav-tabs.nav-justified > .active > a,
.nav-tabs.nav-justified > .active > a:hover,
.nav-tabs.nav-justified > .active > a:focus {
  border: 1px solid #ddd;
}
@media (min-width: 768px) {
  .nav-tabs.nav-justified > li > a {
    border-bottom: 1px solid #ddd;
    border-radius: 4px 4px 0 0;
  }
  .nav-tabs.nav-justified > .active > a,
  .nav-tabs.nav-justified > .active > a:hover,
  .nav-tabs.nav-justified > .active > a:focus {
    border-bottom-color: #fff;
  }
}
.nav-tabs.nav-justified > li > a {
  margin-right: 0;
  border-radius: 4px;
}
.nav-tabs.nav-justified > .active > a,
.nav-tabs.nav-justified > .active > a:hover,
.nav-tabs.nav-justified > .active > a:focus {
  border: 1px solid #ddd;
}
@media (min-width: 768px) {
  .nav-tabs.nav-justified > li > a {
    border-bottom: 1px solid #ddd;
    border-radius: 4px 4px 0 0;
  }
  .nav-tabs.nav-justified > .active > a,
  .nav-tabs.nav-justified > .active > a:hover,
  .nav-tabs.nav-justified > .active > a:focus {
    border-bottom-color: #fff;
  }
}
```

这里有一个媒体查询条件：“@media (min-width:768px){…}”表示自适应导航仅在浏览器视窗宽度大于768px才能按上图风格显示。

#### 导航加下拉菜单（二级导航）

##### 使用方法

```
<ul class="nav nav-pills">
  <li class="active"><a href="##">首页</a></li>
  <li class="dropdown">
      <a href="##" class="dropdown-toggle" data-toggle="dropdown">教程<span class="caret"></span></a>
      <ul class="dropdown-menu">
          <li><a href="##">CSS3</a></li>
        <li><a href="##">Sass</a></li>
        <li><a href="##">jQuery</a></li>
        <li><a href="##">Responsive</a></li>
      </ul>
  </li>
 <li><a href="##">关于我们</a></li>
</ul>
```

![](http://ojt6zsxg2.bkt.clouddn.com/4bf8a8e79319e7f1063df139d34a61a4.png)

##### css 分析

```
.nav .open > a,
.nav .open > a:hover,
.nav .open > a:focus {
  background-color: #eee;
  border-color: #337ab7;
}
```

#### 面包屑式导航

##### 使用方法
为ul加入breadcrumb类
```
<ul class="breadcrumb">
  <li><a href="#">首页</a></li>
  <li><a href="#">我的书</a></li>
  <li class="active">《图解CSS3》</li>
</ul> 
```
![](http://ojt6zsxg2.bkt.clouddn.com/6fd1b9027245cda754ca736968634afe.png)

##### css 分析

```
.breadcrumb {
  padding: 8px 15px;
  margin-bottom: 20px;
  list-style: none;
  background-color: #f5f5f5;
  border-radius: 4px;
}
.breadcrumb > li {
  display: inline-block;
}
.breadcrumb > li + li:before {
  padding: 0 5px;
  color: #ccc;
  content: "/\00a0";
}
.breadcrumb > .active {
  color: #777;
}
```
作者是使用li+li:before实现li与li之间的分隔符。使用 li+li:before 可以实现从第二个li 开始起作用。

## 导航条

导航条（navbar）和上一节介绍的导航（nav），就相差一个字，多了一个“条”字。其实在Bootstrap框架中他们还是明显的区别。**在导航条(navbar)中有一个背景色、而且导航条可以是纯链接（类似导航），也可以是表单，还有就是表单和导航一起结合等多种形式**。

### 使用方法

```
<div class="navbar navbar-default" role="navigation">
     <ul class="nav navbar-nav">
     	<li class="active"><a href="##">网站首页</a></li>
        <li><a href="##">系列教程</a></li>
        <li><a href="##">名师介绍</a></li>
        <li><a href="##">成功案例</a></li>
        <li><a href="##">关于我们</a></li>
	 </ul>
</div>
<div class="navbar navbar-default" role="navigation">
  　<div class="navbar-header">
  　    <a href="##" class="navbar-brand">慕课网</a>
  　</div>
     <ul class="nav navbar-nav">
	 	<li class="active"><a href="##">网站首页</a></li>
      <li class="dropdown">
        <a href="##" data-toggle="dropdown" class="dropdown-toggle">系列教程<span class="caret"></span></a>
        <ul class="dropdown-menu">
        	<li><a href="##">CSS3</a></li>
        	<li><a href="##">JavaScript</a></li>
        	<li class="disabled"><a href="##">PHP</a></li>
        </ul>
     </li>
      <li><a href="##">名师介绍</a></li>
      <li><a href="##">成功案例</a></li>
      <li><a href="##">关于我们</a></li>
	 </ul>
  <form action="##" class="navbar-form navbar-left" rol="search">
   	<div class="form-group">
   		<input type="text" class="form-control" placeholder="请输入关键词" />
   	</div>
     <button type="submit" class="btn btn-default">搜索</button>
   </form>
</div>
```

![](http://ojt6zsxg2.bkt.clouddn.com/0b80714252dcbe76ada61cb29e4e1924.png)

### 基础导航条

#### 使用方法

1. 首先在制作导航的列表(`<ul class=”nav”>`)基础上添加类名“navbar-nav”
2. 在列表外部添加一个容器（div），并且使用类名“navbar”和“navbar-default”

```
<div class="navbar navbar-default" role="navigation">
     <ul class="nav navbar-nav">
	 	<li class="active"><a href="##">网站首页</a></li>
        <li><a href="##">系列教程</a></li>
        <li><a href="##">名师介绍</a></li>
        <li><a href="##">成功案例</a></li>
        <li><a href="##">关于我们</a></li>
	 </ul>
</div>
```

![](http://ojt6zsxg2.bkt.clouddn.com/edee21a16de54929f9c413ca7e5f1a92.png)

#### css 分析

```
.navbar {
  position: relative;
  min-height: 50px;
  margin-bottom: 20px;
  border: 1px solid transparent;
}
@media (min-width: 768px) {
  .navbar {
    border-radius: 4px;
  }
}
```

主要功能就是设置左右padding和圆角等效果，但他和颜色相关的样式没有进行任何的设置。

```
.navbar-default {
  background-color: #f8f8f8;
  border-color: #e7e7e7;
}
```
导航条的颜色都是通过“.navbar-default”来进行控制

navbar-nav样式是在导航.nav的基础上重新调整了菜单项的浮动与内外边距。同时也不包括颜色等样式设置

```
.navbar-nav {
  margin: 7.5px -15px;
}
.navbar-nav > li > a {
  padding-top: 10px;
  padding-bottom: 10px;
  line-height: 20px;
}
@media (max-width: 767px) {
  .navbar-nav .open .dropdown-menu {
    position: static;
    float: none;
    width: auto;
    margin-top: 0;
    background-color: transparent;
    border: 0;
    -webkit-box-shadow: none;
            box-shadow: none;
  }
  .navbar-nav .open .dropdown-menu > li > a,
  .navbar-nav .open .dropdown-menu .dropdown-header {
    padding: 5px 15px 5px 25px;
  }
  .navbar-nav .open .dropdown-menu > li > a {
    line-height: 20px;
  }
  .navbar-nav .open .dropdown-menu > li > a:hover,
  .navbar-nav .open .dropdown-menu > li > a:focus {
    background-image: none;
  }
}
@media (min-width: 768px) {
  .navbar-nav {
    float: left;
    margin: 0;
  }
  .navbar-nav > li {
    float: left;
  }
  .navbar-nav > li > a {
    padding-top: 15px;
    padding-bottom: 15px;
  }
}
.navbar-default .navbar-nav > li > a {
  color: #777;
}
.navbar-default .navbar-nav > li > a:hover,
.navbar-default .navbar-nav > li > a:focus {
  color: #333;
  background-color: transparent;
}
.navbar-default .navbar-nav > .active > a,
.navbar-default .navbar-nav > .active > a:hover,
.navbar-default .navbar-nav > .active > a:focus {
  color: #555;
  background-color: #e7e7e7;
}
.navbar-default .navbar-nav > .disabled > a,
.navbar-default .navbar-nav > .disabled > a:hover,
.navbar-default .navbar-nav > .disabled > a:focus {
  color: #ccc;
  background-color: transparent;
}
```

### 为导航条添加标题、二级菜单及状态

在Web页面制作中，常常在菜单前面都会有一个标题（文字字号比其它文字稍大一些），其实在Bootstrap框架也为大家做了这方面考虑，其通过“navbar-header”和“navbar-brand”来实现

#### 使用方法

```
<!--导航条状态及二级菜单-->
<div class="navbar navbar-default" role="navigation">
  　<div class="navbar-header">
  　    <a href="##" class="navbar-brand">慕课网</a>
  　</div>
	<ul class="nav navbar-nav">
	 	<li class="active"><a href="##">网站首页</a></li>
        <li class="dropdown">
          <a href="##" data-toggle="dropdown" class="dropdown-toggle">系列教程<span class="caret"></span></a>
          <ul class="dropdown-menu">
        	<li><a href="##">CSS3</a></li>
        	<li><a href="##">JavaScript</a></li>
        	<li class="disabled"><a href="##">PHP</a></li>
          </ul>
       </li>
       <li><a href="##">名师介绍</a></li>
       <li><a href="##">成功案例</a></li>
       <li><a href="##">关于我们</a></li>
	</ul>
</div>
```

![](http://ojt6zsxg2.bkt.clouddn.com/b51ca45835a02edaf02635a4b4ddc5d8.png)

#### css 分析

```
.navbar-header:before,
.navbar-header:after{
  display: table;
  content: " ";
}
.navbar-header:after{
 clear: both;
}
@media (min-width: 768px) {
  .navbar-header {
    float: left;
  }
}
```
清除了浮动。

```
.navbar-brand {
  float: left;
  height: 50px;
  padding: 15px 15px;
  font-size: 18px;
  line-height: 20px;
}
.navbar-brand:hover,
.navbar-brand:focus {
  text-decoration: none;
}
.navbar-brand > img {
  display: block;
}
.navbar-default .navbar-brand {
  color: #777;
}
.navbar-default .navbar-brand:hover,
.navbar-default .navbar-brand:focus {
  color: #5e5e5e;
  background-color: transparent;
}
```
其样式主要是加大了字体设置。

### 带表单的导航条

有的导航条中会带有搜索表单，比如新浪微博的导航条：
![](http://img.mukewang.com/53edcf9d00013cf506950056.jpg)

在Bootstrap框架中提供了一个“navbar-form”，使用方法很简单，在navbar容器中放置一个带有navbar-form类名的表单

#### 使用方法

```
<div class="navbar navbar-default" role="navigation">
  　<div class="navbar-header">
  　    <a href="##" class="navbar-brand">慕课网</a>
  　</div>
    <ul class="nav navbar-nav">
       <li class="active"><a href="##">网站首页</a></li>
       <li class="dropdown">
          <a href="##" data-toggle="dropdown" class="dropdown-toggle">系列教程<span class="caret"></span></a>
          <ul class="dropdown-menu">
        	<li><a href="##">CSS3</a></li>
        	<li><a href="##">JavaScript</a></li>
        	<li class="disabled"><a href="##">PHP</a></li>
          </ul>
      </li>
      <li><a href="##">名师介绍</a></li>
      <li><a href="##">成功案例</a></li>
      <li><a href="##">关于我们</a></li>
	 </ul>
     <form action="##" class="navbar-form navbar-left" role="search">
   	    <div class="form-group">
   		   <input type="text" class="form-control" placeholder="请输入关键词" />
   	    </div>
        <button type="submit" class="btn btn-default">搜索</button>
     </form>
</div>
```

![](http://ojt6zsxg2.bkt.clouddn.com/f66e7f62869a9af532bcee1085fa2463.png)

“navbar-left”让表单左浮动，更好实现对齐。在Bootstrap框架中，还提供了“navbar-right”样式，让元素在导航条靠右对齐。

#### css 分析

```
@media (min-width: 768px) {
  .navbar-left {
    float: left !important;
  }
  .navbar-right {
    float: right !important;
    margin-right: -15px;
  }
  .navbar-right ~ .navbar-right {
    margin-right: 0;
  }
}
```

这里有一个条件，只有当浏览器视窗宽度大于768px生效。

### 导航条中的按钮、文本和链接

Bootstrap框架的导航条中除了使用navbar-brand中的a元素和navbar-nav的ul和navbar-form之外，还可以使用其他元素。框架提供了三种其他样式：

1. 导航条中的按钮navbar-btn
2. 导航条中的文本navbar-text
3. 导航条中的普通链接navbar-link

但这三种样式在框架中使用时受到一定的限制，需要和navbar-brand、navbar-nav配合起来使用。而且对数量也有一定的限制，一般情况在使用一到两个不会有问题，超过两个就会有问题。

#### 使用方法

使用 navbar-text 的时候要使用 div 包裹 a 标签，而不是使用 ul 包裹 a 标签。

```
<--错误的写法-->
<div class="navbar navbar-default" role="navigation">
  　<div class="navbar-header">
  　    <a href="##" class="navbar-brand">慕课网</a>
  　</div>
	 <ul class="nav navbar-nav">
	 	<li><a href="##" class="navbar-text">Navbar Text</a></li>
	 	<li><a href="##" class="navbar-text">Navbar Text</a></li>
	 	<li><a href="##" class="navbar-text">Navbar Text</a></li>
	 </ul>
</div>
<--正确的写法-->
<div class="navbar navbar-default" role="navigation">
  　<div class="navbar-header">
  　    <a href="##" class="navbar-brand">慕课网</a>
  　</div>
	 <div class="nav navbar-nav">
	 	<a href="##" class="navbar-text">Navbar Text</a>
	 	<a href="##" class="navbar-text">Navbar Text</a>
	 	<a href="##" class="navbar-text">Navbar Text</a>
	 </div>
</div>
```
![](http://ojt6zsxg2.bkt.clouddn.com/f8eb4d5473f25487abd04a0d382e83b7.png)

#### css 分析

```
.navbar-btn {
  margin-top: 8px;
  margin-bottom: 8px;
}
.navbar-btn.btn-sm {
  margin-top: 10px;
  margin-bottom: 10px;
}
.navbar-btn.btn-xs {
  margin-top: 14px;
  margin-bottom: 14px;
}
.navbar-text {
  margin-top: 15px;
  margin-bottom: 15px;
}
@media (min-width: 768px) {
  .navbar-text {
    float: left;
    margin-right: 15px;
    margin-left: 15px;
  }
}
.navbar-default .navbar-link {
  color: #777;
}
.navbar-default .navbar-link:hover {
  color: #333;
}
```

### 固定导航条

很多情况之一，设计师希望导航条固定在浏览器顶部或底部，这种固定式导航条的应用在移动端开发中更为常见。Bootstrap框架提供了两种固定导航条的方式：

1. .navbar-fixed-top：导航条固定在浏览器窗口顶部
2. .navbar-fixed-bottom：导航条固定在浏览器窗口底部

#### 使用方法

使用方法很简单，只需要在制作导航条最外部容器navbar上追加对应的类名即可

```
<div class="navbar navbar-default navbar-fixed-top" role="navigation">
  　<div class="navbar-header">
  　    <a href="##" class="navbar-brand">慕课网</a>
  　</div>
	 <ul class="nav navbar-nav">
	 	<li class="active"><a href="##">网站首页</a></li>
        <li><a href="##">系列教程</a></li>
        <li><a href="##">名师介绍</a></li>
        <li><a href="##">成功案例</a></li>
        <li><a href="##">关于我们</a></li>
	 </ul>
</div>
```
![](http://ojt6zsxg2.bkt.clouddn.com/7b00b05b5a8382500dcd0cb5ac6674a3.png)

#### css 分析

```
  .navbar-fixed-top .navbar-collapse,
  .navbar-static-top .navbar-collapse,
  .navbar-fixed-bottom .navbar-collapse {
    padding-right: 0;
    padding-left: 0;
  }
}
.navbar-fixed-top .navbar-collapse,
.navbar-fixed-bottom .navbar-collapse {
  max-height: 340px;
}
@media (max-device-width: 480px) and (orientation: landscape) {
  .navbar-fixed-top .navbar-collapse,
  .navbar-fixed-bottom .navbar-collapse {
    max-height: 200px;
  }
}
.navbar-fixed-top,
.navbar-fixed-bottom {
  position: fixed;
  right: 0;
  left: 0;
  z-index: 1030;
}
@media (min-width: 768px) {
  .navbar-fixed-top,
  .navbar-fixed-bottom {
    border-radius: 0;
  }
}
.navbar-fixed-top {
  top: 0;
  border-width: 0 0 1px;
}
.navbar-fixed-bottom {
  bottom: 0;
  margin-bottom: 0;
  border-width: 1px 0 0;
}
```
在navbar-fixed-top和navbar-fixed-bottom使用了position：fixed属性，并且设置navbar-fixed-top的top值为0,而navbar-fixed-bottom的bottom值为0。

**从运行效果中大家不难发现，页面主内容顶部和底部都被固定导航条给遮住了。为了避免固定导航条遮盖内容，我们需要在body上做一些处理：**

```
body {
  padding-top: 70px;/*有顶部固定导航条时设置*/
  padding-bottom: 70px;/*有底部固定导航条时设置*/
}
```

**第二种解决方法：**

把固定导航条都放在页面内容前面：

```
<div class="navbar navbar-default navbar-fixed-top" role="navigation">
　…
</div>
<div class="navbar navbar-default navbar-fixed-bottom" role="navigation">
　…
</div>
<div class="content">我是内容</div>
```

在文件中添加下列样式代码：

```
.navbar-fixed-top ~ .content {
   padding-top: 70px;
}
.navbar-fixed-bottom ~ .content {
  padding-bottom: 70px;
}
```

### 响应式导航条

#### 使用方法

1、 保证在窄屏时需要折叠的内容必须包裹在带一个div内，并且为这个div加入collapse、navbar-collapse两个类名。最后为这个div添加一个class类名或者id名。

2、 保证在窄屏时要显示的图标样式（固定写法）：

```
<button class="navbar-toggle" type="button" data-toggle="collapse">
  <span class="sr-only">Toggle Navigation</span>
  <span class="icon-bar"></span>
  <span class="icon-bar"></span>
  <span class="icon-bar"></span>
</button>
```

3、 为button添加data-target=".类名/#id名"，究竞是类名还是id名呢？由需要折叠的div来决定。如：

需要折叠的div代码段：

```
<div class="collapse navbar-collapse" id="example">
      <ul class="nav navbar-nav">
      …
      </ul>
</div>
```

窄屏时显示的图标代码段：

```
<button class="navbar-toggle" type="button" data-toggle="collapse" data-target="#example">
  ...
</button>
```

也可以这么写，需要折叠的div代码段：

```
<div class="collapse navbar-collapse example" >
      <ul class="nav navbar-nav">
      …
      </ul>
</div>
```
窄屏时要显示的图标：

```
<button class="navbar-toggle" type="button" data-toggle="collapse" data-target=".example">
  ...
</button>
```

下面是一个完整的案例：

```
<div class="navbar navbar-default" role="navigation">
  <div class="navbar-header">
     　<!-- .navbar-toggle样式用于toggle收缩的内容，即nav-collapse collapse样式所在元素 -->
       <button class="navbar-toggle" type="button" data-toggle="collapse" data-target=".navbar-responsive-collapse">
         <span class="sr-only">Toggle Navigation</span>
         <span class="icon-bar"></span>
         <span class="icon-bar"></span>
         <span class="icon-bar"></span>
       </button>
       <!-- 确保无论是宽屏还是窄屏，navbar-brand都显示 -->
       <a href="##" class="navbar-brand">慕课网</a>
  </div>
  <!-- 屏幕宽度小于768px时，div.navbar-responsive-collapse容器里的内容都会隐藏，显示icon-bar图标，当点击icon-bar图标时，再展开。屏幕大于768px时，默认显示。 -->
  <div class="collapse navbar-collapse navbar-responsive-collapse">
    	<ul class="nav navbar-nav">
      		<li class="active"><a href="##">网站首页</a></li>
      		<li><a href="##">系列教程</a></li>
      		<li><a href="##">名师介绍</a></li>
      		<li><a href="##">成功案例</a></li>
      		<li><a href="##">关于我们</a></li>
	 	</ul>
  </div>
</div>
```
![](http://ojt6zsxg2.bkt.clouddn.com/692ebe815164e2d08e88b1b707e07a4c.png)

折叠后的显示效果是：

![](http://ojt6zsxg2.bkt.clouddn.com/5cb8ae9ab727b281867cb6e9c066f285.png)

### 反色导航条

#### 使用方法

使用方法并无区别，只是将navbar-deafult类名换成navbar-inverse。其变化只是导航条的背景色和文本做了修改。

```
<div class="navbar navbar-inverse" role="navigation">
  <div class="navbar-header">
     <a href="##" class="navbar-brand">慕课网</a>
  </div>
  <ul class="nav navbar-nav">
      <li class="active"><a href="">首页</a></li>
    <li><a href="">教程</a></li>
    <li><a href="">关于我们</a></li>
  </ul>
</div>
```

![](http://ojt6zsxg2.bkt.clouddn.com/b19b4598d9a201f9ea228a8815319205.png)

### 分页导航（带页码的分页导航）


分页导航几乎在哪个网站都可见。好的分页导航能给用户带来更好的用户体验。在Bootstrap框架中提供了两种分页导航：
1. 带页码的分页导航
2. 带翻页的分页导航

#### 带页码的分页导航

平时很多同学喜欢用div>a和div>span结构来制作带页码的分页导航。不过，在Bootstrap框架中使用的是ul>li>a这样的结构，在ul标签上加入pagination方法。

在Bootstrap框架中，也可以通过几个不同的情况来设置其大小。类似于按钮一样：
1. 通过“pagination-lg”让分页导航变大；
2. 通过“pagination-sm”让分页导航变小：

```
<ul class="pagination pagination-lg">
  <li><a href="#">&laquo;第一页</a></li>
  <li><a href="#">11</a></li>
  <li><a href="#">12</a></li>
  <li class="active"><a href="#">13</a></li>
  <li><a href="#">14</a></li>
  <li><a href="#">15</a></li>
  <li class="disabled"><a href="#">最后一页&raquo;</a></li>
</ul> 
```

![](http://ojt6zsxg2.bkt.clouddn.com/4fcf9513dd76c49b01038dae04f0a803.png)

从效果中可以看出，当前状态页码会高亮显示，而且不能点击。而最后一页是禁用状态，也不能点击。

##### css 分析

```
.pagination > .active > a,
.pagination > .active > span,
.pagination > .active > a:hover,
.pagination > .active > span:hover,
.pagination > .active > a:focus,
.pagination > .active > span:focus {
  z-index: 3;
  color: #fff;
  cursor: default;
  background-color: #337ab7;
  border-color: #337ab7;
}
.pagination > .disabled > span,
.pagination > .disabled > span:hover,
.pagination > .disabled > span:focus,
.pagination > .disabled > a,
.pagination > .disabled > a:hover,
.pagination > .disabled > a:focus {
  color: #777;
  cursor: not-allowed;
  background-color: #fff;
  border-color: #ddd;
}
```
要禁用当前状态和禁用状态不能点击，我们还要依靠js来实现，或者将这两状态下的a标签换成span标签。

#### 分页导航（翻页分页导航）

Bootstrap框架除了提供带页码的分页导航之外还提供了翻页导航。这种分页导航常常在一些简单的网站上看到，比如说个人博客，杂志网站等。这种分页导航是看不到具体的页码，只会提供一个“上一页”和“下一页”的按钮。

##### 使用方法

在实际使用中，翻页分页导航和带页码的分页导航类似，为ul标签加入pager类

```
<ul class="pager">
  <li><a href="#">&laquo;上一页</a></li>
  <li><a href="#">下一页&raquo;</a></li>
</ul> 
<!--左右对齐-->
<ul class="pager">
  <li class="previous"><a href="#">&laquo;上一页</a></li>
  <li class="next"><a href="#">下一页&raquo;</a></li>
</ul> 
<!--禁止状态-->
<ul class="pager">
  <li class="disabled"><span>&laquo;上一页</span></li>
  <li><a href="#">下一页&raquo;</a></li>
</ul>
```

![](http://ojt6zsxg2.bkt.clouddn.com/167c183fcb42bce72812ab559b4c2394.png)

##### css 分析

```
.pager {
  padding-left: 0;
  margin: 20px 0;
  text-align: center;
  list-style: none;
}
.pager li {
  display: inline;
}
.pager li > a,
.pager li > span {
  display: inline-block;
  padding: 5px 14px;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 15px;
}
.pager li > a:hover,
.pager li > a:focus {
  text-decoration: none;
  background-color: #eee;
}
.pager .next > a,
.pager .next > span {
  float: right;
}
.pager .previous > a,
.pager .previous > span {
  float: left;
}
.pager .disabled > a,
.pager .disabled > a:hover,
.pager .disabled > a:focus,
.pager .disabled > span {
  color: #777;
  cursor: not-allowed;
  background-color: #fff;
}
```

## 标签

### 使用方法

```
<h3>Example heading <span class="label label-default">New</span></h3>  
<!--代码-->
<span class="label label-default">默认标签</span>
<span class="label label-primary">主要标签</span>
<span class="label label-success">成功标签</span>
<span class="label label-info">信息标签</span>
<span class="label label-warning">警告标签</span>
<span class="label label-danger">错误标签</span>
```

![](http://ojt6zsxg2.bkt.clouddn.com/cde4ac54f17463f3c926446a8479d02f.png)

### css 分析

```
.label {
  display: inline;
  padding: .2em .6em .3em;
  font-size: 75%;
  font-weight: bold;
  line-height: 1;
  color: #fff;
  text-align: center;
  white-space: nowrap;
  vertical-align: baseline;
  border-radius: .25em;
}
a.label:hover,
a.label:focus {
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}
.label:empty {
  display: none;
}
```

## 徽章

### 使用方法

可以像标签一样，使用span标签来制作，然后为他加入badge类：

```
<a href="#">Inbox <span class="badge">42</span></a> 
<!--navbar-default导航条勋章-->
<div class="navbar navbar-default" role="navigation">
  　<div class="navbar-header">
  　    <a href="##" class="navbar-brand">慕课网</a>
  　</div>
	<ul class="nav navbar-nav">
	 	<li class="active"><a href="##">网站首页</a></li>
        <li><a href="##">系列教程</a></li>
        <li><a href="##">名师介绍</a></li>
        <li><a href="##">成功案例<span class="badge">23</span></a></li>
        <li><a href="##">关于我们</a></li>
	</ul>
</div>
<!--nav-pills导航条勋章-->
<ul class="nav nav-pills">
  <li class="active"><a href="#">Home <span class="badge">42</span></a></li>
  <li><a href="#">Profile</a></li>
  <li><a href="#">Messages <span class="badge">3</span></a></li>
</ul>
<br /> 
<ul class="nav nav-pills nav-stacked" style="max-width: 260px;">
      <li class="active">
        <a href="#">
          <span class="badge pull-right">42</span>
          Home
        </a>
      </li>
      <li><a href="#">Profile</a></li>
      <li>
        <a href="#">
          <span class="badge pull-right">3</span>
          Messages
        </a>
      </li>
</ul>
<br />
<!--按钮勋章-->
<button class="btn btn-primary" type="button">
      Messages <span class="badge">4</span>
</button>
```
![](http://ojt6zsxg2.bkt.clouddn.com/d3ee6e4dea19368b98352950bb345df4.png)

### css 分析

```
.badge {
  display: inline-block;
  min-width: 10px;
  padding: 3px 7px;
  font-size: 12px;
  font-weight: bold;
  line-height: 1;
  color: #fff;
  text-align: center;
  white-space: nowrap;
  vertical-align: middle;
  background-color: #777;
  border-radius: 10px;
}
.badge:empty {
  display: none;
}
```

除了基本的徽章样式以外，还有针对不同的徽章位置定义了不同的样式：
```
.btn .badge {
  position: relative;
  top: -1px;
}
.btn-xs .badge,
.btn-group-xs > .btn .badge {
  top: 0;
  padding: 1px 5px;
}
a.badge:hover,
a.badge:focus {
  color: #fff;
  text-decoration: none;
  cursor: pointer;
}
.list-group-item.active > .badge,
.nav-pills > .active > a > .badge {
  color: #337ab7;
  background-color: #fff;
}
.list-group-item > .badge {
  float: right;
}
.list-group-item > .badge + .badge {
  margin-right: 5px;
}
.nav-pills > li > a > .badge {
  margin-left: 3px;
}
```

## 缩略图

缩略图在网站中最常用的地方就是产品列表页面，一行显示几张图片，有的在图片底下（左侧或右侧）带有标题、描述等信息。Bootstrap框架将这一部独立成一个模块组件。并通过“thumbnail”样式配合bootstrap的网格系统来实现。可以将产品列表页变得更好看。

### 使用方法

```
<div class="container">
    <div class="row">
		<div class="col-xs-6 col-md-3">
			<a href="#" class="thumbnail">
				<img alt="100%x180" src="http://img.mukewang.com/5434eba100014fe906000338.png" style="height: 180px; width: 100%; display: block;" >
			</a>
		</div>
		<div class="col-xs-6 col-md-3">
			<a href="#" class="thumbnail">
				<img alt="100%x180" src="http://img.mukewang.com/5434eba100014fe906000338.png" style="height: 180px; width: 100%; display: block;">
			</a>
		</div>
		<div class="col-xs-6 col-md-3">
			<a href="#" class="thumbnail">
				<img alt="100%x180" src="http://img.mukewang.com/5434eba100014fe906000338.png" style="height: 180px; width: 100%; display: block;">
			</a>
		</div>
		<div class="col-xs-6 col-md-3">
			<a href="#" class="thumbnail">
				<img alt="100%x180" src="http://img.mukewang.com/5434eba100014fe906000338.png" style="height: 180px; width: 100%; display: block;">
			</a>
		</div>
	</div>
</div>
```

配合着网格系统进行显示。

这是小于 768px 的界面显示效果。

![](http://ojt6zsxg2.bkt.clouddn.com/f3665f4abd4603c26eca628a796192d3.png)

大于 768px 界面显示效果。

![](http://ojt6zsxg2.bkt.clouddn.com/3ca4aabd94e2d0f6b263f9fdcd90530a.png)

除了这种方式之外，还可以让缩略图配合标题、描述内容，按钮等

```
<div class="container">
    <div class="row">
		<div class="col-xs-6 col-md-3">
			<a href="#" class="thumbnail">
				<img src="http://img.mukewang.com/5434eba100014fe906000338.png" style="height: 180px; width: 100%; display: block;" alt="">
			</a>
			<div class="caption">
				<h3>Bootstrap框架系列教程</h3>
				<p>Bootstrap框架是一个优秀的前端框，就算您是一位后端程序员或者你是一位不懂设计的前端人员，你也能依赖于Bootstrap制作做优美的网站...</p>
				<p>
					<a href="##" class="btn btn-primary">开始学习</a>
					<a href="##" class="btn btn-info">正在学习</a>
				</p>
			</div>  
		</div>
	...
```

![](http://ojt6zsxg2.bkt.clouddn.com/fad464d845d80deb0e26960effd289a5.png)

### css 分析

```
.thumbnail {
  display: block;
  padding: 4px;
  margin-bottom: 20px;
  line-height: 1.42857143;
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 4px;
  -webkit-transition: border .2s ease-in-out;
       -o-transition: border .2s ease-in-out;
          transition: border .2s ease-in-out;
}
.thumbnail > img,
.thumbnail a > img {
  margin-right: auto;
  margin-left: auto;
}
a.thumbnail:hover,
a.thumbnail:focus,
a.thumbnail.active {
  border-color: #337ab7;
}
.thumbnail .caption {
  padding: 9px;
  color: #333;
}
```

## 警告框



### 使用方法

```
<h2>默认警示框</h2>
<div class="alert alert-success" role="alert">恭喜您操作成功！</div>
<div class="alert alert-info" role="alert">请输入正确的密码</div>
<div class="alert alert-warning" role="alert">您已操作失败两次，还有最后一次机会</div>
<div class="alert alert-danger" role="alert">对不起，您输入的密码有误</div> 
```

![](http://ojt6zsxg2.bkt.clouddn.com/f04241cff82ef52ac047e041e7c4e979.png)

使用可关闭的警世框，只需要在默认的警示框里面添加一个关闭按钮。然后进行三个步骤：

  1、需要在基本警示框“alert”的基础上添加“alert-dismissable”样式。

  2、在button标签中加入class="close"类，实现警示框关闭按钮的样式。

  3、要确保关闭按钮元素上设置了自定义属性：“data-dismiss="alert"”（因为可关闭警示框需要借助于Javascript来检测该属性，从而控制警示框的关闭）

```
<h2>可关闭的警示框</h2>
<div class="alert alert-success alert-dismissable" role="alert">
    <button class="close" type="button" data-dismiss="alert">&times;</button>
    恭喜您操作成功！
</div>
<div class="alert alert-info alert-dismissable" role="alert">
	<button class="close" type="button" data-dismiss="alert">&times;</button>
	请输入正确的密码
</div>
<div class="alert alert-warning alert-dismissable" role="alert">
	<button class="close" type="button" data-dismiss="alert">&times;</button>
	您已操作失败两次，还有最后一次机会
</div>
<div class="alert alert-danger alert-dismissable" role="alert">
	<button class="close" type="button" data-dismiss="alert">&times;</button>
	对不起，您输入的密码有误
</div>
```

![](http://ojt6zsxg2.bkt.clouddn.com/eae4e8c5e87a9fd052beb921a5c9640c.png)

在Bootstrap框架中对警示框里的**链接样式**做了一个高亮显示处理。为不同类型的警示框内的链接进行了加粗处理，并且颜色相应加深。

```
<h2>警示框的链接</h2>
<div class="alert alert-success" role="alert">
    <strong>Well done!</strong> 
    You successfully read 
	<a href="#" class="alert-link">this important alert message</a>
	.
</div>
<div class="alert alert-info" role="alert">
	<strong>Heads up!</strong>
	 This 
	 <a href="#" class="alert-link">alert needs your attention</a>
	 , but it's not super important.
</div>
<div class="alert alert-warning" role="alert">
	<strong>Warning!</strong>
	 Better check yourself, you're 
	 <a href="#" class="alert-link">not looking too good</a>
	 .
</div>
<div class="alert alert-danger" role="alert">
	<strong>Oh snap!</strong>
	<a href="#" class="alert-link">Change a few things up</a>
	 and try submitting again.
</div>
```

![](http://ojt6zsxg2.bkt.clouddn.com/f8fa496279673f989d322dfa417fdecd.png)

### css 分析

```
.alert {
  padding: 15px;
  margin-bottom: 20px;
  border: 1px solid transparent;
  border-radius: 4px;
}
.alert h4 {
  margin-top: 0;
  color: inherit;
}
.alert .alert-link {
  font-weight: bold;
}
.alert > p,
.alert > ul {
  margin-bottom: 0;
}
.alert > p + p {
  margin-top: 5px;
}
.alert-dismissable,
.alert-dismissible {
  padding-right: 35px;
}
.alert-dismissable .close,
.alert-dismissible .close {
  position: relative;
  top: -2px;
  right: -21px;
  color: inherit;
}
.alert-success {
  color: #3c763d;
  background-color: #dff0d8;
  border-color: #d6e9c6;
}
.alert-success hr {
  border-top-color: #c9e2b3;
}
.alert-success .alert-link {
  color: #2b542c;
}
```

## 进度条

### 使用方法

```
<h2>基本进度条</h2>
<div class="progress">
     <div class="progress-bar" style="width:40%">
    </div>
</div> 
<h2>彩色进度条</h2>
<div class="progress">
    <div class="progress-bar progress-bar-success" style="width:40%"></div>
</div> 
<div class="progress">
     <div class="progress-bar progress-bar-info" style="width:60%"></div>
</div> 
<div class="progress">
 	<div class="progress-bar progress-bar-warning" style="width:80%"></div>
</div> 
<div class="progress">
 	<div class="progress-bar progress-bar-danger" style="width:50%"></div>
</div> 
```

![](http://ojt6zsxg2.bkt.clouddn.com/c23a2631c8146393095c0d9d7c1f3a12.png)

虽然这样实现了基本进度条效果，但对于残障人员浏览网页有点困难，所以我们可以将结构做得更好些（语义化更友好些）：

```
<div class="progress">
    <div class="progress-bar" style="width:40%;" role="progressbar" aria-valuenow="40" aria-valuemin="0" aria-valuemax="100">
        <span class="sr-only">40% Complete</span>
    </div>
</div>
```

1. role属性作用：告诉搜索引擎这个div的作用是进度条。
2. aria-valuenow="40"属性作用：当前进度条的进度为40%。
3. aria-valuemin="0"属性作用：进度条的最小值为0%。
4. aria-valuemax="100"属性作用：进度条的最大值为100%。

```
<h2>条纹进度条</h2>
<div class="progress progress-striped">
    <div class="progress-bar progress-bar-success" style="width:40%"></div>
</div>
<div class="progress progress-striped">
    <div class="progress-bar progress-bar-info" style="width:60%"></div>
</div>
<div class="progress progress-striped">
	<div class="progress-bar progress-bar-warning" style="width:80%"></div>
</div>
<div class="progress progress-striped">
	<div class="progress-bar progress-bar-danger" style="width:50%"></div>
</div>
```

![](http://ojt6zsxg2.bkt.clouddn.com/49bb8f8118070a1295d1c87e8d1db6b9.png)

```
<h2>动态条纹进度条</h2>
<div class="progress progress-striped active">
    <div class="progress-bar progress-bar-success" style="width:40%"></div>
</div> 
<div class="progress progress-striped active">
    <div class="progress-bar progress-bar-info" style="width:60%"></div>
</div> 
<div class="progress progress-striped active">
	<div class="progress-bar progress-bar-warning" style="width:80%"></div>
</div> 
<div class="progress progress-striped active">
	<div class="progress-bar progress-bar-danger" style="width:50%"></div>
</div>
```

![](http://ojt6zsxg2.bkt.clouddn.com/image/gif/Kapture%202017-01-26%20at%2016.03.45.gif)

```
<h2>层叠进度条</h2>
<h5>正常层叠进度条</h5>
<div class="progress">
    <div class="progress-bar progress-bar-success" style="width:20%"></div>
    <div class="progress-bar progress-bar-info" style="width:10%"></div>
    <div class="progress-bar progress-bar-warning" style="width:30%"></div>
    <div class="progress-bar progress-bar-danger" style="width:15%"></div>
</div> 
<h5>不良效果层叠进度条</h5> 
<div class="progress">
    <div class="progress-bar progress-bar-success" style="width:20%"></div>
	<div class="progress-bar progress-bar-info" style="width:40%"></div>
	<div class="progress-bar progress-bar-warning" style="width:30%"></div>
	<div class="progress-bar progress-bar-danger" style="width:45%"></div>
</div> 
<h5>层叠条纹进度条</h5>
<div class="progress">
	<div class="progress-bar progress-bar-success" style="width:20%"></div>
	<div class="progress-bar progress-bar-info" style="width:20%"></div>
	<div class="progress-bar progress-bar-warning" style="width:30%"></div>
	<div class="progress-bar progress-bar-danger" style="width:15%"></div>
</div>  
<div class="progress">
	<div class="progress-bar progress-bar-success progress-bar-striped" style="width:20%"></div>
	<div class="progress-bar progress-bar-info progress-bar-striped" style="width:20%"></div>
	<div class="progress-bar progress-bar-striped progress-bar-warning" style="width:30%"></div>
	<div class="progress-bar progress-bar-danger progress-bar-striped" style="width:15%"></div>
</div> 
<div class="progress">
	<div class="progress-bar progress-bar-success" style="width:20%"></div>
	<div class="progress-bar progress-bar-info progress-bar-striped" style="width:20%"></div>
	<div class="progress-bar progress-bar-warning" style="width:30%"></div>
	<div class="progress-bar progress-bar-danger progress-bar-striped" style="width:15%"></div>
</div>
```

![](http://ojt6zsxg2.bkt.clouddn.com/b08f4603c875cf60730220f36e2fe205.png)

```
<h2>带Label的进度条</h2>
<h5>进度条1</h5>
<div class="progress">
    <div class="progress-bar progress-bar-success"  role="progressbar" aria-valuenow="20" aria-valuemin="0" aria-valuemax="100" style="width:20%">20%</div>  
</div>  
<div class="progress">
    <div class="progress-bar progress-bar-info" role="progressbar" aria-valuenow="70" aria-valuemin="0" aria-valuemax="100"   style="width:70%">70%</div>
</div>
<div class="progress">
	<div class="progress-bar progress-bar-warning"  role="progressbar" aria-valuenow="30" aria-valuemin="0" aria-valuemax="100" style="width:30%">30%</div>
</div>
<div class="progress">
	<div class="progress-bar progress-bar-danger" role="progressbar" aria-valuenow="15" aria-valuemin="0" aria-valuemax="100" style="width:15%">15%</div>
</div>

<h5>进度条2</h5> 
<div class="progress">
  <div class="progress-bar" role="progressbar" aria-valuenow="0" aria-valuemin="0" aria-valuemax="100">0%</div>
</div>
```

![](http://ojt6zsxg2.bkt.clouddn.com/41786c7ddc55828c41fd4cfb62002daf.png)

### css 分析

```
.progress {
  height: 20px;
  margin-bottom: 20px;
  overflow: hidden;
  background-color: #f5f5f5;
  border-radius: 4px;
  -webkit-box-shadow: inset 0 1px 2px rgba(0, 0, 0, .1);
          box-shadow: inset 0 1px 2px rgba(0, 0, 0, .1);
}
.progress-bar {
  float: left;
  width: 0;
  height: 100%;
  font-size: 12px;
  line-height: 20px;
  color: #fff;
  text-align: center;
  background-color: #337ab7;
  -webkit-box-shadow: inset 0 -1px 0 rgba(0, 0, 0, .15);
          box-shadow: inset 0 -1px 0 rgba(0, 0, 0, .15);
  -webkit-transition: width .6s ease;
       -o-transition: width .6s ease;
          transition: width .6s ease;
}
.progress-bar-success {
  background-color: #5cb85c;
}
```

progres样式主要设置进度条容器的背景色，容器高度、间距等。而progress-bar样式在设置进度方向，重要的是设置了进度条的背景颜色和过渡效果。


```
.progress-striped .progress-bar,
.progress-bar-striped {
  background-image: -webkit-linear-gradient(45deg, rgba(255, 255, 255, .15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, .15) 50%, rgba(255, 255, 255, .15) 75%, transparent 75%, transparent);
  background-image:      -o-linear-gradient(45deg, rgba(255, 255, 255, .15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, .15) 50%, rgba(255, 255, 255, .15) 75%, transparent 75%, transparent);
  background-image:         linear-gradient(45deg, rgba(255, 255, 255, .15) 25%, transparent 25%, transparent 50%, rgba(255, 255, 255, .15) 50%, rgba(255, 255, 255, .15) 75%, transparent 75%, transparent);
  -webkit-background-size: 40px 40px;
          background-size: 40px 40px;
}
```
实现条纹进度条，主要使用的是CSS3的线性渐变

```
@keyframes progress-bar-stripes {
  from {
    background-position: 40px 0;
  }
  to {
    background-position: 0 0;
  }
}
.progress.active .progress-bar,
.progress-bar.active {
  -webkit-animation: progress-bar-stripes 2s linear infinite;
       -o-animation: progress-bar-stripes 2s linear infinite;
          animation: progress-bar-stripes 2s linear infinite;
}
```
为了让条纹进度条动起来，Bootstrap框架还提供了一种动态条纹进度条。其实现原理主要通过CSS3的animation来完成。首先通过@keyframes创建了一个progress-bar-stripes的动画，这个动画主要做了一件事，就是改变背景图像的位置，也就是background-position的值。因为条纹进度条是通过CSS3的线性渐变来制作的，而linear-gradient实现的正是对应背景中的背景图片。
@keyframes仅仅是创建了一个动画效果，如果要让进度条真正的动起来，我们需要通过一定的方式调用@keyframes创建的动画“progress-bar-stripes”，并且通过一个事件触发动画生效。在Bootstrap框架中，通过给进度条容器“progress”添加一个类名“active”，并让文档加载完成就触“progress-bar-stripes”动画生效。

## 媒体对象

媒体对象一般是成组出现，而一组媒体对象常常包括以下几个部分：
1. 媒体对像的容器：常使用“media”类名表示，用来容纳媒体对象的所有内容
2. 媒体对像的对象：常使用“media-object”表示，就是媒体对象中的对象，常常是图片
3. 媒体对象的主体：常使用“media-body”表示，就是媒体对像中的主体内容，可以是任何元素，常常是图片侧边内容
4. 媒体对象的标题：常使用“media-heading”表示，就是用来描述对象的一个标题，此部分可选

如图所示：

![](http://img.mukewang.com/54192bd200016f6306660264.jpg)

除了上面四个部分之外，在Bootstrap框架中还常常使用“pull-left”或者“pull-right”来控制媒体对象中的对象浮动方式。

### 使用方法

```
<div class="media">
    <a class="pull-left" href="#">
    	<img class="media-object" src="http://img.mukewang.com/52e1d29d000161fe06000338-300-170.jpg" alt="...">
  	</a>
  	<div class="media-body">
    	<h4 class="media-heading">系列：十天精通CSS3</h4>
    	<div>全方位深刻详解CSS3模块知识，经典案例分析，代码同步调试，让网页穿上绚丽装备！</div>
  	</div>
</div>
```
![](http://ojt6zsxg2.bkt.clouddn.com/e79af5cff9d0593da014d746e774b047.png)

```
<h3>媒体对象的嵌套</h3>
<div class="media">
    <a class="pull-left" href="#">
    	<img class="media-object" src="http://a.disquscdn.com/uploads/users/3740/2069/avatar92.jpg?1406972031" alt="...">
	</a>
	<div class="media-body">
		<h4 class="media-heading">我是大漠</h4>
		<div>我是W3cplus站长大漠，我在写Bootstrap框中的媒体对象测试用例</div>
		<div class="media">
			<a class="pull-left" href="#">
				<img class="media-object" src="http://tp2.sinaimg.cn/3306361973/50/22875318196/0" alt="...">
			</a>
			<div class="media-body">
				<h4 class="media-heading">慕课网</h4>
				<div>大漠写的《玩转Bootstrap》系列教程即将会在慕课网上发布</div>
				<div class="media">
					<a class="pull-left" href="#">
						<img class="media-object" src="http://tp4.sinaimg.cn/1167075935/50/22838101204/1" alt="...">
					</a>
					<div class="media-body">
						<h4 class="media-heading">W3cplus</h4>
						<div>W3cplus站上还有很多教程....</div>
					</div>
				</div>
			</div>
		</div>
	</div>
</div>
```

![](http://ojt6zsxg2.bkt.clouddn.com/53fff3478820ad0ca6c75134c2de732a.png)

```
<h3>媒体对象列表</h3>
<ul class="media-list">
    <li class="media">
        <a class="pull-left" href="#">
            <img class="media-object" src="http://a.disquscdn.com/uploads/users/3740/2069/avatar92.jpg?1406972031" alt="...">
        </a>
        <div class="media-body">
            <h4 class="media-heading">我是大漠</h4>
            <div>我是W3cplus站长大漠，我在写Bootstrap框中的媒体对象测试用例</div>
        </div>
    </li>
    <li class="media">
        <a class="pull-left" href="#">
            <img class="media-object" src="http://tp2.sinaimg.cn/3306361973/50/22875318196/0" alt="...">
        </a>
        <div class="media-body">
            <h4 class="media-heading">慕课网</h4>
            <div>大漠写的《玩转Bootstrap》系列教程即将会在慕课网上发布</div>
        </div>
    </li>
    <li class="media">
        <a class="pull-left" href="#">
            <img class="media-object" src="http://tp4.sinaimg.cn/1167075935/50/22838101204/1" alt="...">
        </a>
        <div class="media-body">
            <h4 class="media-heading">W3cplus</h4>
            <div>W3cplus站上还有很多教程....</div>
        </div>
    </li>
</ul>
```

![](http://ojt6zsxg2.bkt.clouddn.com/5fefbeedd21a649aa81044d2766891e3.png)

### css 分析

```
.media {
  margin-top: 15px;
}
.media:first-child {
  margin-top: 0;
}
.media,
.media-body {
  overflow: hidden;
  zoom: 1;
}
.media-body {
  width: 10000px;
}
.media-object {
  display: block;
}
.media-object.img-thumbnail {
  max-width: none;
}
.media-right,
.media > .pull-right {
  padding-left: 10px;
}
.media-left,
.media > .pull-left {
  padding-right: 10px;
}
.media-left,
.media-right,
.media-body {
  display: table-cell;
  vertical-align: top;
}
.media-middle {
  vertical-align: middle;
}
.media-bottom {
  vertical-align: bottom;
}
.media-heading {
  margin-top: 0;
  margin-bottom: 5px;
}
.media-list {
  padding-left: 0;
  list-style: none;
}
```
媒体对象样式相对来说比较简单，只是设置他们之间的间距

## 列表组

相比于列表有了更多的显示效果。

### 使用方法

```
<h3>基础列表组</h3>
<ul class="list-group">
    <li class="list-group-item">揭开CSS3的面纱</li>
    <li class="list-group-item">CSS3选择器</li>
	<li class="list-group-item">CSS3边框</li>
	<li class="list-group-item">CSS3背景</li>
	<li class="list-group-item">CSS3文本</li>
</ul>
```
![](http://ojt6zsxg2.bkt.clouddn.com/1de7a10c51f3d1348c0e86b03b3c567b.png)

```
<h3>带徽章的列表组</h3>
<ul class="list-group">
    <li class="list-group-item">
    	<span class="badge">13</span>揭开CSS3的面
	</li>
	<li class="list-group-item">
		<span class="badge">456</span>CSS3选择器
	</li>
	<li class="list-group-item">
		<span class="badge">892</span>CSS3边框
	</li>
	<li class="list-group-item">
		<span class="badge">90</span>CSS3背景
	</li>
	<li class="list-group-item">
		<span class="badge">1290</span>CSS3文本
	</li>
</ul>
```
![](http://ojt6zsxg2.bkt.clouddn.com/e980ef6a953516a5acafacbadb4608a3.png)

```
<h3>带链接的列表组</h3>
<ul class="list-group">
    <li class="list-group-item">
    	<a href="##">揭开CSS3的面</a>
	</li>
	<li class="list-group-item">
		<a href="##">CSS3选择器</a>
	</li>
	<li class="list-group-item">
		<a href="##">CSS3边框</a>
	</li>
	<li class="list-group-item">
		<a href="##">CSS3背景</a>
	</li>
	<li class="list-group-item">
		<a href="##">CSS3文本</a>
	</li>
</ul>
<div class="list-group">
	<a href="##" class="list-group-item">图解CSS3</a>
	<a href="##" class="list-group-item"><span class="badge">220</span>Sass教程</a>
	<a href="##" class="list-group-item">玩转Bootstrap</a>
</div>
```
这样做有一个不足之处，就是链接的点击区域只在文本上有效，但很多时候，都希望在列表项的任何区域都具备可点击。这个时候就需要在链接标签上增加额外的样式：“display:block”。虽然这样能解决问题，达到需求。但在Bootstrap框架中，还是采用了另一种实现方式。就是将ul.list-group使用div.list-group来替换，而li.list-group-item直接用a.list-group-item来替换。这样就可以达到需要的效果

![](http://ojt6zsxg2.bkt.clouddn.com/ee7cc45aac2b473e7831b9554af4f6d2.png)

```
<h3>自定义列表组</h3>
<div class="list-group">
    <a href="##" class="list-group-item">
    	<h4 class="list-group-item-heading">图解CSS3</h4>
		<p class="list-group-item-text">详细讲解了选择器、边框、背景、文本、颜色、盒模型、伸缩布局盒模型、多列布局、渐变、过渡、动画、媒体、响应Web设计、Web字体等主题下涵盖的所有CSS3新特性...</p>
	</a>
	<a href="##" class="list-group-item">
		<h4 class="list-group-item-heading">Sass中国</h4>
		<p class="list-group-item-text">致力于为中国开发者提供最全面，最具影响力，最前沿的Sass相关技术与教程...</p>
	</a>
</div>
```
Bootstrap框加在链接列表组的基础上新增了两个样式：
1. list-group-item-heading：用来定义列表项头部样式
2. list-group-item-text：用来定义列表项主要内容

![](http://ojt6zsxg2.bkt.clouddn.com/2f3637e36c14a41d9804591863073977.png)

```
<h3>组合列表项的状态</h3>
<div class="list-group">
    <a href="##" class="list-group-item active"><span class="badge">5902</span>图解CSS3</a>
    <a href="##" class="list-group-item"><span class="badge">15902</span>W3cplus</a>
	<a href="##" class="list-group-item"><span class="badge">59020</span>慕课网</a>
	<a href="##" class="list-group-item disabled"><span class="badge">0</span>Sass中国</a>
</div>
```
![](http://ojt6zsxg2.bkt.clouddn.com/e0d4b1ec6ed6eda66438c4f3952b678c.png)

```
<h3>多彩列表组</h3>
<div class="list-group">
    <a href="##" class="list-group-item active"><span class="badge">5902</span>图解CSS3</a>
    <a href="##" class="list-group-item list-group-item-success"><span class="badge">15902</span>W3cplus</a>
	<a href="##" class="list-group-item list-group-item-info"><span class="badge">59020</span>慕课网</a>
	<a href="##" class="list-group-item list-group-item-warning"><span class="badge">0</span>Sass中国</a>
	<a href="##" class="list-group-item list-group-item-danger"><span class="badge">10</span>Mobile教程</a>
</div>
```
![](http://ojt6zsxg2.bkt.clouddn.com/6a1d9189c5177109083c8186724ab345.png)

### css 分析

```
.list-group {
  padding-left: 0;
  margin-bottom: 20px;
}
.list-group-item {
  position: relative;
  display: block;
  padding: 10px 15px;
  margin-bottom: -1px;
  background-color: #fff;
  border: 1px solid #ddd;
}
.list-group-item:first-child {
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
}
.list-group-item:last-child {
  margin-bottom: 0;
  border-bottom-right-radius: 4px;
  border-bottom-left-radius: 4px;
}
```
对于基础列表组并没有做过多的样式设置，主要设置了其间距，边框和圆角等

```
a.list-group-item .list-group-item-heading,
button.list-group-item .list-group-item-heading {
  color: #333;
}
.list-group-item.disabled .list-group-item-text,
.list-group-item.disabled:hover .list-group-item-text,
.list-group-item.disabled:focus .list-group-item-text {
  color: #777;
}
.list-group-item.active .list-group-item-text,
.list-group-item.active:hover .list-group-item-text,
.list-group-item.active:focus .list-group-item-text {
  color: #c7ddef;
}
```
这两个样式主要控制不同状态下的文本颜色

```
.list-group-item-success {
  color: #3c763d;
  background-color: #dff0d8;
}
a.list-group-item-success,
button.list-group-item-success {
  color: #3c763d;
}
a.list-group-item-success .list-group-item-heading,
button.list-group-item-success .list-group-item-heading {
  color: inherit;
}
a.list-group-item-success:hover,
button.list-group-item-success:hover,
a.list-group-item-success:focus,
button.list-group-item-success:focus {
  color: #3c763d;
  background-color: #d0e9c6;
}
a.list-group-item-success.active,
button.list-group-item-success.active,
a.list-group-item-success.active:hover,
button.list-group-item-success.active:hover,
a.list-group-item-success.active:focus,
button.list-group-item-success.active:focus {
  color: #fff;
  background-color: #3c763d;
  border-color: #3c763d;
}
```
仅修改了背景色和文本色

## 面板

### 使用方法

```
<h3>基础面板</h3>
<div class="panel panel-default">
    <div class="panel-body">我是一个基础面板，带有默认主题样式风格</div>
</div>
<h3>带有头和尾的面板</h3>
<div class="panel panel-default">
    <div class="panel-heading">图解CSS3</div>
    <div class="panel-body">详细讲解了选择器、边框、背景、文本、颜色、盒模型、伸缩布局盒模型、多列布局、渐变、过渡、动画、媒体、响应Web设计、Web字体等主题下涵盖的所有CSS3新特性
	</div>
	<div class="panel-footer">作者：大漠</div>
</div>
<h3>彩色面板</h3>
<div class="panel panel-default">
    <div class="panel-heading">图解CSS3</div>
    <div class="panel-body">			详细讲解了选择器、边框、背景、文本、颜色、盒模型、伸缩布局盒模型、多列布局、渐变、过渡、动画、媒体、响应Web设计、Web字体等主题下涵盖的所有CSS3新特性
	</div>
	<div class="panel-footer">作者：大漠</div>
</div>
<div class="panel panel-primary">
	<div class="panel-heading">图解CSS3</div>
	<div class="panel-body">详细讲解了选择器、边框、背景、文本、颜色、盒模型、伸缩布局盒模型、多列布局、渐变、过渡、动画、媒体、响应Web设计、Web字体等主题下涵盖的所有CSS3新特性</div>
	<div class="panel-footer">作者：大漠</div>
</div>
<div class="panel panel-success">
	<div class="panel-heading">图解CSS3</div>
	<div class="panel-body">详细讲解了选择器、边框、背景、文本、颜色、盒模型、伸缩布局盒模型、多列布局、渐变、过渡、动画、媒体、响应Web设计、Web字体等主题下涵盖的所有CSS3新特性</div>
	<div class="panel-footer">作者：大漠</div>
</div>
<div class="panel panel-info">
	<div class="panel-heading">图解CSS3</div>
	<div class="panel-body">详细讲解了选择器、边框、背景、文本、颜色、盒模型、伸缩布局盒模型、多列布局、渐变、过渡、动画、媒体、响应Web设计、Web字体等主题下涵盖的所有CSS3新特性</div>
	<div class="panel-footer">作者：大漠</div>
</div>
<div class="panel panel-warning">
	<div class="panel-heading">图解CSS3</div>
	<div class="panel-body">详细讲解了选择器、边框、背景、文本、颜色、盒模型、伸缩布局盒模型、多列布局、渐变、过渡、动画、媒体、响应Web设计、Web字体等主题下涵盖的所有CSS3新特性</div>
	<div class="panel-footer">作者：大漠</div>
</div>
<div class="panel panel-danger">
	<div class="panel-heading">图解CSS3</div>
	<div class="panel-body">详细讲解了选择器、边框、背景、文本、颜色、盒模型、伸缩布局盒模型、多列布局、渐变、过渡、动画、媒体、响应Web设计、Web字体等主题下涵盖的所有CSS3新特性</div>
	<div class="panel-footer">作者：大漠</div>
</div>
```

![](http://ojt6zsxg2.bkt.clouddn.com/fa0c6f287a2dc81bf12179fb0e3aab14.png)

![](http://ojt6zsxg2.bkt.clouddn.com/d18691752f36d570025350ae840f6fad.png)

![](http://ojt6zsxg2.bkt.clouddn.com/7c3dac651e23d1460bb34db0931ef57d.png)

一般情况下可以把面板理解为一个区域，在使用面板的时候，都会在panel-body放置需要的内容，可能是图片、表格或者列表等。来看看面板中嵌套表格和列表组的一个效果。

```
<h3>面板中嵌套表格</h3>
<div class="panel panel-default">
    <div class="panel-heading">图解CSS3</div>
    <div class="panel-body">
		<p>详细讲解了选择器、边框、背景、文本、颜色、盒模型、伸缩布局盒模型、多列布局、渐变、过渡、动画、媒体、响应Web设计、Web字体等主题下涵盖的所有CSS3新特性
		</p>
		<table class="table table-bordered">
			<thead>
				<tr>
					<th>＃</th>
					<th>我的书</th>
					<th>发布时间</th>
				</tr>
			</thead>
			<tbody>
				<tr>
					<td>1</td>
					<td>《图解CSS3》</td>
					<td>2014-07-10</td>
				</tr>
			</tbody>
		</table>
	</div>
	<div class="panel-footer">作者：大漠</div>
</div>
```
![](http://ojt6zsxg2.bkt.clouddn.com/2ea399e06455ae499769f6627a2af2fc.png)

在实际应用运中，你或许希望表格和面板边缘不需要有任何的间距。但由于panel-body设置了一个padding：15px的值，为了实现这样的效果。我们在实际使用的时候需要把table提取到panel-body外面

![](http://ojt6zsxg2.bkt.clouddn.com/08c4f599b72d296a83ce4f9de0caea3f.png)

```
<h3>面板中嵌套列表组（一）</h3>
<div class="panel panel-default">
    <div class="panel-heading">图解CSS3</div>
	<div class="panel-body">
		<p>详细讲解了选择器、边框、背景、文本、颜色、盒模型、伸缩布局盒模型、多列布局、渐变、过渡、动画、媒体、响应Web设计、Web字体等主题下涵盖的所有CSS3新特性
		</p>
		<ul class="list-group">
			<li class="list-group-item">我是列表项</li>
			<li class="list-group-item">我是列表项</li>
			<li class="list-group-item">我是列表项</li>
		</ul>
	</div>
	<div class="panel-footer">作者：大漠</div>
</div>

<h3>面板中嵌套列表组（二）</h3>
<div class="panel panel-default">
	<div class="panel-heading">图解CSS3</div>
	<div class="panel-body">
		<p>详细讲解了选择器、边框、背景、文本、颜色、盒模型、伸缩布局盒模型、多列布局、渐变、过渡、动画、媒体、响应Web设计、Web字体等主题下涵盖的所有CSS3新特性
		</p>
	</div>
	<ul class="list-group">
		<li class="list-group-item">我是列表项</li>
		<li class="list-group-item">我是列表项</li>
		<li class="list-group-item">我是列表项</li>
	</ul>
	<div class="panel-footer">作者：大漠</div>
</div>
```
![](http://ojt6zsxg2.bkt.clouddn.com/3a56296daa8d1465ed50d89678b1ab37.png)

### css 分析

```
.panel {
  margin-bottom: 20px;
  background-color: #fff;
  border: 1px solid transparent;
  border-radius: 4px;
  -webkit-box-shadow: 0 1px 1px rgba(0, 0, 0, .05);
          box-shadow: 0 1px 1px rgba(0, 0, 0, .05);
}
.panel-body {
  padding: 15px;
}
.panel-heading {
  padding: 10px 15px;
  border-bottom: 1px solid transparent;
  border-top-left-radius: 3px;
  border-top-right-radius: 3px;
}
.panel-heading > .dropdown .dropdown-toggle {
  color: inherit;
}
```
“panel“主要对边框，间距和圆角做了一定的设置

## Bootstrap 支持的 JavaScript 插件

Bootstrap的JavaScript插件可以单独导入到页面中，也可以一次性导入到页面中。因为在Bootstrap中的JavaScript插件都是依赖于jQuery库，所以不论是单独导入还一次性导入之前必须先导入jQuery库。

### 一次性导入

Bootstrap提供了一个单一的文件，这个文件包含了Bootstrap的所有JavaScript插件，即bootstrap.js（压缩版本：bootstrap.min.js）

###  单独导入

1. 动画过渡（Transitions）:对应的插件文件“transition.js”
2. 模态弹窗（Modal）:对应的插件文件“modal.js”
3. 下拉菜单（Dropdown）：对应的插件文件“dropdown.js”
4. 滚动侦测（Scrollspy）：对应的插件文件“scrollspy.js”
5. 选项卡（Tab）：对应的插件文件“tab.js”
6. 提示框（Tooltips）：对应的插件文件“tooltop.js”
7. 弹出框（Popover）：对应的插件文件“popover.js”
8. 警告框（Alert）：对应的插件文件“alert.js”
9. 按钮（Buttons）：对应的插件文件“button.js”
10. 折叠/手风琴（Collapse）：对应的插件文件“collapse.js”
11. 图片轮播Carousel：对应的插件文件“carousel.js”
12. 自动定位浮标Affix：对应的插件文件“affix.js”

上述单独插件的下载可到github去下载（https://github.com/twbs/bootstrap）

## 自定义Bootstrap

在Bootstrap框架的官网为大家提供了一个在线自定义 Bootstrap 框架的配置页面 http://getbootstrap.com/customize/　，可以通过这里进行配置。

在线自定义设置主要包括三个部分：

1. Bootstrap 组件
2. Bootstrap 插件
3. Bootstrap 的 LESS 版本变量设置