---
layout: post
title: Python游戏开发之BombMan
categories: 实战
tags: 游戏
comments: true
---

## 环境安装

Python3、pygame

我用的是 **macbook**，下面讲讲 **mac OS** 的环境搭建：

先使用homebrew安装Python3.

![brew list](http://wx2.sinaimg.cn/mw690/006zFO3ggy1fbvru5hipoj30g403sjrw.jpg)

可以看到我已经安装好了Python3。

>关于homebrew的安装和使用教程网上很多，我这里就不写了，有疑问可以在评论里面提，我将一一解答

然后安装pygame:

`pip3 install pygame`

我在使用pygame的时候遇到了一点问题，我的代码如下：

```
# coding=utf-8

import pygame
from pygame.locals import *

pygame.init()
```

在Pycharm（python的IDE，Integrated Development Environmnet，集成开发环境）中`from pygame.locals import *`显示是灰色的（unused import statement，没有用到的导入语句），而且提示init()不存在。

>这时候你该想到可能是平台的问题了

上谷歌搜索：mac Python3 pygame，我找到这个页面：http://pygame.org/wiki/macintosh

安装上面的指示，我安装了XQuartz，重启macbook，解决了问题。

这时候依然有个问题：`cannot find reference 'load' in 'image.py'`。看到这个问题，我心态有点爆炸，暗骂道，什么鬼。
