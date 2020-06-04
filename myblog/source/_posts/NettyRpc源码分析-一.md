---
title: NettyRpc源码分析(一)
date: 2020-06-03 09:46:30
tags: 源码分析
---
### 一、概览
RPC, 即Remote Procedure Call(远程过程调用)，简单点说调用远程计算机服务，就像调用本地服务一样。

<!--more-->
Rpc协议可基于HTTP协议或TCP协议，WebService就是基于HTTP协议的RPC,但是性能却不如基于Tcp协议的RPC。 

有两个方面影响RPC的性能：1.传输方式 2.序列化方式

根据网络四层架构(物理层、网络层、传输层、应用层)，TCP属于传输层协议，http属于应用层协议，在数据传输方面越底层，传输越快。

java提供了默认的序列化方式，但是在高并发情况下，这种方式会带来性能瓶颈，所以还有一些优秀的序列化框架，如protobuf、kryo、hession、jackson、avro等。

为了支持高并发，不能采用传统的阻塞IO,需要采用异步的IO即NIO。一般有通信框架有mina、netty等。

需要将服务部署在分布式环境的不同节点上，通过服务注册的方式，让客户端自动发现当前可用的服务，并调用这些服务。这时候需要一种注册表的组件，注册分布式环境下所有的服务地址。(主机名与端口号)

应用、服务、服务注册表关系如下图:
![关系图](/imgs/rpc关系图.png)

### 二、NettyRpc总览
技术选型：
1.spring：bean管理
2.netty：nio
3.protobuf：序列化
4.zookeeper：注册中心

代码结构如下：
![代码结构](/imgs/NettyRpc_代码结构.png)

包含四个部分：
1.client
2.protocol
3.registry
4.server

### 三、总结
这个轻量级的rpc框架小巧但是五脏俱全，很值得学习。