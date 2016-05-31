---
layout: post
title: 抽象工厂模式
date: 2016-05-13 21:36:55 +0800
comments: true
categories: 
 - 架构
tags: 
 - iOS设计模式

---

抽象工厂模式 -- 不是很好理解，我更愿意叫它总工厂模式  
一句话阐述 -- 一个子工厂对应一个产品，总工厂知道所有的子工厂，想要一个特定的产品，找总工厂总是没错的。  
![image](http://7xtaiq.com1.z0.glb.clouddn.com/image/zonggongchang.png)
<!-- more -->

## 定义
提供一个创建一系列相关或相互依赖对象的接口，而无需指定他们具体的类。

## 解析
前面已经提到了【总工厂模式】的叫法更易理解，为什么呢？【抽象工厂方法】描述的是这样一个场景：我需要【狙击枪】【霰弹枪】【手枪】，他们有很多共同点，也有许多不同点，如果都由同一个类来生产这些枪械，那么这个类肯定会比较复杂。所以要提炼出共同点，再把不同点分散到【子工厂】去实现。我们不知道最终是谁生产的枪械，只需要到【总工厂】提枪就行了。

## 类图
<div align=center>
![image](http://7xtaiq.com1.z0.glb.clouddn.com/image/AbstractFactoryPattern.png)
</div>
类图讲解：  
&emsp;&emsp;从上一个【工厂方法模式】可以知道，【聚能枪】可以发射各种聚能弹，但是在【工厂方法模式】里面，【聚能枪】之所以能发射不同聚能弹的原因是可以更换拥有相同接口的【聚能弹生成器】。  
&emsp;&emsp;这个【抽象工厂模式】要说明的是，不同的聚能枪可以强化聚能弹不同属性进而达到更理想的击打效果。比如【高压远程聚能枪】配合【α远程聚能弹】可以击打更远的目标哦。  
&emsp;&emsp;那么问题来了，怎样得到不同的聚能枪呢？答案就是【总工厂】。
<div align=center>
![image](http://7xtaiq.com1.z0.glb.clouddn.com/image/zonggongchang.png)
</div>

----
这个模式关键的就是【总工厂】，它提供了一个 **工厂对象** 以及 **所有产品的名单**  

1. 所有【子工厂】都提供【总工厂】列出的所有产品，也就是你获得了一个什么样的【子工厂】，也就获得了什么样的【产品】。所以你需要明确的告诉【总工厂】你想要的【子工厂】类型。
2. 你可以模糊【子工厂】的概念，甚至使用工厂的人不需要知道【子工厂】的存在。【总工厂】可以提供一个接口：传入产品类型，返回相应的【子工厂】（**子工厂**会被当做**总工厂**使用）。

## 示例代码

````objectivec

@interface SizeProduct : NSObject
@end

@interface SizeProduct1 : SizeProduct
@end

@interface SizeProduct2 : SizeProduct
@end

@interface ColorProduct : NSObject
@end

@interface ColorProduct1 : ColorProduct
@end

@interface ColorProduct2 : ColorProduct
@end


@interface SimpleFactory : NSObject
- (SizeProduct *)getSizeProduct;// return [[SizeProduct alloc] init]
- (ColorProduct *)getColorProduct:// return [[ColorProduct alloc] init]
@end

@interface Factory1 : SimpleFactory
- (SizeProduct *)getSizeProduct;// return [[SizeProduct1 alloc] init]
- (ColorProduct *)getColorProduct:// return [[ColorProduct1 alloc] init]
@end

@interface Factory2 : SimpleFactory
- (SizeProduct *)getSizeProduct;// return [[SizeProduct2 alloc] init]
- (ColorProduct *)getColorProduct:// return [[ColorProduct2 alloc] init]
@end

````



