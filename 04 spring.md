# 内容介绍

1. 框架概述

2. IOC容器
   
   1. IOC底层原理
   
   2. IOC接口（BeanFactory）
   
   3. IOC操作Bean管理（基于XML）
   
   4. IOC操作Bean管理（基于注解）

3. AOP

4. JdbcTemplate

5. 事务管理

6. Spring5新特性

# 1. Spring5 框架概述

1、Spring 是轻量级的开源的 JavaEE 框架

2、Spring 可以解决企业应用开发的复杂性

3、Spring 有两个核心部分：IOC 和 Aop

（1）IOC：**控制反转，把创建对象过程交给 Spring 进行管理**

（2）Aop：**面向切面，不修改源代码进行功能增强**

4、Spring 特点

（1）方便解耦，简化开发

（2）Aop 编程支持

（3）方便程序测试

（4）方便和其他框架进行整合

（5）方便进行事务操作

（6）降低 API 开发难度

# IOC容器

IOC概念和原理

1. 控制反转，把对象创建和对象之间的调用过程，交给spring进行管理

2. 使用IOC的目的：为了降低耦合度

IOC底层原理

1. xml解析 工厂模式 反射

IOC思想基于IOC容器完成，IOC容器底层及时对象工厂

Spring提供IOC容器实现的两种方式：（两个接口）

（1） BeanFactory

（2） **ApplicationContext**
