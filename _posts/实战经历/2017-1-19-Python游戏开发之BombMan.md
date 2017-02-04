---
layout: post
title: Python游戏开发之BombMan
categories: 实战经历
tags: [游戏, Python, 编程]
comments: true
---

## 环境安装

Python3、pygame

我用的是 **macbook**，下面讲讲 **mac OS** 的环境搭建：

先使用homebrew安装Python3.

![brew list](https://wx2.sinaimg.cn/mw690/006zFO3ggy1fbvru5hipoj30g403sjrw.jpg)

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

我按照这：https://gist.github.com/ExPHAT/0cfc67ceb8982d11fd27
上面装了那些软件，依旧没有卵用，而且这个问题实在蹊跷。

最后终于揭晓了问题原因，IDE没找到load函数而已，程序依旧可以运行正确。

代码如下：

```
#coding=utf-8

# 1 - Import library
import pygame
from pygame.locals import *

# 2 - Initialize the game
pygame.init()
width, height = 640, 480
screen = pygame.display.set_mode((width, height))

# 3 - Load images
player = pygame.image.load(u"./宝宝加油.png")

# 4 - keep looping through
while 1:
    # 5 - clear the screen before drawing it again
    screen.fill(0)
    # 6 - draw the screen elements
    screen.blit(player, (100, 100))
    # 7 - update the screen
    pygame.display.flip()
    # 8 - loop through the events
    for event in pygame.event.get():
        # check if the event is the X button
        if event.type == pygame.QUIT:
            # if it is quit the game
            pygame.quit()
            exit(0)
```

代码运行效果：

![代码运行效果](https://wx4.sinaimg.cn/mw690/006zFO3ggy1fbwtk3wpqej30zq0rw1kx.jpg)

## 架构

搞定了环境，就开始分析游戏架构。

首先必不可少的目录：

- src（source的缩写，存放代码）
- res（resource的缩写，存放资源，如：音乐、图片）
- data（存放游戏数据，如：地图、人物属性、游戏进度等等）
- lib（library，存放第三库）。

这个炸弹人游戏是仿泡泡堂制作的，大家应该都玩过。
