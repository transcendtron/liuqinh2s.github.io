---
layout: post
title: 从C++到Python
categories: 趟坑笔记
tags: [Python, 教程, 编程语言]
comments: true
---

## python 特性

### 写在前面：

**编程是非常注重实战的，一定要在实战中慢慢体会，这样效率才高，
单看语法教程不仅看不进去，而且一点卵用都没有。**

>我是从C/C++转过来学python的，所以我会拿C/C++来和python进行对比。

### 1. 不需要申明变量类型，比如：

```
#!/usr/bin/python
# -*- coding: UTF-8 -*-

counter = 100 # 赋值整型变量
miles = 1000.0 # 浮点型
name = "John" # 字符串

print counter
print miles
print name
# 这个print语法是python2的，python3的print要用函数形式：print()
```

### 2. 同时给多个变量赋值，比如：

```
a = b = c = 1
# 以上实例，创建一个整型对象，值为1，三个变量被分配到相同的内存空间上。
a, b, c = 1, 2, "john"
```

### 3. 基本数据类型有：

- Numbers（数字）
- String（字符串）
- List（列表）
- tuple（元组）
- Dictionary（字典），相当于其他语言中的hashmap，存储键值对（key, value）

Numbers包括：

- int（整形）
- long（长整形）
- float（浮点型）
- complex（复数）

### 高级数据结构

List  特别好用的高级动态数组
tuple 不能更改的List
dict  其实就是其他语言中的hashmap
set   不重复集合，也可以看成没有value，只有key的dict

### 高级操作

切片(slice) 可以灵活的取list、str，可以倒数地取数
迭代(Iterate) 这个很多语言都有
列表生成式 在中括号框里面码代码[x*x for x in range(1,10)]，其实也没啥卵用
生成器(generator)，也叫惰性求值，其实保存函数，在需要的时候再实时的计算，比如生成斐波那契数列、杨辉三角，还是很有用的。

### 高阶函数

高阶函数的定义是：参数或返回值里面有函数。
map/reduce函数，map就是把一个迭代对象里的每一个元素，都调用一个函数计算，相当于数学里的函数映射，reduce则是一种fold运算，累次计算，可以用来累加、累乘。
filter，删选函数，对象也是迭代对象。
sorted，排序
匿名函数，lambda式就是一个匿名函数，这个概念在很多语言里面都有。
装饰器，decorate，用来打印日志的，图个方便而已，其实也没啥卵用。
偏函数，partial function，用来处理默认参数的，图个方便而已，其实也没啥卵用。

### 四种参数

位置参数，就是必选参数
默认参数，可以写上参数=什么
可变参数，参数是一个多元素的对象，比如tuple，使用*args来调用
关键字参数，参数对象是一个map，用**kw，来调用，一般处理注册信息的时候，非必填信息可以用这个来装。

## 一些细小的变化

- 使用 **空格缩进** 来完成语句划分，不使用分号和花括号。
- 与不是 && ，而是 and ，或不是 || ，而是 or ，非不是 ！ 而是 not
- if、while、for 都不使用圆括号，另外还需加冒号(:)
- 函数可以返回多个返回值，并统一使用`def`来定义函数，函数内可再定义函数
- 类的成员函数和成员变量统统要加`self.`，没有访问权限控制（public,private,protect等等），全靠自觉

### python2到python3的转换

Python虽然好用，但Python2到Python3的跨越确实把很多新手恶心到了，但作为一个程序员，我们的能力应该是可以强到解决这种小问题的。[python2和python3的区别](https://gist.github.com/scturtle/3060332)

## python 趣谈

[python 发展史](https://www.15yan.com/story/1JKTBQvVk5e/)

摘要：
1. python语言结合了ABC语言和C语言
2. Python从一开始就特别在意可拓展性。Python可以在多个层次上拓展。从高层上，你可以直接引入.py文件。在底层，你可以引用C语言的库。Python程序员可以快速的使用Python写.py文件作为拓展模块。但当性能是考虑的重要因素时，Python程序员可以深入底层，写C程序，编译为.so文件引入到Python中使用。**俗称：胶水语言**
