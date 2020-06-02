---
title: spring cloud gateway
date: 2019-06-02 10:13:49
tags: spring cloud
---
### 一、Gateway简介
Spring Cloud GateWay是Spring Cloud推出的第二代网关框架，取代Zuul网关。网关作为流量入口，在微服务中起着重要作用。网关常见的功能有请求转发，权限校验，熔断，限流等。

<!--more-->

### 二、Gateway功能
* 请求转发
* 熔断
可以集成Hystrix组件实现
* 限流
限流主要有两种算法:漏桶算法和令牌桶算法。

漏桶算法是请求直接进入漏桶中，漏桶以一定的速率释放连接去请求响应，当请求访问频率超过接口响应速率，拒绝访问。
令牌桶算法是预先设置一个令牌桶，以一定的速率往令牌桶中添加令牌，请求只有先获取令牌才能继续执行，获取不到则丢弃请求。
* 认证授权

### 三、总结