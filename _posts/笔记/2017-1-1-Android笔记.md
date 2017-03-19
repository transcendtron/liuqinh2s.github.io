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
- LinearLayout子组件的定义顺序决定着其在屏幕上显示的顺序。一般是从上到下，从左到右，如果设备语言为从右至左显示，如Arabic或者Hebrew，第一个定义的子组件则出现在屏幕的最右端。
- 使用`strings.xml`轻松实现本地化。
- `strings.xml`的根元素是`resource`
- 想知道activity_quiz.xml中的XML元素是如何转换为视图对象的吗？答案就在于Quiz_Activity类。
- extends Activity
- onCreate(Bundle savedInstanceState)
- setContentView(R.layout.activity_quiz);
- public void setContentView(int layoutResID)
- 通过传入资源ID参数，生成布局视图，布局视图生成后，布局文件包含的组件也随之以各自的属性定义完成实例化
- 布局是一种资源，资源是应用非代码形式的内容，比如图像文件、音频文件以及XML文件等
- 所有资源文件都在目录`res`的子目录下。
- `R.java`文件在Android项目编译过程中 **自动生成**，遵照该文件头部的警示，请不要尝试修改该文件的内容。
- Android为整个布局文件以及各个字符串生成资源ID，但activity_quiz.xml布局文件中的组件除外，因为不是所有的组件都需要资源ID。要为组件生成资源ID，请在定义组件的时为其添加上`android:id`属性。
- android:id="@+id/true_button"，android:text="@string/true_button"请注意`android:id`属性值前面有一个+标志，而`android:text`属性值没有，这是因为我们将要创建资源ID，而对字符串资源只是做了引用。
