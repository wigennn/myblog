---
title: netty学习总览
date: 2020-05-28 14:43:24
tags: netty
---
### 一、前言
netty框架作为一款优秀的高性能的NIO通信框架，包括网络通信、多线程编程、序列化、反序列化、异步和同步编程模型、SSL/TLS安全、内存池、HTTP、MQTT等协议栈。

<!--more-->
### 二、netty核心类库介绍
#### 2.1 JAVA NIO
* Channel
    `通道，负责读取写入，网络数据通过Channel读取和写入。与流不同的地方在于Channel是双向的，流只在一个方向上流动Inputstream和OutputStream。Channel是全双工的，同时支持读写操作。`
* Buffer
    `所有数据都是通过缓冲区处理的，读取数据时，直接读取到缓冲区中，写入数据时，写入到缓冲区中。任何时候访问NIO中的数据，都是通过缓冲区进行操作.`
* Selector
    `Selector不断轮询注册在其上的Channel，如果某个Channel有新的TCP连接接入，读写事件，channel就处于就绪状态，会被Selector轮询出来，通过SelectionKey获取就绪Channel的集合，进行后续IO操作。`

#### 2.2 Netty核心类库
* ByteBuf
* Channel Unsafe
* ChannelPipeLine ChannelHandler
* EventLoop
    `主要负责IO读写, 普通TASK:调用NioEventLoop的execute()实现; 定时任务: 调用NIOEventLoop的schedule方法实现`
* Future Promise
    `异步操作结果`

### 三、总结
重点掌握Netty服务端和客户端的创建，创建过程中使用到的核心类库和api，以及消息的发送、接收、消息的编解码。
