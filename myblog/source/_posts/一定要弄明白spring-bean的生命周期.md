---
title: 一定要弄明白spring bean的生命周期
date: 2020-06-03 20:28:51
tags: spring
---
### 一、Bean的完整生命周期
在传统的java应用中，bean的生命周期很简单，使用的时候new一下，使用完等待垃圾收集器回收。

<!--more-->

spring管理bean比较复杂，bean的构造过程如下:
![springbean生命周期](/imgs/springbean生命周期.jpg)

**bean的生命周期**
1.spring启动，加载需要被spring管理的bean，进行实例化

2.Bean的属性注入

3.如果bean实现BeanNameAware的接口，spring将beanid传递给setBeanName方法

4.如果bean实现了BeanFactoryAware接口，spring将调用setBeanFactory方法，将BeanFactory容器实例传入

5.如果bean实现了BeanContextAware接口，spring将调用bean的setApplicationContext方法，将bean的所在的上下文引用传入进来

6.如果bean实现BeanPostProcessor接口，spring将调用他们的postProcessBeforeInitialization方法

7.如果bean实现了initializingBean接口，spring将调用他们的afterpropertiesSet方法，如果bean使用init-method声明初始化方法，该方法也会被调用

8.如果bean实现BeanPostProcessor接口，spring将调用他们的postProcessAfterInitialization方法

9.bean使用

10.如果bean实现了DisposableBean接口，spring将调用destory方法，如果bean使用了destory-method方法，该方法也会被调用
