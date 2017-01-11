---
layout: post
titile: javascript教程
categories: 教程
tags: 前端
comments: true
---

学完HTML、CSS，就该学javascript了，JavaScript是一门 **解释型 编程语言**。不像HTML和CSS这种死的、静态的标记语言，JavaScript是一种编程语言，它的存在就是让网页动起来，给用户点反应。

谈到编程语言，首先又得是关于基本语法的老生常谈。

**语句以分号结尾，当然也可以不加分号，在 JavaScript 中，用分号来结束语句是可选的。**

**注释和C语言一样，和CSS一样**

>通用的注释就那么几个吧，HTML用<!-- -->，C/C++、Java、CSS、JavaScript都是用`//`或者`/* */`，python和shell用`#`。

**JavaScript 对大小写敏感。**

例如：函数 getElementById 与 getElementbyID 是不同的。

**JavaScript 会忽略多余的空格**

例如：

```
var name="Hello";
var name = "Hello";
```

是一样的。

>有哪些语言不忽略空格呢，典型的：**shell**，shell编程赋值时不能加多于的空格，否则会报错。

**对代码行进行折行**

可以在文本字符串中使用反斜杠对代码行进行换行。下面的例子会正确地显示：

```
document.write("Hello \
World!");
```

不过，不能像这样折行：

```
document.write \
("Hello World!");
```

这种小细节没必要刻意去记，用起来的时候自然就会了，而且不会也没关系，谁说非得要用到折行了？

**JavaScript 拥有 动态类型**

var x = 1, y=2;

声明变量加个var就行，变量类型不用管。

**数据类型**

JavaScript的数据类型有：
**字符串、数字、布尔、数组、对象、Null、Undefined**
JavaScript 中的所有事物都是对象，这点和python是一样的，像C/C++、Java这种是有基本数据类型的，比如Java中的int是基本数据类型，而Integer就是对象了。

>面向对象编程，你就要掌握如下概念：类(class)、对象（object）、实例(instance)、属性（property/attribute）、方法(method/function)、属性和方法的访问权限（default缺省的，private私有的，public公共的，protected受保护的）、继承（inheritance）、单继承还是多继承、多态(polymorphism)、构造函数（constructor）、析构函数(destructor)、抽象类(abstract class)、接口（interface）、抽象方法(abstract method)、虚函数(virtual function)、重载（overload）函数(function)或者运算符(operator)、重写(override)。这么多概念是不是眼花了，有种想死的感觉，没你想的那么难，很容易看懂，而且这些概念非常重要，好好记住了。


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

>那些老旧的实例可能会在 `<script>` 标签中使用type="text/javascript"。现在已经不必这样做了。JavaScript 是所有现代浏览器以及 HTML5 中的默认脚本语言。可以说JavaScript是现在最流行的语言，去年（2016）github上最火的10个项目好像全是前端吧。微软支持通过 JavaScript 创建 Windows 8 app。
对于因特网和视窗操作系统，JavaScript 都意味着未来。

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
