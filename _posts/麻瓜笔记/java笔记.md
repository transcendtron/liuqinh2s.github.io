---
layout: post
title: java笔记
categories: 麻瓜笔记
tags: [记录, 编程]
comments: true
---

>申明：这是我个人的学习笔记，从网上摘抄而来，并非原创。

JAVA三大框架Struts、Hibernate和Spring的各自作用是什么？

struts 主要负责表示层的显示，spring 利用它的IOC和AOP来处理控制业务（负责对数据库的操作），hibernate 主要作用是数据的持久化到数据库。

Spring是一个解决了许多在J2EE开发中常见的问题的强大框架。 Spring提供了管理业务对象的一致方法并且鼓励了注入对接口编程而不是对类编程的良好习惯。Spring的架构基础是基于使用JavaBean属性的Inversion of Control容器。然而，这仅仅是完整图景中的一部分：Spring在使用IoC容器作为构建完关注所有架构层的完整解决方案方面是独一无二的。

Struts是一个基于Sun J2EE平台的MVC框架，主要是采用Servlet和JSP技术来实现的。由于Struts能充分满足应用开发的需求，简单易用，敏捷迅速，在过去的一年中颇受关注。Struts把Servlet、JSP、自定义标签和信息资源(message resources)整合到一个统一的框架中，开发人员利用其进行开发时不用再自己编码实现全套MVC模式，极大的节省了时间，所以说Struts是一个非常不错的应用框架。

Hibernate是一个开放源代码的对象关系映射框架，它对JDBC进行了非常轻量级的对象封装，使得Java程序员可以随心所欲的使用对象编程思维来操纵数据库。 Hibernate可以应用在任何使用JDBC的场合，既可以在Java的客户端程序实用，也可以在Servlet/JSP的Web应用中使用，最具革命意义的是，Hibernate可以在应用EJB的J2EE架构中取代CMP，完成数据持久化的重任。

学习一种框架最先需要知道的是为什么需要使用这个框架，**任何一个框架的发明都是为了解决编程中的一些痛点**，打开任何一本hibernate或者其他框架的入门书，第一章都是介绍框架的理念和优势。如果需要理解这些理念和优势，那么 **你需要知道不使用这个框架之前是怎么处理的，才能知道框架做了一些什么事情**。

针对Spring的学习，第一步就是理解IoC和AOP；这是基础；然后学习SpringMVC,其实还是Java EE开发，如果要理解这个框架，就要知道没有这个框架之前，使用的是什么技术。
