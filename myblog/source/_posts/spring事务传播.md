---
title: spring事务传播
date: 2020-06-02 11:01:47
tags: spring
---
### 一、前言
spring在TransactionDefinition中规定了7种类型的事务传播行为，他规定了事务方法和事务方法发生嵌套调用时事务如何传播？
<!--more-->

### 二、Spring七种事务传播行为
* PROPAGATION_REQUIRED
    ``method2方法必须在事务中运行，如果当前method1存在事务，加入当前事务执行，不存在，则新建一个事务执行。``    
* PROPAGATION_SUPPORTS
    ``method2方法支持事务执行，但是如果存在method1事务，它可以在当前事务中执行``
* PROPAGATION_MANDATORY
    ``method2必须在事务中执行，如果当前method1不存在事务，抛出异常``
* PROPAGATION_REQUIRES_NEW
    ``method2方法必须运行在自己的事务中，如果method1存在事务则挂起，等到method2事务执行完毕再执行``
* PROPAGATION_NOT_SUPPORTED
    ``method2方法不应在事务中执行，如果method1事务正在执行，method2将被挂起，直到method1执行完毕``
* PROPAGATION_NEVER
    ``当前方法method2不应在事务中执行，如果存在一个事务，则抛出异常``
* PROPAGATION_NESTED
    ``表示如果当前方法正有一个事务在运行中，则该方法应该运行在一个嵌套事务中，被嵌套的事务可以独立于被封装的事务中进行提交或者回滚。如果封装事务存在，并且外层事务抛出异常回滚，那么内层事务必须回滚，反之，内层事务并不影响外层事务。如果封装事务不存在，则同PROPAGATION_REQUIRED的一样``

### 三、总结