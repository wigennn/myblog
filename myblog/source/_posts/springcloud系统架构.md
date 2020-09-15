---
title: springcloud系统架构
date: 2020-06-04 11:20:31
tags: spring cloud
---
### 一、一般的服务系统架构
在常见的系统架构中，一般包含网关，认证中心、前后台，中间件，注册中心，配置中心，监控服务等。

<!--more-->

![系统架构](/imgs/springcloud系统架构.PNG)

如上图所示, 一般包含以下组件服务:
- 1.网关
    springcloud实现网关服务的组件：gateway，zuul
- 2.认证授权中心
    一般使用oauth2.0 security组件
- 3.注册中心
    springcloud注册中心组件: nacos, consul, eureka
    
    传统的一般使用ZOOKEEPER作为注册中心
- 4.配置中心
    config, nacos, zookeeper, consul
- 5.前台
- 6.中台
    系统与系统之间通信一般是通过MQ或者rpc接口
    
    传统的rpc组件有：dubbo
    
    springcloud rpc组件：feign
    
    当然接口可能出现不可调用的情况，此时需要接口熔断服务，可使用hystrix
    
    有时候接口调用量非常大，需要限流，可使用网关限流
    
- 7.系统监控服务
    springbootadmin
- 8.调度中心
    xxl-job
- 9.缓存
    redis
- 10.消息
    rocketmq、kafka、rabbitmq、activemq等
- 11.数据库
    mysql