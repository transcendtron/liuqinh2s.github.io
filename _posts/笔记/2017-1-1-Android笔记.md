---
layout: post
title: Android笔记
categories: 笔记
tags: [编程, Android]
comments: true
---

- activity，活动
- layout，布局
- DNS(Domain Name System 或 Domain Name Service，域名系统或域名服务)反转约定，遵循这个约定可以保证包名的唯一性，比如：com.liuqinh2s.firstandroid。
- wiget，组件
- 开发工具无法校验布局XML，请避免输入或拼写错误。
- 根据所使用的工具版本不同，以android:text开头的代码可能会产生错误信息。
- gravity
- padding（除了内容本身外，还需要增加额外指定量的空间）
- 根元素LinearLayout必须指定Android XML资源文件的命名空间属性为http://schemas.android.com/apk/res/android。
- LinearLayout组件继承自View子类的ViewGroup组件（ViewGroup组件还包括：FrameLayout、TableLayout、RelativeLayout）。
- 以前还有一个`fill_parent`属性值，等同于`match_parent`，目前已经废弃不用。
- LinearLayout虽然是根元素，但它也有父视图（View）--Android提供该父视图来容纳应用的整个视图层级结构。
- 24dp，dp即：density-independent pixel，指与密度无关像素。
