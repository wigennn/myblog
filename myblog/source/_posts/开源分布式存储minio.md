---
title: 开源分布式存储minio
date: 2021-03-11 11:48:59
tags: 分布式存储
---

## Minio介绍
MinIO 是一个基于Apache License v2.0开源协议的对象存储服务。它兼容亚马逊S3云存储服务接口，非常适合于存储大容量非结构化的数据，例如图片、视频、日志文件、备份数据和容器/虚拟机镜像等，而一个对象文件可以是任意大小，从几kb到最大5T不等。

MinIO是一个非常轻量的服务,可以很简单的和其他应用的结合，类似 NodeJS, Redis 或者 MySQL。

<!--more-->

## 启动
```$xslt
    nohup ./minio server /root/minio/data > /root/minio/data/minio.log 2>&1 & 
```

#### 傻瓜式启动，而且感觉超级好用！