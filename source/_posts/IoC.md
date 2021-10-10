---
title: IoC
date: 2020-11-07 12:06:11
categories: 
- [技术]
- [笔记]
tags:
- IoC
---
原文：[Inversion of control - Wikipedia](https://en.wikipedia.org/wiki/Inversion_of_control)
以下为为摘录翻译。
## 简介
在软件工程领域，控制反转`Inversion of control (IoC)`是一种编程原理。
传统的过程式编程`Procedural programming`，实现业务逻辑的代码自己去调用框架去处理通用逻辑。
控制反转则把控制流反了过来，由框架自己去调用相应的业务逻辑。

> Inversion of control is sometimes facetiously referred to as the “Hollywood Principle: Don’t call us, we’ll call you”.

## 内涵
控制反转的情况下，即使可重用代码和特定于问题的代码在应用程序中一起运行，两部分代码往往也是独立开发的。软件框架，回调，调度程序，事件循环，依赖项注入和模板方法都可视为控制反转的例子。

*译者：这样的话，iOS的delegate设计模式其实也体现了控制反转的思想。*

## 目的
* 任务执行与实现的解耦
* 让模块专注于它的设计任务
* 让模块不再需要假设别的系统如何调用自己，取而代之依赖于合约`contract`
* 防止替换模块时的副作用


## 实现技术
在面向对象编程中，有几种技术可以实现控制反转。分别是：
* 服务定位器模式 [service locator pattern](https://en.wikipedia.org/wiki/Service_locator_pattern) 
* 使用依赖注入
* 上下文查询 (contextualized lookup)
* 模板方法设计模式 ( [template method design pattern](https://en.wikipedia.org/wiki/Template_method_design_pattern) )
* 策略设计模式 ( [strategy design pattern](https://en.wikipedia.org/wiki/Strategy_design_pattern) )

**依赖注入**是大家比较熟悉的方式，常见的几种注入又可分为：
* 构造器(Constructor)注入
* 参数注入
* setter注入
* 接口注入