---
layout: post
titile: javascript教程
categories: 教程
tags: 前端
comments: true
---

学完HTML、CSS，就该学javascript了，JavaScript是一门 **解释型 编程语言**。不像HTML和CSS这种死的、静态的标记语言，JavaScript是一种编程语言，它的存在就是让网页动起来，给用户点反应。

先来个例子：

```
<!DOCTYPE html>
<html>
<body>
<script>
function changeImage()
{
element=document.getElementById('myimage')
if (element.src.match("bulbon"))
  {
  element.src="http://www.w3school.com.cn/i/eg_bulboff.gif";
  }
else
  {
  element.src="http://www.w3school.com.cn/i/eg_bulbon.gif";
  }
}
</script>

<img id="myimage" onclick="changeImage()" src="http://www.w3school.com.cn/i/eg_bulboff.gif">

<p>点击灯泡来点亮或熄灭这盏灯</p>

</body>
</html>
```

<script>
function changeImage()
{
element=document.getElementById('myimage')
if (element.src.match("bulbon"))
  {
  element.src="http://www.w3school.com.cn/i/eg_bulboff.gif";
  }
else
  {
  element.src="http://www.w3school.com.cn/i/eg_bulbon.gif";
  }
}
</script>

<img id="myimage" onclick="changeImage()" src="http://www.w3school.com.cn/i/eg_bulboff.gif">

<p>点击灯泡来点亮或熄灭这盏灯</p>

很简单的一段代码，就是用了一个条件判断，把图片换了一下而已。

>那些老旧的实例可能会在 `<script>` 标签中使用type="text/javascript"。现在已经不必这样做了。JavaScript 是所有现代浏览器以及 HTML5 中的默认脚本语言。可以说JavaScript是现在最流行的语言，去年（2016）github上最火的10个项目好像全是前端吧。

你可以在 HTML 文档中放入不限数量的脚本。
脚本可位于 HTML 的 `<body>` 或 `<head>` 部分中，或者同时存在于两个部分中。
通常的做法是把函数放入 `<head>` 部分中，或者放在页面底部。这样就可以把它们安置到同一处位置，不会干扰页面的内容。当然最好是单独放到一个文件中：

```
<!DOCTYPE html>
<html>
<body>
<script src="myScript.js"></script>
//myScript.js就是那个单独的文件，把JavaScript代码放到这个文件中，然后使用的时候只需引用它即可。
</body>
</html>
```

内联的例子：

```
<button type="button" onclick="alert('Welcome!')">点击这里</button>
```

<button type="button" onclick="alert('Welcome!')">点击这里</button>

>举一反三，你有没有发现CSS和JavaScript都有三种放置方式，内联，内部，外部。我觉得这类发现都属常识，等你的这类发现多起来的时候，你的能力自然就提高了。
