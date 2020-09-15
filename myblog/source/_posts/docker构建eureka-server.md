---
title: docker构建eureka-server
date: 2020-06-24 16:13:15
tags: docker
---
### 一、目标
使用docker启动eureka-server.jar

<!--more-->

### 二、操作步骤
1.eureka-server.jar生成
![eureka-server.jar](/imgs/eureka-server-jar.png)

2.Dockerfile编写
![eureka-Dockerfile](/imgs/eureka-Dockerfile.png)

3.上传jar包和Dockerfile
    
    我是用的是idea上传文件, 配置如下
![configuration](/imgs/idea-deploy-config.png)

    本地上传目录, 文件上传目标路径,然后对需要上传的文件右击deployment-upload

![mappings](/imgs/idea-deploy-config-mappings.png)

    也可以使用idea ssh连接本地虚拟机, 上传Dockerfile和eureka中心的jar包
    
![ssh](/imgs/docker-ssh.png)

4.生成eureka-server.jar的镜像image
    
    在dockerfile目录使用命令 docker build -t eureka_v0.0.1 .  生成镜像 // 意思是 生成的镜像名是eureka_v0.0.1

![eureka-docker-image](/imgs/eureka-build-docker-image.png)
    
    查看docker镜像(docker images命令)，已经有了刚生成的eureka_v0.0.1的镜像

![docker-images](/imgs/docker-images.png)

5.启动eureka-server
    
    docker镜像启动命令 docker run -p 8761:8761 -d eureka_v0.0.1
    然后可以使用命令 docker ps 查看在运行的容器

![docker-run](/imgs/docker-ps.png) 

6.浏览器查看eureka-server是否运行
    
    浏览器查看192.168.99.100:8769, 
    192.168.99.100是docker的default虚拟机的ip地址， 
    8769是Eureka的启动端口，docker run的时候需要 -p 8769:8769映射到外网接口，否则访问不了
    
![eureka-server-browser](/imgs/eureka-server-browser.png)

### 三、总结
通过此次实操，了解docker基本命令，dockerfile的编写，docker image的生成，image的启动及外网的映射