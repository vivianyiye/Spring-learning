中文文档：https://www.docs4dev.com/docs/zh/spring-framework/5.1.3.RELEASE/reference

一.课程介绍

1.Spring框架概述
2002，首次推出了Spring框架的雏形：interface21框架
2004年3月24日发布了1.0正式版
Rod Johnson， Spring Framework的创始人，著名作者，悉尼大学音乐学博士

Spring理念：使现有的技术更加容易使用，本身是一个大杂烩，整合了现有的技术框架

2.IOC容器

3.Aop

4.jdbcTemplate

5.事务管理

6.Spring5新特性

二.Spring框架概述

1.Spring是轻量级的、开源的、非入侵式的、JavaEE框架

2.Spring可以解决企业应用开发的复杂性

3.Spring有两个核心部分：IOC和Aop
（1）IOC：控制反转，把创建对象过程交给Spring进行管理
（2）Aop：面向切面，不修改源代码进行功能增强

4.Spring特点
（1）方便解耦，简化开发-->与IOC有关
（2）Aop编程支持
（3）方便程序测试
（4）方便和其它框架进行整合
（5）方便进行事务操作
（6）降低API开发难度

5.SSH：Struct2+Spring+Hibernate
SSM：SpringMVC+Spring+Mybatis

6.总结：Spring就是一个轻量级的控制反转（IOC）和面向切面编程（AOP）的框架
###
三.入门案例

1.下载Spring5
（1）打开Spring.io下载GA稳定版
（2）下载地址：https://repo.spring.io/release/org/springframework/spring/

![image](https://user-images.githubusercontent.com/75358006/124002234-11504980-da08-11eb-9c41-da66cdb1f5fa.png)

3.导入Spring5相关jar包

4.创建普通类，在这个类创建普通方法

5.创建Spring配置文件，在配置文件配置创建的对象
（1）Spring配置文件使用xml格式
###

三.七大模块、三大思想
![image](https://user-images.githubusercontent.com/75358006/124922031-a916ee80-e02b-11eb-84eb-8e6a79f78176.png)



四.扩展

现代化的Java开发
![image](https://user-images.githubusercontent.com/75358006/124070736-e0f0c580-da70-11eb-9f29-e208d606a1cb.png)

Spring Boot：
一个快速开发的脚手架
基于它可以快速的开发单个微服务
约定大于配置

Spring Cloud：
Spring Cloud是基于Spring Boot实现的

因为现在大多数公司都在使用SpingBoot进行快速开发，学习SpringBoot的前提，需要完全掌握Spring及SpringMVC（承上启下）

弊端：发展了太久，违背了原来的理念，配置十分繁琐，即“配置地狱”


















