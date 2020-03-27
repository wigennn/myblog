---
title: 关于JVM垃圾回收
date: 2020-03-01 12:02:50
tags:
---
JVM的内存模型分为
线程共享:堆、方法区
线程私有:程序计数器、本地方法栈、虚拟机栈

两种异常:StackOverFlowException(请求栈深度大于JVM所允许的深度)和OutOfMemoryException

程序计数器: 记录指令执行地址
本地方法栈: native method
虚拟机栈: 栈帧(局部变量表、操作数栈、动态链接、方法出口)
堆: 存放对象和数组
方法区: 常量池，静态变量、类信息

堆分析：垃圾回收区
新生代(eden,survivorfrom,survivorto)、老年代

判断回收对象:
引用计数法  对象与之关联的引用，引用为0，对象可回收
可达性分析:GC Roots(虚拟机栈中本地变量表引用的对象、方法区中静态属性引用的对象、常量引用的对象、本地方法栈的JNI引用的对象)

回收算法:
复制算法:内存先一分为二，从一个复制到另一个
标记清除:会产生大量内存碎片
标记整理: 内存整理
分代收集:新生代、老年代

垃圾收集器:
Serial: 单线程收集、暂停其他工作线程、复制算法
ParNew: 多线程版本、暂停工作线程、复制算法
Parallel Scavenge: 并行、新生代、复制算法、可控制的吞吐量
Serial Old: 标记整理
Parallel Old: 多线程、标记整理、吞吐量
CMS: 最短回收停顿时间、(初始标记、并发标记、重新标记、并发清除)、CPU资源敏感、无法处理浮动垃圾，内存碎片,有参数设置内存碎片合并
G1: 并行并发、分代收集、标记整理、可预测停顿、(初始标记、并发标记、最终标记、筛选回收)

JVM命令:
jps：虚拟机进程 jps -l
jstat: 虚拟机统计信息监视工具 jstat -gc [pid] [ms] [count]
jinfo: java配置信息工具 jinfo [option] pid
jmap: java内存映像 jmap -dump:format=b,file=xxx pid (dump文件生成)   jmap -histo(对象统计信息)
jhat: 虚拟机存储快照分析 分析dump文件
jstack: 当前时刻的线程快照 jstack -l pid



