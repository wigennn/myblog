---
title: 关于spring
date: 2020-02-29 19:59:52
tags:
---
关于spring主要两大块IOC和AOP,这两块可以说是构成spring的核心.
粗读过<spring源码解析>,不说精通,但也是学到很多

首先关于IOC,说白了就是spring管理java对象，通过xml配置，注解等方式注入bean
在IOC中最顶层的接口是BeanFactory,最后我们启动spring是通过ApplicationContext这个类
spring Bean生命周期:
    实例化-属性赋值-初始化-销毁
    new实例化-属性注入-设置beanName-设置上下文-执行初始化方法-InitializingBean执行afterpropertiesSet方法-使用bean-destroy销毁bean
    
循环依赖:
什么是循环依赖? A引用B，B引用C，C又引用A
spring解决方法：
    1)通过构造器注入，直接BeanCurrentIncreationException抛出异常，创建一个bean就把这个bean放入当前创建bean池中，如果创建bean的过程中发现缓存池中已存在，就抛出异常
    2)通过setter注入，有个addSingleFactory方法，提前暴露ObjectFactory，这是提前暴露单例工厂方法，然后获取该该bean
    3)通过prototype作用域注入,直接抛出异常

关于AOP
springAOP的实现无非是代理
spring开启aop:配置文件中<aop:aspectj-autoproxy />
静态代理
动态代理: 
    JDK动态代理, 实现invocationHandler接口,只能代理接口
    开启cglib动态代理proxy-target-class=true,实现MethodInterceptor，代理类和接口 
    
关于mybatis
SqlSessionFactory 两个属性configLocation和dataSource,读mybatis的配置文件
MapperFactoryBean 扫描调用数据库接口
MapperScannerConfigurer 属性basePackage扫描接口包

关于事务
开启事务 <tx:annotation-driven transaction-manager= "transactionManager"/>
DataSourceTransactionManager
事务传播行为:当一个事务A方法调用事务B方法时，methodB怎么运行?是在A事务中运行还是重启一个事务
    required:当前事务A存在，methodB在事务A中执行，否则重启一个事务
    supports:当前方法不需要上下文，存在当前事务，该方法在这个事务中运行
    mandatory:强制执行，必须在当前事务中执行,否则抛出异常
    required_new:当前事务挂起，新起一个事务
    not_supported:表示该方法不应运行在事务中,当前存在事务,事务挂起
    never:不应运行在当前事务中，并抛出异常
    nested:嵌套事务
    
关于springmvc
请求-dispatchServlet-handlerMapping(生成handlerexecutorChain)-handlerAdapter(生成ModeAndView)-ViewSolver(解析视图返回View)

关于jms activeMQ
配置文件
ActiveMQConnectionFactory
JmsTemplate
ActiveMQQueue
MessageListener




