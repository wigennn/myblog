---
title: flink-windows下源码编译、启动、调试
date: 2020-09-19 09:47:36
tags: FLINK
---

## 前言
> 想要快速上手了解一个项目, 就需要先把项目跑起来 : p)

flink最新分支版本是release-1.11, 但是此版本还未支持windows启动脚本(原因可能是大佬都用mbp), 
所以本次使用支持windows启动的flink release-1.8的分支版本。
<!--more-->

## 环境准备
- JDK: 1.8+ 
> ps:1.7版本的jdk启动不了flink, 自行cmd, java -version检查本机jdk版本，不是就自行百度配置环境变量。
- ide: IDEA
> 宇宙最好用的java ide. : )
- flink源码拉取: clone到本地，并切换分支release-1.8, 拉取最新代码
> flink源码去github上拉取, 地址 https://github.com/apache/flink.git 

![flink-code](/imgs/flink/flink项目.png)

## 源码编译
- 使用命令```mvn clean install -DskipTests -Dfast```build项目, 需配置maven的环境变量方便全局使用

- 或者使用idea的maven编译按钮编译项目, 1.11的编译会有报错, 根据提示解决报错, 1.8版本的build时间过长, 大概需要10+分钟。

![flink编译构建](/imgs/flink/flink编译构建.png)

- 构建完成后会有```buid success```字样出现在console里。

## 配置修改启动
- 编译完成后找到flink-dist模块，启动配置都在这里。

![flink-dist](/imgs/flink/flink-dist.png)

- 在bin同级目录下创建log目录和lib目录, 不然启动会报错
- 需要把resource目录中的flink.yaml文件拷贝到conf目录中, 不然启动会启动失败
- 把target里的flink-dist jar包放到lib目录里，还有两个log的相关的jar包
- 修改start-cluster.bat文件，在最后添加远程调试参数，并修改启动参数

```$xslt
SET JVM_REMOTE_JOBMANAGER=-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005
SET JVM_REMOTE_TASKMANAGER=-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5006

start java %JVM_ARGS% %JVM_REMOTE_JOBMANAGER% %log_setting_jm% -cp "%FLINK_CLASSPATH%"; org.apache.flink.runtime.entrypoint.StandaloneSessionClusterEntrypoint --configDir "%FLINK_CONF_DIR%" > "%out_jm%" 2>&1
start java %JVM_ARGS% %JVM_REMOTE_TASKMANAGER% %log_setting_tm% -cp "%FLINK_CLASSPATH%"; org.apache.flink.runtime.taskexecutor.TaskManagerRunner --configDir "%FLINK_CONF_DIR%" > "%out_tm%" 2>&1

```
- 执行start-cluster.bat脚本

![flink-启动](/imgs/flink/flink-启动.png)

- 启动成功后, 会弹出两个java弹窗, 并在5005和5006端口listen.
> 可访问本地地址localhost:80801 查看flink-ui, 并可提交examples里的jar包执行

![flink-ui](/imgs/flink/flink-ui.png)

## debug调试

### 配置idea远程调试
> 在idea的启动栏, add configuration, 找到remote, 创建
- remote-jobmanager配置, 启动后就可以调试jobmanager模块相关代码执行

![remote-jm](/imgs/flink/remote-jm.png)

- remote-taskmanager配置, 启动后可调试taskmanager相关代码执行

![remote-tm](m/imgs/flink/remote-tm.png)

### flink整体执行流程
> 参考官网的架构图可知,首先由program优化生成streamGraph,
交给client, 由client submit job到jobmanager, 
再由jobmanager分发调度submit task, 交给taskmanager执行

![flink-process](/imgs/flink/process.png)

### jobmanager DEBUG
> 入口类: Dispatcher

![jm-debug](/imgs/flink/flink-jm-debug.png)

### taskmanager
> 入口类: TaskExecutor

![tm-debug](/imgs/flink/flink-debug-tm.png)

这三个组件之间的通信是通过rpc来的, rpc使用了netty, 具体逻辑在handler里.

jobManager和taskManager的日志都在之前创建的log目录里

<H3>最后愉快debug! 嘻嘻!</H3> 
## FAQ
> 1. start-cluster.bat里的两个类是启动类, 但是debug进不去?
```$xslt
org.apache.flink.runtime.entrypoint.StandaloneSessionClusterEntrypoint
org.apache.flink.runtime.taskexecutor.TaskManagerRunner
```
