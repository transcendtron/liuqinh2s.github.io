---
layout: post
titile: javascript教程
categories: 教程
tags: 前端
comments: true
---

学完HTML、CSS，就该学javascript了，JavaScript是一门 **解释型 编程语言**。

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
  element.src="/i/eg_bulboff.gif";
  }
else
  {
  element.src="/i/eg_bulbon.gif";
  }
}
</script>

<img id="myimage" onclick="changeImage()" src="/i/eg_bulboff.gif">

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
