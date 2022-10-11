# SSM

## Mybatis

mybatis_comfig.xml    核心配置文件

```xml
<?xml version="1.0" encoding="UTF-8" ?> 
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "http://mybatis.org/dtd/mybatis-3-config.dtd"> 
<configuration> <!--设置连接数据库的环境--> 
    <environments default="development"> 
        <environment id="development"> 
            <transactionManager type="JDBC"/> 
                <dataSource type="POOLED"> 
                    <property name="driver" value="com.mysql.cj.jdbc.Driver"/> 
                    <property name="url" value="jdbc:mysql://localhost:3306/ssm? serverTimezone=UTC"/> 
                    <property name="username" value="root"/> 
                    <property name="password" value="123456"/> 
                </dataSource> 
        </environment> 
    </environments> 
    <!--引入映射文件--> 
    <mappers> 
        <package name="mappers/UserMapper.xml"/> 
    </mappers> 
</configuration>
```

UserMapper.xml

UserMapper  是一个接口，定义数据库的方法，

```xml
<?xml version="1.0" encoding="UTF-8" ?> 
<!DOCTYPE mapper 
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" 
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd"> 
<mapper namespace="com.atguigu.mybatis.mapper.UserMapper"> 
    <!--int insertUser();--> 
    <insert id="insertUser"> 
        insert into t_user values(null,'admin','123456',23,'男','12345@qq.com') 
    </insert> 
</mapper>
```

## Test

```java
//读取MyBatis的核心配置文件 
InputStream is = Resources.getResourceAsStream("mybatis-config.xml"); 
//创建SqlSessionFactoryBuilder对象 
SqlSessionFactoryBuilder sqlSessionFactoryBuilder = new SqlSessionFactoryBuilder(); 
//通过核心配置文件所对应的字节输入流创建工厂类SqlSessionFactory，生产SqlSession对象 
SqlSessionFactory sqlSessionFactory = sqlSessionFactoryBuilder.build(is); 
//创建SqlSession对象，此时通过SqlSession对象所操作的sql都必须手动提交或回滚事务 
//SqlSession sqlSession = sqlSessionFactory.openSession(); 
//创建SqlSession对象，此时通过SqlSession对象所操作的sql都会自动提交 
SqlSession sqlSession = sqlSessionFactory.openSession(true); 

//通过代理模式创建UserMapper接口的代理实现类对象 UserMapper 
userMapper = sqlSession.getMapper(UserMapper.class); 
//调用UserMapper接口中的方法，就可以根据UserMapper的全类名匹配元素文件，
//通过调用的方法名匹配 映射文件中的SQL标签，并执行标签中的SQL语句 
int result = userMapper.insertUser(); 
//sqlSession.commit(); 
System.out.println("结果："+result);
```

* SqlSession：代表Java程序和数据库之间的会话。（HttpSession是Java程序和浏览器之间的会话）

* SqlSessionFactory： 是“生产”SqlSession的“工厂”

* 工厂模式：如果创建某一个对象，使用的过程基本固定，那么我们就可以把创建这个对象的相关代码封装到一个“工厂类”中，以后都使用这个工厂类来“生产”我们需要的对象。

增删改查

```xml
<!--int insertUser();--> 
<insert id="insertUser"> 
    insert into t_user values(null,'admin','123456',23,'男') 
</insert>


<!--int deleteUser();--> 
<delete id="deleteUser"> 
    delete from t_user where id = 7 
</delete>


<!--int updateUser();--> 
<update id="updateUser"> 
    update t_user set username='ybc',password='123' where id = 6 
</update>



<!--User getUserById();--> 
<select id="getUserById" resultType="com.atguigu.mybatis.bean.User"> 
    select * from t_user where id = 2 
</select>



<!--List<User> getUserList();--> 
<select id="getUserList" resultType="com.atguigu.mybatis.bean.User"> 
    select * from t_user 
</select>
```

获取参数值的两种方式

各种查询功能

特殊SQL的执行

动态SQL

if

where

trim

choose

when

otherwise

foreach

缓存

## Spring

内容介绍

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

## IOC

IOC概念和原理

1. 控制反转，把对象创建和对象之间的调用过程，交给spring进行管理

2. 使用IOC的目的：为了降低耦合度

IOC底层原理

1. xml解析 工厂模式 反射

IOC思想基于IOC容器完成，IOC容器底层及时对象工厂

Spring提供IOC容器实现的两种方式：（两个接口）

（1） BeanFactory

（2） **ApplicationContext**

ApplicationContext的主要实现类

基于XML管理bean

入门案例

获取bean

依赖注入之setter注入

依赖注入之构造器注入

特殊值处理

为类类型属性赋值

为数组类型属性赋值

为集合类型属性赋值

p命名空间

引入外部属性文件

bean的作用域

bean的生命周期

FactoryBean

基于XML的自动装配

基于注解管理bean

@Component：将类标识为普通组件 

@Controller：将类标识为控制层组件 

@Service：将类标识为业务层组件 

@Repository：将类标识为持久层组件

## AOP

# SpringMVC

配置文件

```xml

```
