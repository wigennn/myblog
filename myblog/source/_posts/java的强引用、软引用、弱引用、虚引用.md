---
title: java的强引用、软引用、弱引用、虚引用
date: 2020-06-01 21:42:59
tags: java
---
### 一、前言
   jvm判断对象是否可回收有两种方式:
   * 引用计数法
   
    对于创建的对象都有一个引用计数的属性，引用每新增一次+1，引用释放一次-1。当为0的时候就可被GC.
    
   <!--more-->
   * 可达性分析
   
    对象被引用变量引用，当不被引用时，可被GC
 
 从jdk1.2开始，对象的引用被划分为4个等级，分别是**强引用**、**软引用**、**弱引用**、**虚引用**。    

### 二、四种引用
   #### 2.1 强引用（StrongReference）
    Object obj = new Object();
   当一个对象是强引用时，GC是不会回收的。
   
   当堆空间不够时，JVM垃圾收集器也不会回收强引用对象，而是抛出OOM终止程序。当obj为全局变量时，可在对象不用时提前设置obj=null
   #### 2.2 软引用（SoftReference）
   当内存空间不足时，垃圾收集器会回收软引用对象。继承SoftReference实现软引用。
   
   #### 2.3 弱引用（WeakReference）
   弱引用对象只要发生GC就会被回收。通过继承WeakReference实现。
   
    String str = new String("abc");
    WeakReference<String> wr = new WeakReference<>(str);
   
   #### 2.4 虚引用（PhantomReference）
   如果一个对象仅支持虚引用，相当于没有被引用。虚引用必须与引用队列(ReferenceQueue)联合使用。\
   当垃圾收集器准备回收一个对象时，如果发现它还有虚引用，就会在对象回收之前，把这个虚引用加入到与之关联的引用队列中。
   
    String str = new String("abc");
    ReferenceQueue queue = new ReferenceQueue();
    // 创建虚引用，必须与之关联一个引用队列
    PhantomReference pr = new PhantomReference(str, queue);
   
### 三、总结
   主要是软引用和弱引用的区别，软引用主要在内存空间不够时才会被回收，弱引用只要发生GC就会被回收。