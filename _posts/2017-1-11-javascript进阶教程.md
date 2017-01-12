---
layout: post
title: javascript进阶教程
categories: 教程
tags: 前端
comments: true
---

学完了javascript基本语法，就可以看这篇博客了。

## JavaScript HTML DOM

通过 HTML DOM，可访问 HTML 文档的所有元素。

HTML DOM （文档对象模型）
当网页被加载时，浏览器会创建页面的文档对象模型（Document Object Model）。
HTML DOM 模型被构造为对象的树。

HTML DOM 树：

![HTML DOM 树](http://ww1.sinaimg.cn/mw690/006zFO3ggw1fbmlkdxp4pg30di07e3yb.gif)

### 查找HTML元素

- 通过 id 找到 HTML 元素
- 通过标签名找到 HTML 元素
- 通过类名找到 HTML 元素

```
var x=document.getElementById("main");
var y=x.getElementsByTagName("p");
```

### 改变HTML内容

在 JavaScript 中，document.write() 可用于直接向 HTML 输出流写内容。

```
<!DOCTYPE html>
<html>
<body>

<script>
document.write(Date());
</script>

</body>
</html>
```

绝不要使用在文档加载之后使用 document.write()。这会覆盖该文档。
修改 HTML 内容的最简单的方法时使用 innerHTML 属性。

```
<html>
<body>

<p id="p1">Hello World!</p>

<script>
document.getElementById("p1").innerHTML="New text!";
</script>

</body>
</html>
```

```
<!DOCTYPE html>
<html>
<body>

<img id="image" src="smiley.gif">

<script>
document.getElementById("image").src="landscape.jpg";
</script>

</body>
</html>
```

### 改变 CSS

```
<h1 id="id1">My Heading 1</h1>

<button type="button" onclick="document.getElementById('id1').style.color='red'">
点击这里
</button>
```

<h1 id="id1">My Heading 1</h1>

<button type="button" onclick="document.getElementById('id1').style.color='red'">
点击这里
</button>

### DOM 事件

```
<button onclick="displayDate()">点击这里</button>
```

<button onclick="displayDate()">点击这里</button>

[w3school 上的其他DOM事件例子](http://www.w3school.com.cn/js/js_htmldom_events.asp)

## JavaScript库（框架）

- jQuery
- Prototype
- MooTools

所有这些框架都提供针对常见 JavaScript 任务的函数，包括动画、DOM 操作以及 Ajax 处理。

### CDN - 内容分发网络

您总是希望网页可以尽可能地快。您希望 **页面的容量尽可能地小**，同时您希望 **浏览器尽可能多地进行缓存**。
如果许多不同的网站使用相同的 JavaScript 框架，那么 **把框架库存放在一个通用的位置供每个网页分享** 就变得很有意义了。
CDN (Content Delivery Network) 解决了这个问题。CDN 是包含可分享代码库的服务器网络。
Google 为一系列 JavaScript 库提供了免费的 CDN，包括：
- jQuery
- Prototype
- MooTools
- Dojo
- Yahoo! YUI
如需在您的网页中使用 JavaScript 框架库，只需在 <script> 标签中引用该库即可：

引用 jQuery

```
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.8.3/jquery.min.js">
</script>
```
