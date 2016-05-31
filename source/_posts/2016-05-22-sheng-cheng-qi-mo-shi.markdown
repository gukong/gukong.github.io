---
layout: post
title: 生成器模式
date: 2016-05-22 10:54:31 +0800
comments: true
categories: 
 - 架构
tags: 
 - iOS设计模式

---

复杂对象包含许多子部件，其提供一系列创建子部件的接口。  
构建者持有复杂对象，可以创建某种风格的子部件。  
主管被赋予构建者的管理权限，进而指导构建者构建复杂对象。
<!-- more -->

## 定义
将一个复杂对象的构建与它的表现分离，使得同样的构建过程可以创建不同的表现。

## 解析
需要创建的对象很复杂，需要许多的步骤来创建，生成器模式最主要的就是把创建过程封装到一个抽象类，继承该抽象类的子类都有了创建复杂对象的流程。

## 类图

<!--<div align=center>-->
![image](http://7xtaiq.com1.z0.glb.clouddn.com/image/generate-pattern.png?imageMogr2/thumbnail/300000@)
<!--</div>-->
类图详解  
&emsp;&emsp;制造枪械需要许多零部件，【聚能枪制造车间】专门制造枪械零部件，子类通过继承【聚能枪制造车间】来获得制造枪械的关键步骤，进而可以创建个性化的枪械。整个制造流程是在【机械制造技师】的控制下的。

## 示例代码

````objectivec

//Complex Product
@interface ComplexProduct : NSObject

@property (nonatomic, strong) Part1 *part1;
@property (nonatomic, strong) Part2 *part2;
@property (nonatomic, strong) Part3 *part3;

@end

//Abstract Builder
@interface AbstractBuilder : NSObject

@property (nonatomic, strong) ComplexProduct *product;

- (void)createNewProduct;// _product = [[ComplexProduct alloc] init]
- (void)buildPart1;//empty implementation
- (void)buildPart2;//empty implementation
- (void)buildPart3;//empty implementation

@end

//ConcreteBuilder
@interface Builder1 : AbstractBuilder

- (void)buildPart1;//self.product.part1 = /*something*/
- (void)buildPart2;//self.product.part2 = /*something*/
- (void)buildPart3;//self.product.part3 = /*something*/

@end

//ConcreteBuilder
@interface Builder2 : AbstractBuilder

- (void)buildPart1;//self.product.part1 = /*something else*/
- (void)buildPart2;//self.product.part2 = /*something else*/
- (void)buildPart3;//self.product.part3 = /*something else*/

@end

//Director
@interface Director : NSObject

@property (nonatomic, strong) AbstractBuilder *builder;

- (ComplexProduct *)getProduct;// builder.product

/**
 *	do something like this
 *	[builder createNewProduct];
 *	[builder buildPart1];
 *	[builder buildPart2];
 *	[builder buildPart3];
 */
- (void)startBuildProduct;

@end


//BuilderExample

- (void)builderExample {

	Builder1 *builder1 = [[Builder1 alloc] init];//choose one builder
	
	Director *director = [[Director alloc] init];
	director.builder = builder1;
	[director StartBuilderProduct];
	
	ComplexProduct *product = [director getProduct];
	/*
	 * do something with product
	 */
}

````

----

这个模式关键就是分离构建对象的步骤。一个抽象工厂提供构建对象的流程，子工厂在流程当中构建具体的部件。另外需要一个主管来操作子工厂构建复杂对象。
