---
title: DockFile详解
date: 2020-06-24 11:04:29
tags: Docker
---

### 一、什么是Dockfile
相当于生成docker镜像的配置文件, 使用docker build执行命令生成docker镜像。

<!--more-->

### 二、Dockerfile有哪些命令
####2.1 dockerfile的组成部分:

基础镜像信息: FROM

维护者信息: MAINTAINER

镜像操作指令: RUN、COPY、ADD、EXPOSE、WORKDIR、ONBUILD、USER、VOLUME等

容器启动时执行指令: CMD, ENTRYPOINT

#### 2.2 命令详解
- FROM ``构建的镜像设置基础镜像`` 

    ```
    FROM <image> [AS name]
    FROM <image> [:<tag>] [AS name]
    FROM <image> [@digest] [AS name]
    ```
    
- RUN ``在镜像的构建中执行特定的指令``

    ```
    RUN <command> (shell格式)
    ```
   
- EXPOSE ``为构建的镜像设置监听端口``

    ```
    EXPOSE <port> [<protocol></protocol>]
    ```

- ENV ``在构建的镜像中设置环境变量``

    ```
    1. ENV key val1 val2
    2. ENV key=val key2=val2
    ```
    
- COPY ``复制文件``
    
    ```
    COPY <源文件> <复制路径>
    例: COPY test.cong /usr/local/
    ```
    
- ADD ``构建镜像时，复制上下文中的文件到镜像内``
    
    ```
    ADD <源文件> <复制路径>
    ```
- VOLUME ``定义匿名卷，用于挂载点``

    ```
    VOLUME ["/data"]
    ```
- WORKDIR ``指定工作目录``

    ```
    WORKDIR /path/
    设置工作目录后，dockerfile后面命令都会在该目录下执行
    ```
- CMD ``指定容器启动时所执行的命令``

- ENTRYPOINT ``用于给容器配置一个可执行的程序``

### 三、Dockerfile实例:
安装一个nginx, 并在80端口启动

    ```
    FROM ubuntu:16.04
    MAINTAINER wigen
    RUN apt-get update
    RUN apt-get install -y nginx
    RUN echo 'Hello World, 我是个容器' \ 
       > /var/www/html/index.html
    ENTRYPOINT ["/usr/sbin/nginx"]
    EXPOSE 80
    ```
