---
title: MVC与MVVM、Rx
date: 2020-11-04 14:20:06
categories: 
- 技术
- 笔记
tags:
- MVVM
- Rx
- Swift
---
MVC、MVVM都是大家熟悉的常用架构。

## MVVM
关于MVC不展开，下面讲讲MVVM。[App 架构](https://objccn.io/products/app-architecture)一书提到：

MVVM 所做的不仅仅是把代码移动到新的地方。加入一层新的 `view-model` 层的目的是双重的： 
* 鼓励将 `model` 和 `view` 之间的关系构建为一系列的变形管道。
* 提供一套独立于 app 框架的接口，但是它在相当程度上代表了 view 应该展示的状态。

两者结合起来，对 MVC 中两个最大的被人诟病的地方进行了修正。第一项通过把 model 相关 的观察和变形从 controller 层移除出去，减少了 controller 所需要承担的责任。第二项为场景 的 `view state` 提供了一套干净的接口，让它可以独立于 app 框架进行测试，而不需要使用MVC 的集成测试。 
 
但MVVM也有自己的一些要求，[App 架构](https://objccn.io/products/app-architecture)一书提到：
为了保持 `view` 与 `view-model` 的同步，MVVM 强制使用某种形式的绑定，也就是说，需要一种保证一个对象上的属性与另一个对象上的属性同步的方式。`Controller`负责构建这些绑定，将 `view-model` 所暴露的属性和场景中 `view-model` 所代表的 `view` 上的属性关联起来。

## 双向绑定
典型的绑定是利用响应式框架`RxSwift`来实现的（不是一定）。但通过学习`RxSwift`提供的Demo，发现`RxSwift`本身的知识点（如各种操作符的组合）以及响应式编程的思想的灵活运用还是有陡峭的学习曲线的。
 
响应式编程解决的重要的一个问题，是State的同步问题。就目前来看，该问题在我们开发的应用中并没有十分突出。而我们基于非声明式UI利用响应式编程又会导致绑定等的胶水代码过多。
## 结论
综上，利用MVC开始应用开发，在适当的时候引入适当的响应式编程可能才是最佳选择。