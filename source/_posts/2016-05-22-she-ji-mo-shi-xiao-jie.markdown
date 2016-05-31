---
layout: post
title: 设计模式小结
date: 2016-05-22 15:14:10 +0800
comments: true
categories: 
 - 架构
tags: 
 - iOS设计模式

---

工厂方法模式、抽象工厂模式、生成器模式 小结，展现了几个创建型模式的异同和变化
![image](http://7xtaiq.com1.z0.glb.clouddn.com/image/pattern_change.png?imageMogr2/thumbnail/100000@)
<!-- more -->

## 类图变化
点击放大
![image](http://7xtaiq.com1.z0.glb.clouddn.com/image/pattern_change.png)
希望大家可以从这个图里面体会出创建型设计模式的思想。
在这里说几个关键点：  
1. 会变化的部分需要抽象  
&emsp;&emsp;![image](http://7xtaiq.com1.z0.glb.clouddn.com/image/20160622-pattern-abstract.png?imageMogr2/thumbnail/300)  
2. 复杂对象的创建和使用分离  
&emsp;&emsp;![image](http://7xtaiq.com1.z0.glb.clouddn.com/image/20160622-parrent-complexobject.png?imageMogr2/thumbnail/300)  
3. 同一系列的多个产品的创建，集中到一个类里面（可选）  
&emsp;&emsp;封装到一个类里面的方法有多种，可以多探索下，我就懒得一一列举了
&emsp;&emsp;![image](http://7xtaiq.com1.z0.glb.clouddn.com/image/20160622-pattern-factory-optional.png?imageMogr2/thumbnail/600)
