---
title: SpringBootAdmin介绍
date: 2020-06-04 10:49:23
tags: spring cloud
---

### 一、springboot admin简介
Spring Boot Admin是一个开源社区项目，用于管理和监控SpringBoot应用程序。 应用程序作为Spring Boot Admin Client向为Spring Boot Admin Server注册（通过HTTP）或使用SpringCloud注册中心（例如Eureka，Consul）发现。

<!--more-->

### 二、为什么使用springboot admin
sprinboot admin 监控，解决集群各节点监控问题。
非侵入式的，只需将springbootadmin server注册到注册中心上，各个节点暴露actuator状态，就可实现全集群节点监控。
springboot admin主要功能：
- 1.健康状态
- 2.上下线情况
- 3.内存
- 4.GC
- 5.环境变量
- 6.日志级别
- 7.线程存储
- 8.堆快照
- 9.JMX
- 10.监控指标
- 11.endpoint
- 12.系统参数
- 13.CPU
- 14.硬盘
......

最主要是可视化, 如下图：
![springbootadmin](/imgs/springbootadmin.PNG)

### 三、springboot admin部署架构
3.1结合注册中心
- server端
    注册到注册中心上如eureka
- client端
    各节点暴露监控状态，即配置文件中添加如下配置:
    ``management.endpoints.web.exposure.include=*
      management.endpoint.health.show-details=always``
    如果没有集成client，是不支持JMX的

3.2 客户端服务端模式
    客户端配置服务端地址，支持JMX

### 四、springboot admin监控原理
**actuator**

    - env
    - info
    - health
    - dump
    ......
    
JMX
    