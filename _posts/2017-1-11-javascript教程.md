---
layout: post
titile: javascript教程
categories: 教程
tags: 前端
comments: true
---

学完HTML、CSS，就该学javascript了，JavaScript是一门 **解释型 编程语言**。不像HTML和CSS这种死的、静态的标记语言，JavaScript是一种编程语言，它的存在就是让网页动起来，给用户点反应。

来个实用点的例子：

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

## 语法

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

```
var x = 1, y=2;
```

声明变量加个var就行，变量类型不用管。

```
function myFunction(a,b)
{
if (a>b)
  {
  return;
  }
x=a+b
}
```

声明函数加个function就行，返回值类型都不用管。

>面向过程编程，你就要掌握如下概念：变量（variable）、函数(function)、变量的作用域（action scope）和生命期（lifetime）。

比如C/C++中的最大坑之一：

```
void swap(int a, int b){
  int temp = a;
  a = b;
  b = temp;
}
```

这段代码是无效的，因为函数会新建两个变量（作用域只在函数内，生命期：函数调用结束立马销毁），传入的a和b会分别赋值给这两个新建的变量，所以函数体内的交换实际上是在交换函数自己新建的这两个变量。该函数完全没有起到交换变量值的作用。正确的做法是用C++提供的引用，或者通过指针来交换变量。代码如下：

```
#include <iostream>
using namespace std;

//使用指针来交换：
void swap1(int *a, int *b){
  int temp = *a;//用指针取a的值
  *a = *b;
  *b = temp;
}

//使用引用（注意：引用是C++的，C语言没有）
void swap2(int &a, int &b){
  int temp = a;
  a = b;
  b = temp;
}

int main(){
  int a=1,b=2;
  int *aa = &a;
  int *bb = &b;
  swap1(aa, bb);
  cout << a << b << endl;
  swap2(a, b);
  cout << a << b << endl;
}
```

写这个东西是为了提醒你们注意变量的作用域和生命期。

据说一下是JavaScript最大的坑之一：

向未声明的 JavaScript 变量来分配值，如果您把值赋给尚未声明的变量，该变量将被自动作为全局变量声明。

```
carname="Volvo";
```

将声明一个全局变量 carname，即使它在函数内执行。

**数据类型**

JavaScript的数据类型有：
**字符串、数字、布尔、数组、对象、Null、Undefined**
JavaScript 中的所有事物都是对象，这点和python是一样的，像C/C++、Java这种是有基本数据类型的，比如Java中的int是基本数据类型，而Integer就是对象了。

>面向对象编程，你就要掌握如下概念：类(class)、对象（object）、实例(instance)、属性（property/attribute）、方法(method/function)、属性和方法的访问权限（default缺省的，private私有的，public公共的，protected受保护的）、继承（inheritance）、单继承还是多继承、多态(polymorphism)、构造函数（constructor）、析构函数(destructor)、抽象类(abstract class)、接口（interface）、抽象方法(abstract method)、虚函数(virtual function)、重载（overload）函数(function)或者运算符(operator)、重写(override)。这么多概念是不是眼花了，有种想死的感觉，没你想的那么难，很容易看懂，而且这些概念非常重要，好好记住了。

>电影里面张无忌学乾坤大挪移的时候只花了半个时辰，而乾坤大挪移的说明书上写着：从来没学过武功的小白需要20年的时间，有些基础的则需要1年半载，内功深厚的行家则只需半个时辰。我拿出这个例子只是想说，编程也是一样，如果你学过C语言，那么根本不用我讲运算符、比较、if..else、while、for、switch、break等等这些，因为每介绍一门语言就要讲这些，而程序员最讨厌的就是重复的工作，世界上的编程语言有200多种吧，常用的也就那么几种，语法上是有些差异，但我们人生来就是会抽象出共同点（这叫：归纳），然后对比出差异，并注意这些不同，然后举一反三（这叫：演绎），**归纳和演绎是人类最基本的思维技巧。** 多学点语言总没有坏处（但是要注意经常使用，不使用绝对掌握不了的），道理都是相通的。

try/catch/throw的例子：

```
<script>
function myFunction()
{
try
  {
  var x=document.getElementById("demo").value;
  if(x=="")    throw "empty";
  if(isNaN(x)) throw "not a number";
  if(x>10)     throw "too high";
  if(x<5)      throw "too low";
  }
catch(err)
  {
  var y=document.getElementById("mess");
  y.innerHTML="Error: " + err + ".";
  }
}
</script>

<h1>My First JavaScript</h1>
<p>Please input a number between 5 and 10:</p>
<input id="demo" type="text">
<button type="button" onclick="myFunction()">Test Input</button>
<p id="mess"></p>
```

JavaScript 表单验证 的例子：

验证必填项是否填了：

```
<html>
<head>
<script type="text/javascript">

function validate_required(field,alerttxt)
{
with (field)
  {
  if (value==null||value=="")
    {alert(alerttxt);return false}
  else {return true}
  }
}

function validate_form(thisform)
{
with (thisform)
  {
  if (validate_required(email,"Email must be filled out!")==false)
    {email.focus();return false}
  }
}
</script>
</head>

<body>
<form action="submitpage.htm" onsubmit="return validate_form(this)" method="post">
Email: <input type="text" name="email" size="30">
<input type="submit" value="Submit">
</form>
</body>

</html>
```

验证邮箱格式是否正确，验证的方法：输入的数据必须包含 `@` 符号和点号(`.`)。同时，`@` 不可以是邮件地址的首字符，并且 `@` 之后需有至少一个点号

```
<html>
<head>
<script type="text/javascript">
function validate_email(field,alerttxt)
{
with (field)
{
apos=value.indexOf("@")
dotpos=value.lastIndexOf(".")
if (apos<1||dotpos-apos<2)
  {alert(alerttxt);return false}
else {return true}
}
}

function validate_form(thisform)
{
with (thisform)
{
if (validate_email(email,"Not a valid e-mail address!")==false)
  {email.focus();return false}
}
}
</script>
</head>

<body>
<form action="submitpage.htm"onsubmit="return validate_form(this);" method="post">
Email: <input type="text" name="email" size="30">
<input type="submit" value="Submit">
</form>
</body>

</html>

```
