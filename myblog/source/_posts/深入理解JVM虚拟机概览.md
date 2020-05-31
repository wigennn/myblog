---
title: 深入理解JAVA虚拟机概览
date: 2020-05-26 15:28:46
tags: JVM
---

相信对于《深入理解JAVA虚拟机》第二版这本书大家并不陌生，对于JAVA从业者来说是必读的书，面试也常常考察该知识点。最近也出了《深入理解JAVA虚拟机》第三版,此版本基于JAVA8。

<!--more-->
### 一、概述
JVM (java virtual Machine) java虚拟机，jvm具有可移植性的平台特点，一份代码，到处可用，所以风靡到现在。以前由于机器的配置不一样，一份代码在这台机器上运行，但是放在别的机器上不能运行，导致开发成本大，所以JVM的横空出世不是没有道理，也是理所当然出现的。

此书大概讲三部分:
* JVM内存
* 类加载
* jvm性能调优

### 二、JVM概览
#### 2.1 JVM内存
* JVM内存
    * 程序计数器
        ``记录程序执行的地址``
    * 虚拟机栈
        ``栈帧 就是运行的局部方法相关``
    * 本地方法栈
        ``java native 方法``
    * 堆
        ``主要存放对象和数组``
    * 方法区
        ``主要存放类信息、常量池等``
      
    有两个ERROR, OutOfMemoryError(内存溢出)和StackOverFlowError(栈溢出 XSS)
    
* 对象回收
    * 判断回收算法 
        * 引用计数法
        * 可达性分析GC ROOT
    * 垃圾回收算法 
        * 复制算法
        * 标记清除
        * 标记整理
        
* 垃圾收集器
    * Serial
    * Serial Old
    * Parnew
    * parallel scanvage
    * CMS
    * G1
 
#### 2.2 类加载
   * 类加载过程
        * 加载
        * 验证
        * 准备
        * 解析
        * 初始化
        * 销毁
   * 类加载器
        * BootStrap Classloader 
        ``加载java的rt.jar``
        * Extension ClassLoader 
        ``加载extension包里的jar包``
        * Application Classloader 
        ``加载第三方jar包``
   * 双亲委派 
    ``先委托给父类加载器加载，父类加载器加载不到在委托给子类加载器加载``
#### 2.3 jvm性能调优
掌握几个重要的命令
* jps ``查看java进程``
* jmap ``可以导dump文件``
* jstat ``查看jvm gc状态``
* jinfo ``查看jvm信息``
* jstack ``查看线程状态``

### 三、总结
多实践，多观察，遇到问题多总结。对于概念有个基本掌握，实际上对于问题的排查在实际的工作中更为重要。