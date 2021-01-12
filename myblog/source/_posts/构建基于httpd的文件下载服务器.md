---
title: 构建基于httpd的文件下载服务器
date: 2020-10-09 17:16:40
tags: linux
---

# httpd
> httpd为Apache HTTP服务器程序，简单的改造就可以作为一般企业的文件下载服务器.
<!--more-->
## 启动httpd
> service httpd start

## 修改启动端口
> 配置文件所在目录 /etc/httpd/conf/httpd.conf

> 修改指定端口: Listen ****

> 创建文件目录: /var/www/html/  只需要在此文件目录下创建文件夹即可，然后通过sftp的方法把文件上传到创建的目录中

以下为展示效果
![httpd](/imgs/httpd.png)