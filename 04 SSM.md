# MyBatis

### MyBatis introduction

### 搭建MyBatis的核心配置文件
文件位置：`src/main/resource/mybatis_comfig.xml`    MyBatis核心配置文件

```xml
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

2. mapper接口
	相当于Dao，区别在于mapper仅仅是接口，不需要实现
	`UserMapper`  是一个接口，定义数据库的方法，
	```java
	public interface UserMapper {
	/**
	* 添加用户信息
	*/
	int insertUser();
	}
	```
3. MyBatis映射文件
   相关概念：ORM（Object Relation Mapping）对象关系映射
   - 对象：java的实体类对象
   - 关系：关系型数据库
   - 映射：二者之间的关系

|Java概念|数据库概念|
|--------|---------|
|类|表|
|属性|字段/列|
|对象|记录/行|

 1. 映射文件的命名规则：
	表所对应的`实体类的类名+Mapper.xml`
	例如：表`t_user`，映射的实体类为`User`，所对应的映射文件为`UserMapper.xml`
	因此一个映射文件对应一个实体类，对应一张表的操作
	`MyBatis`映射文件用于编写SQL，访问以及操作表中的数据
	`MyBatis`映射文件存放的位置是`src/main/resources/mappers`目录下
2. MyBatis中可以面向接口操作数据，要保证两个一致：
	- mapper接口的全类名和映射文件的命名空间（namespace）保持一致
	- mapper接口中方法的方法名和映射文件中编写SQL的标签的id属性保持一致
`UserMapper.xml`
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
4. Test
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

* `SqlSession`：代表Java程序和数据库之间的会话。（HttpSession是Java程序和浏览器之间的会话）
* `SqlSessionFactory`： 是“生产”SqlSession的“工厂”
* 工厂模式：如果创建某一个对象，使用的过程基本固定，那么我们就可以把创建这个对象的相关代码封装到一个“工厂类”中，以后都使用这个工厂类来“生产”我们需要的对象。

### 增删改查

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


<!--查询一个实体对象-->
<!--User getUserById();--> 
<select id="getUserById" resultType="com.atguigu.mybatis.bean.User"> 
    select * from t_user where id = 2 
</select>


<!-- 查询list集合-->
<!--List<User> getUserList();--> 
<select id="getUserList" resultType="com.atguigu.mybatis.bean.User"> 
    select * from t_user 
</select>
```

### 获取参数值的两种方式
MyBatis获取参数值的两种方式：`${}`和`#{}` 
- `${}`的本质就是字符串拼接，`#{}`的本质就是占位符赋值  
- `${}`使用字符串拼接的方式拼接sql，若为字符串类型或日期类型的字段进行赋值时，需要手动加单引号；但是`#{}`使用占位符赋值的方式拼接sql，此时为字符串类型或日期类型的字段进行赋值时，可以自动添加单引号
1. 单个字面量类型的参数
	若mapper接口中的方法参数为单个的字面量类型  
	此时可以使用`${}`和`#{}`以任意的名称获取参数的值，注意${}需要手动加单引号
2. 多个字面量类型的参数
	若mapper接口中的方法参数为多个时  
	此时MyBatis会自动将这些参数放在一个map集合中，以arg0,arg1...为键，以参数为值；以param1,param2...为键，以参数为值；因此只需要通过`${}`和`#{}`访问map集合的键就可以获取相对应的值，注意`${}`需要手动加单引号
3. map集合参数的类型
	若mapper接口中的方法需要的参数为多个时，此时可以手动创建map集合，将这些数据放在map中只需要通过`${}`和`#{}`访问map集合的键就可以获取相对应的值，注意`${}`需要手动加单引号 
4. 实体类类型的参数
	若mapper接口中的方法参数为实体类对象时此时可以使用`${}`和`#{}`，通过访问实体类对象中的属性名获取属性值，注意`${}`需要手动加单引号
5. 使用`@Param`标识参数
	可以通过@Param注解标识mapper接口中的方法参数  
	此时，会将这些参数放在map集合中，以@Param注解的value属性值为键，以参数为值；以param1,param2...为键，以参数为值；只需要通过${}和#{}访问map集合的键就可以获取相对应的值，  
	注意${}需要手动加单引号

### 各种查询功能
1. 查询一个实体类对象
```java
/**
* 根据用户id查询用户信息
* @param id
* @return
*/
User getUserById(@Param("id") int id);
```

```xml
<!--User getUserById(@Param("id") int id);-->
<select id="getUserById" resultType="User">
select * from t_user where id = #{id}
</select>
```

2. 查询一个list集合
```java
/**

* 查询所有用户信息

* @return

*/

List<User> getUserList();
```

```xml
<!--List<User> getUserList();-->
<select id="getUserList" resultType="User">
select * from t_user
</select>
```

3. 查询单个数据
```java
/**
* 查询用户的总记录数
* @return
* 在MyBatis中，对于Java中常用的类型都设置了类型别名
* 例如： java.lang.Integer-->int|integer
* 例如： int-->_int|_integer
* 例如： Map-->map,List-->list
*/
int getCount();
```

```xml
<!--int getCount();-->
<select id="getCount" resultType="_integer">
select count(id) from t_user
</select>
```

4. 查询一条数据为map集合
```java
/**
* 根据用户id查询用户信息为map集合
* @param id
* @return
*/
Map<String, Object> getUserToMap(@Param("id") int id);
```

```xml
<!--Map<String, Object> getUserToMap(@Param("id") int id);-->
<!--结果： {password=123456, sex=男 , id=1, age=23, username=admin}-->
<select id="getUserToMap" resultType="map">
select * from t_user where id = #{id}
</select>
```

5. 查询多条数据为map集合
- 方式一
```java
/**
* 查询所有用户信息为map集合
* @return
* 将表中的数据以map集合的方式查询，一条数据对应一个map；若有多条数据，就会产生多个map集合，此
时可以将这些map放在一个list集合中获取
*/
List<Map<String, Object>> getAllUserToMap();
```

```xml
<!--Map<String, Object> getAllUserToMap();-->
<select id="getAllUserToMap" resultType="map">
select * from t_user
</select>
```

- 方式二
```java
/**
* 查询所有用户信息为map集合
* @return
* 将表中的数据以map集合的方式查询，一条数据对应一个map；若有多条数据，就会产生多个map集合，并且最终要以一个map的方式返回数据，此时需要通过@MapKey注解设置map集合的键，值是每条数据所对应的map集合
*/
@MapKey("id")
Map<String, Object> getAllUserToMap();
```

```xml
<!--Map<String, Object> getAllUserToMap();-->
<!--
{
1={password=123456, sex=男, id=1, age=23, username=admin},
2={password=123456, sex=男, id=2, age=23, username=张三},
3={password=123456, sex=男, id=3, age=23, username=张三}
}
-->
<select id="getAllUserToMap" resultType="map">
select * from t_user
</select>
```

### 特殊SQL的执行
- 模糊查询
```xml
<!--List<User> testMohu(@Param("mohu") String mohu);-->

<select id="testMohu" resultType="User">

<!--select * from t_user where username like '%${mohu}%'-->

<!--select * from t_user where username like concat('%',#{mohu},'%')-->

select * from t_user where username like "%"#{mohu}"%"

</select>
```
- 批量删除
```xml
<!--int deleteMore(@Param("ids") String ids);-->
<delete id="deleteMore">
delete from t_user where id in (${ids})
</delete>
```
- 动态设置表名
```xml
<!--List<User> getAllUser(@Param("tableName") String tableName);-->
<select id="getAllUser" resultType="User">
select * from ${tableName}
</select>
```
添加功能获取自增的组件

### 自定义映射resultMap


<<<<<<< HEAD

=======
>>>>>>> 20e5998209cc8d1f79e1a39460c278a0139a9ad1
### 动态SQL

- `if`
if标签可通过test属性的表达式进行判断，若表达式的结果为true，则标签中的内容会执行；反之标签中的内容不会执行
```xml
<!--List<Emp> getEmpListByCondition(Emp emp);-->

<select id="getEmpListByMoreTJ" resultType="Emp">
	select * from t_emp where 1=1
	<if test="ename != '' and ename != null">
	and ename = #{ename}
	</if>
	<if test="age != '' and age != null">
	and age = #{age}
	</if>
	<if test="sex != '' and sex != null">
	and sex = #{sex}
	</if>
</select>
```
- `where`  
where和if一般结合使用：  
a>若where标签中的if条件都不满足，则where标签没有任何功能，即不会添加where关键字  
b>若where标签中的if条件满足，则where标签会自动添加where关键字，并将条件最前方多余的and去掉

注意：where标签不能去掉条件最后多余的and
```xml
<select id="getEmpListByMoreTJ2" resultType="Emp">
	select * from t_emp
	<where>
		<if test="ename != '' and ename != null">
		ename = #{ename}
		</if>
		<if test="age != '' and age != null">
		and age = #{age}
		</if>
		<if test="sex != '' and sex != null">
		and sex = #{sex}
		</if>
	</where>
</select>
```
- `trim`  
trim用于去掉或添加标签中的内容 
常用属性：
prefix：在trim标签中的内容的前面添加某些内容
prefixOverrides：在trim标签中的内容的前面去掉某些内容
suffix：在trim标签中的内容的后面添加某些内容
suffixOverrides：在trim标签中的内容的后面去掉某些内容
```xml
<select id="getEmpListByMoreTJ" resultType="Emp">
	select * from t_emp
	<trim prefix="where" suffixOverrides="and">
		<if test="ename != '' and ename != null">
		ename = #{ename} and
		</if>
		<if test="age != '' and age != null">
		age = #{age} and
		</if>
		<if test="sex != '' and sex != null">
		sex = #{sex}
		</if>
	</trim>
</select>
```
- `choose when otherwise`
choose、when、 otherwise相当于if...else if..else
```xml
<!--List<Emp> getEmpListByChoose(Emp emp);-->
<select id="getEmpListByChoose" resultType="Emp">
	select <include refid="empColumns"></include> from t_emp
	<where>
		<choose>
			<when test="ename != '' and ename != null">
			ename = #{ename}
			</when>
			<when test="age != '' and age != null">
			age = #{age}
			</when>
			<when test="sex != '' and sex != null">
			sex = #{sex}
			</when>
			<when test="email != '' and email != null">
			email = #{email}
			</when>
		</choose>
	</where>
</select>
```
- `foreach`
```xml
<!--int insertMoreEmp(List<Emp> emps);-->
<insert id="insertMoreEmp">
	insert into t_emp values
	<foreach collection="emps" item="emp" separator=",">
	(null,#{emp.ename},#{emp.age},#{emp.sex},#{emp.email},null)
	</foreach>
</insert>
<!--int deleteMoreByArray(int[] eids);-->
<delete id="deleteMoreByArray">
	delete from t_emp where
	<foreach collection="eids" item="eid" separator="or">
	eid = #{eid}
	</foreach>
</delete>
<!--int deleteMoreByArray(int[] eids);-->
<delete id="deleteMoreByArray">
	delete from t_emp where eid in
	<foreach collection="eids" item="eid" separator="," open="(" close=")">
	#{eid}
	</foreach>
</delete>
```
<<<<<<< HEAD
- `SQL片段`
sql片段，可以记录一段公共sql片段，在使用的地方通过include标签进行引入
=======
SQL片段
sql片段，可以记录一段公共sql片段，在使用的地方通过`include`标签进行引入
>>>>>>> 20e5998209cc8d1f79e1a39460c278a0139a9ad1
```xml
<sql id="empColumns">
	eid,ename,age,sex,did
</sql>
select <include refid="empColumns"></include> from t_emp
```
### 缓存
一级缓存

一级缓存是SqlSession级别的，通过同一个SqlSession查询的数据会被缓存，下次查询相同的数据，就会从缓存中直接获取，不会从数据库重新访问

使一级缓存失效的四种情况：

1) 不同的SqlSession对应不同的一级缓存

2) 同一个SqlSession但是查询条件不同

3) 同一个SqlSession两次查询期间执行了任何一次增删改操作

4) 同一个SqlSession两次查询期间手动清空了缓存

二级缓存

二级缓存是SqlSessionFactory级别，通过同一个SqlSessionFactory创建的SqlSession查询的结果会被缓存；此后若再次执行相同的查询语句，结果就会从缓存中获取

二级缓存开启的条件：

a>在核心配置文件中，设置全局配置属性cacheEnabled="true"，默认为true，不需要设置
b>在映射文件中设置标签<cache/>
c>二级缓存必须在SqlSession关闭或提交之后有效
d>查询的数据所转换的实体类类型必须实现序列化的接口

使二级缓存失效的情况：
两次查询之间执行了任意的增删改，会使一级和二级缓存同时失效




### 逆向工程
正向工程：先创建Java实体类，由框架负责根据实体类生成数据库表。 Hibernate是支持正向工程的。
逆向工程：先创建数据库表，由框架负责根据数据库表，反向生成如下资源：
- Java实体类
- Mapper接口
- Mapper映射文件
### 分页插件




# Spring

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

## 1. Spring简介
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

### IOC概念和原理

思想
IOC 就是一种反转控制的思想， 而 DI（Dependency Injection） 是对 IOC 的一种具体实现。
1. 控制反转，把对象创建和对象之间的调用过程，交给spring进行管理

2. 使用IOC的目的：为了降低耦合度

### IOC容器

IOC思想
IOC：Inversion of Control，翻译过来是反转控制。

IOC容器在Spring中的实现
Spring 的 IOC 容器就是 IOC 思想的一个落地的产品实现。IOC 容器中管理的组件也叫做 bean。在创建bean 之前，首先需要创建 IOC 容器。Spring 提供了 IOC 容器的两种实现方式（两个接口）：
（1） `BeanFactory`
（2） `ApplicationContext`

ApplicationContext的主要实现类

|类型名|简介|
|------|--|
|ClassPathXmlApplicationContext|通过读取类路径下的 XML 格式的配置文件创建 IOC 容器对象|
|FileSystemXmlApplicationContext|通过文件系统路径读取 XML 格式的配置文件创建 IOC 容器对象|
|ConfigurableApplicationContext|ApplicationContext 的子接口，包含一些扩展方法refresh() 和 close() ，让 ApplicationContext 具有启动、关闭和刷新上下文的能力。|
|WebApplicationContext|专门为 Web 应用准备，基于 Web 环境创建 IOC 容器对象，并将对象引入存入 ServletContext 域中。|

### 基于XML管理bean
`G:\01 尚硅谷\SSM资料`
#### 1、入门案例
1. 引入依赖
2. 创建类
```java
public class HelloWorld {
public void sayHello(){
	System.out.println("helloworld");
	}
}
```
3. 创建Spring的配置文件
4. 在Spring的配置文件中配置bean
```xml
<!--
	配置HelloWorld所对应的bean，即将HelloWorld的对象交给Spring的IOC容器管理
	通过bean标签配置IOC容器所管理的bean
	属性：
	id：设置bean的唯一标识
	class：设置bean所对应类型的全类名
-->
<bean id="helloworld" class="com.atguigu.spring.bean.HelloWorld"></bean>
```
4. 创建测试类
```java
@Test
public void testHelloWorld(){
	ApplicationContext ac = new
		ClassPathXmlApplicationContext("applicationContext.xml");
		// 获取bean
	HelloWorld helloworld = (HelloWorld) ac.getBean("helloworld");
	helloworld.sayHello();
}
```
#### 2、获取bean
1. 根据**id**获取`ac.getBean("helloworld")`
2. 根据**类型**获取`ac.getBean(HelloWorld.class);`
3. 根据**类型和id**获取`ac.getBean("helloworld", HelloWorld.class)`

#### 3、依赖注入之setter注入
```xml
<bean id="studentOne" class="com.atguigu.spring.bean.Student">
	<!-- property标签：通过组件类的setXxx()方法给组件对象设置属性 -->
	<!-- name属性：指定属性名（这个属性名是getXxx()、setXxx()方法定义的，和成员变量无关）-->
	<!-- value属性：指定属性值 -->
	<property name="id" value="1001"></property>
	<property name="name" value="张三"></property>
	<property name="age" value="23"></property>
	<property name="sex" value="男"></property>
</bean>
```
#### 4、依赖注入之构造器注入
```xml
<bean id="studentTwo" class="com.atguigu.spring.bean.Student">
	<constructor-arg value="1002"></constructor-arg>
	<constructor-arg value="李四"></constructor-arg>
	<constructor-arg value="33"></constructor-arg>
	<constructor-arg value="女"></constructor-arg>
</bean>
```

#### 5、特殊值处理
null值
```xml
<property name="name">
	<null />
</property>
```

xml实体
```xml
<!-- 小于号在XML文档中用来定义标签的开始，不能随便使用 -->

<!-- 解决方案一：使用XML实体来代替 -->

<property name="expression" value="a < b"/>
```
CDATA节
```xml
<property name="expression">
	<!-- 解决方案二：使用CDATA节 -->
	<!-- CDATA中的C代表Character，是文本、字符的含义，CDATA就表示纯文本数据 -->
	<!-- XML解析器看到CDATA节就知道这里是纯文本，就不会当作XML标签或属性来解析 -->
	<!-- 所以CDATA节中写什么符号都随意 -->
	<value><![CDATA[a < b]]></value>
</property>
#### 为类类型属性赋值
```

#### 6、为类类型属性赋值
1. 引用外部已声明的bean  
```xml
<bean id="studentFour" class="com.atguigu.spring.bean.Student">
	<property name="id" value="1004"></property>
	<property name="name" value="赵六"></property>
	<property name="age" value="26"></property>
	<property name="sex" value="女"></property>
	<!-- ref属性：引用IOC容器中某个bean的id，将所对应的bean为属性赋值 -->
	<property name="clazz" ref="clazzOne"></property>
</bean>
```
2. 内部bean
```xml
<bean id="studentFour" class="com.atguigu.spring.bean.Student">
	<property name="id" value="1004"></property>
	<property name="name" value="赵六"></property>
	<property name="age" value="26"></property>
	<property name="sex" value="女"></property>
	<property name="clazz">
		<!-- 在一个bean中再声明一个bean就是内部bean -->
		<!-- 内部bean只能用于给属性赋值，不能在外部通过IOC容器获取，因此可以省略id属性 -->
		<bean id="clazzInner" class="com.atguigu.spring.bean.Clazz">
		<property name="clazzId" value="2222"></property>
		<property name="clazzName" value="远大前程班"></property>
		</bean>
	</property>
</bean>
```
3. 级联属性赋值  
```xml
<bean id="studentFour" class="com.atguigu.spring.bean.Student">
	<property name="id" value="1004"></property>
	<property name="name" value="赵六"></property>
	<property name="age" value="26"></property>
	<property name="sex" value="女"></property>
	<!-- 一定先引用某个bean为属性赋值，才可以使用级联方式更新属性 -->
	<property name="clazz" ref="clazzOne"></property>
	<property name="clazz.clazzId" value="3333"></property>
	<property name="clazz.clazzName" value="最强王者班"></property>
</bean>
```

#### 7、为数组类型属性赋值
```xml
<bean id="studentFour" class="com.atguigu.spring.bean.Student">
	<property name="id" value="1004"></property>
	<property name="name" value="赵六"></property>
	<property name="age" value="26"></property>
	<property name="sex" value="女"></property>
	<!-- ref属性：引用IOC容器中某个bean的id，将所对应的bean为属性赋值 -->
	<property name="clazz" ref="clazzOne"></property>
	<property name="hobbies">
		<array>
		<value>抽烟</value>
		<value>喝酒</value>		
		<value>烫头</value>
		</array>
	</property>
</bean>
```
#### 8、为集合类型属性赋值
1. 为List集合类型属性赋值
```xml
<bean id="clazzTwo" class="com.atguigu.spring.bean.Clazz">
	<property name="clazzId" value="4444"></property>
	<property name="clazzName" value="Javaee0222"></property>
	<property name="students">
		<list>
			<ref bean="studentOne"></ref>
			<ref bean="studentTwo"></ref>
			<ref bean="studentThree"></ref>
		</list>
	</property>
</bean>
```

2. 为Map集合类型属性赋值
```xml
<bean id="teacherOne" class="com.atguigu.spring.bean.Teacher">
	<property name="teacherId" value="10010"></property>
	<property name="teacherName" value="大宝"></property>
</bean>
<bean id="teacherTwo" class="com.atguigu.spring.bean.Teacher">
	<property name="teacherId" value="10086"></property>
	<property name="teacherName" value="二宝"></property>
</bean>
<bean id="studentFour" class="com.atguigu.spring.bean.Student">
	<property name="id" value="1004"></property>
	<property name="name" value="赵六"></property>
	<property name="age" value="26"></property>
	<property name="sex" value="女"></property>
	<!-- ref属性：引用IOC容器中某个bean的id，将所对应的bean为属性赋值 -->
	<property name="clazz" ref="clazzOne"></property>
	<property name="hobbies">
	<array>
		<value>抽烟</value>
		<value>喝酒</value>
		<value>烫头</value>
	</array>
	</property>
	<property name="teacherMap">
		<map>
			<entry>
				<key>
					<value>10010</value>
				</key>
				<ref bean="teacherOne"></ref>
				</entry>
				<entry>
				<key>
					<value>10086</value>
				</key>
			<ref bean="teacherTwo"></ref>
			</entry>
		</map>
	</property>
</bean>
```

3. 引用集合类型的bean
```xml
<!--list集合类型的bean-->
<util:list id="students">
	<ref bean="studentOne"></ref>
	<ref bean="studentTwo"></ref>
	<ref bean="studentThree"></ref>
</util:list>
<!--map集合类型的bean-->
<util:map id="teacherMap">
	<entry>
		<key>
		<value>10010</value>
		</key>
		<ref bean="teacherOne"></ref>
	</entry>
	<entry>
		<key>
		<value>10086</value>
		</key>
		<ref bean="teacherTwo"></ref>
	</entry>
</util:map>
<bean id="clazzTwo" class="com.atguigu.spring.bean.Clazz">
	<property name="clazzId" value="4444"></property>
	<property name="clazzName" value="Javaee0222"></property>
	<property name="students" ref="students"></property>
</bean>
<bean id="studentFour" class="com.atguigu.spring.bean.Student">
	<property name="id" value="1004"></property>
	<property name="name" value="赵六"></property>
	<property name="age" value="26"></property>
	<property name="sex" value="女"></property>
	<!-- ref属性：引用IOC容器中某个bean的id，将所对应的bean为属性赋值 -->
	<property name="clazz" ref="clazzOne"></property>
	<property name="hobbies">
		<array>
			<value>抽烟</value>
			<value>喝酒</value>
			<value>烫头</value>
		</array>
	</property>
	<property name="teacherMap" ref="teacherMap"></property>
</bean>
```
#### 9、p命名空间

#### 10、引入外部属性文件
1. 引入依赖
```xml
<!-- MySQL驱动 -->
<dependency>
<groupId>mysql</groupId>
<artifactId>mysql-connector-java</artifactId>
<version>8.0.16</version>
</dependency>
<!-- 数据源 -->
<dependency>
<groupId>com.alibaba</groupId>
<artifactId>druid</artifactId>
<version>1.0.31</version>
</dependency>
```
2. 创建外部属性文件
```properties
jdbc.user=root

jdbc.password=atguigu

jdbc.url=jdbc:mysql://localhost:3306/ssm?serverTimezone=UTC

jdbc.driver=com.mysql.cj.jdbc.Driver
```
3. 引入属性文件
`<context:property-placeholder location="classpath:jdbc.properties"/>`

4. 配置bean
```xml
<bean id="druidDataSource" class="com.alibaba.druid.pool.DruidDataSource">
	<property name="url" value="${jdbc.url}"/>
	<property name="driverClassName" value="${jdbc.driver}"/>
	<property name="username" value="${jdbc.user}"/>
	<property name="password" value="${jdbc.password}"/>
</bean>
```
测试
```java
@Test
public void testDataSource() throws SQLException {
	ApplicationContext ac = new ClassPathXmlApplicationContext("spring
	datasource.xml");
	DataSource dataSource = ac.getBean(DataSource.class);
	Connection connection = dataSource.getConnection();
	System.out.println(connection);
}
```
#### 11、bean的作用域
概念：在Spring中可以通过配置bean标签的scope属性来指定bean的作用域范围，各取值含义参加下表：

|取值|含义|创建对象时机|
|----|---|--------|
|singleton|在IOC容器中，这个bean的对象始终为单实例|IOC容器初始化时|
|prototype|这个bean在IOC容器中有多个实例|获取bean时|

#### 12、bean的生命周期
具体的生命周期过程
- bean对象创建
- 给bean对象设置属性
- bean对象初始化之前操作（由bean的后置处理器负责）
- bean对象初始化（需在配置bean是指定初始化方法）
- bean初始化之后操作（由bean的后置处理器负责）
- bean对象就绪可以使用
- bean对象销毁（需在配置bean时指定销毁方法）
- IOC容器关闭
#### 13、FactoryBean

FactoryBean是Spring提供的一种整合第三方框架的常用机制。和普通的bean不同，配置一个FactoryBean类型的bean，在获取bean的时候得到的并不是class属性中配置的这个类的对象，而是
getObject()方法的返回值。通过这种机制，Spring可以帮我们把复杂组件创建的详细过程和繁琐细节都屏蔽起来，只把最简洁的使用界面展示给我们。
将来我们整合Mybatis时，Spring就是通过FactoryBean机制来帮我们创建SqlSessionFactory对象的。
```java

public class UserFactoryBean implements FactoryBean<User> {
	`@Override
	public User getObject() throws Exception {
	return new User();
}
	@Override	
	public Class<?> getObjectType() {
	return User.class;
}

}
```

`<bean id="user" class="com.atguigu.bean.UserFactoryBean"></bean>`

```java
@Test
public void testUserFactoryBean(){
	//获取IOC容器
	ApplicationContext ac = new ClassPathXmlApplicationContext("spring
	factorybean.xml");
	User user = (User) ac.getBean("user");
	System.out.println(user);
}
```
`
#### 14、基于XML的自动装配

配置bean
使用***bean标签的autowire属性***设置自动装配效果
自动装配：
根据指定的策略，在IOC容器中匹配某一个bean，自动为指定的bean中所依赖的类类型或接口类
型属性赋值

1. 自动装配方式：`byType`
根据类型匹配IOC容器中的某个兼容类型的bean，为属性自动赋值  
若在IOC中，没有任何一个兼容类型的bean能够为属性赋值，则该属性不装配，即值为默认值
`null`  
若在IOC中，有多个兼容类型的bean能够为属性赋值，则抛出异常`NoUniqueBeanDefinitionException`
```xml
<bean id="userController"
class="com.atguigu.autowire.xml.controller.UserController" autowire="byType">
</bean>
<bean id="userService"
class="com.atguigu.autowire.xml.service.impl.UserServiceImpl" autowire="byType">
</bean>
<bean id="userDao" class="com.atguigu.autowire.xml.dao.impl.UserDaoImpl"></bean>
````
2. 自动装配方式：`byName`
将自动装配的属性的属性名，作为bean的id在IOC容器中匹配相对应的bean进行赋值  
```xml
<bean id="userController"
class="com.atguigu.autowire.xml.controller.UserController" autowire="byName">
</bean>
<bean id="userService"
class="com.atguigu.autowire.xml.service.impl.UserServiceImpl" autowire="byName">
</bean>
<bean id="userServiceImpl"
class="com.atguigu.autowire.xml.service.impl.UserServiceImpl" autowire="byName">
</bean>
<bean id="userDao" class="com.atguigu.autowire.xml.dao.impl.UserDaoImpl"></bean>
<bean id="userDaoImpl" class="com.atguigu.autowire.xml.dao.impl.UserDaoImpl">
</bean>
```

### 基于注解管理bean
#### 标记与扫描
标识组件的常用注解:  
- `@Component`：将类标识为普通组件 
- `@Controller`：将类标识为控制层组件 
- `@Service`：将类标识为业务层组件 
- `@Repository：` 将类标识为持久层组件

`@Controller、@Service、@Repository`这三个注解只是在@Component注解的基础上起了三个新的名字

扫描组件
```xml
<context:component-scan base-package="com.atguigu">
</context:component-scan>
```

指定要排除的组件
```xml
<context:component-scan base-package="com.atguigu">
<!-- context:exclude-filter标签：指定排除规则 -->
<!--
type：设置排除或包含的依据
type="annotation"，根据注解排除，expression中设置要排除的注解的全类名
type="assignable"，根据类型排除，expression中设置要排除的类型的全类名
-->
	<context:exclude-filter type="annotation"
expression="org.springframework.stereotype.Controller"/>
	<!--<context:exclude-filter type="assignable"
expression="com.atguigu.controller.UserController"/>-->
</context:component-scan>
```

仅扫描指定组件
```xml
<context:component-scan base-package="com.atguigu" use-default-filters="false">
<!-- context:include-filter标签：指定在原有扫描规则的基础上追加的规则 -->
<!-- use-default-filters属性：取值false表示关闭默认扫描规则 -->
<!-- 此时必须设置use-default-filters="false"，因为默认规则即扫描指定包下所有类 -->
<!--
	type：设置排除或包含的依据
	type="annotation"，根据注解排除，expression中设置要排除的注解的全类名
	type="assignable"，根据类型排除，expression中设置要排除的类型的全类名
-->
	<context:include-filter type="annotation"
expression="org.springframework.stereotype.Controller"/>
	<!--<context:include-filter type="assignable"
expression="com.atguigu.controller.UserController"/>-->
</context:component-scan>
```
#### 基于注解的自动装配

导入依赖
```
<dependencies>  
    <!-- 基于Maven依赖传递性，导入spring-context依赖即可导入当前所需所有jar包 -->  
    <dependency>  
        <groupId>org.springframework</groupId>  
        <artifactId>spring-context</artifactId>  
        <version>5.3.1</version>  
    </dependency>    <!-- junit测试 -->  
    <dependency>  
        <groupId>junit</groupId>  
        <artifactId>junit</artifactId>  
        <version>4.12</version>  
        <scope>test</scope>  
    </dependency></dependencies>
```


- `@Component`
- `@Controller`
- `@Service`
- `Repository`


②`@Autowired注解`

* 通过注解+扫描所配置的bean的id，默认值为类的小驼峰，即类名的首字母为小写的结果  
* 可以通过标识组件的注解的value属性值设置bean的自定义的id  
*  
* @Autowired:实现自动装配功能的注解  
1. @Autowired注解能够标识的位置  
	* a>标识在成员变量上，此时不需要设置成员变量的set方法  
	* b>标识在set方法上  
	* c>标识在为当前成员变量赋值的有参构造上  
2. @Autowired注解的原理  
	* a>默认通过`byType`的方式，在IOC容器中通过类型匹配某个`bean`为属性赋值  
	* b>若有多个类型匹配的`bean`，此时会自动转换为`byName`的方式实现自动装配的效果，即将要赋值的属性的属性名作为`bean`的id匹配某个`bean`为属性赋值  
	* c>若`byType`和`byName`的方式都无妨实现自动装配，即IOC容器中有多个类型匹配的bean 且这些bean的id和要赋值的属性的属性名都不一致，此时抛异常：`NoUniqueBeanDefinitionException`  
	* d>此时可以在要赋值的属性上，添加一个注解`@Qualifier`通过该注解的`value`属性值，指定某个`bean`的`id`，将这个`bean`为属性赋值  

* 注意：若IOC容器中没有任何一个类型匹配的bean，此时抛出异常：`NoSuchBeanDefinitionException ` 
* 在`@Autowired`注解中有个属性`required`，默认值为true，要求必须完成自动装配  
* 可以将required设置为false，此时能装配则装配，无法装配则使用属性的默认值
## AOP

### 代理模式

### AOP概念及相关术语
概述  
AOP（Aspect Oriented Programming）是一种设计思想，是软件设计领域中的面向切面编程，它是面向对象编程的一种补充和完善，它以通过预编译方式和运行期动态代理方式实现，在不修改源代码的情况下给程序动态统一添加额外功能的一种技术。

相关术语
1. 横向关注点
2. 通知
3. 切面
4. 目标
5. 代理
6. 连接点
7. 切入点
作用
- 简化代码：把方法中固定位置的重复的代码抽取出来，让被抽取的方法更专注于自己的核心功能，提高内聚性。
- 代码增强：把特定的功能封装到切面类中，看哪里有需要，就往上套，被套用了切面逻辑的方法就被切面给增强了。

### 基于注解的AOP

#### 技术说明
- 动态代理（`InvocationHandler`）：JDK原生的实现方式，需要被代理的目标类必须实现接口。因为这个技术要求代理对象和目标对象实现同样的接口（兄弟两个拜把子模式）。
- `cglib`：通过继承被代理的目标类（认干爹模式）实现代理，所以不需要目标类实现接口。
- `AspectJ`：本质上是静态代理，将代理逻辑“织入”被代理的目标类编译得到的字节码文件，所以最终效果是动态的。`weaver`就是织入器。Spring只是借用了`AspectJ`中的注解。

#### 准备工作
1. 添加依赖
```xml
<!-- spring-aspects会帮我们传递过来aspectjweaver -->
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-aspects</artifactId>
	<version>5.3.1</version>
</dependency>
```
2. 准备被代理的目标资源
```java
public interface Calculator {
	int add(int i, int j);
	int sub(int i, int j);
	int mul(int i, int j);
	int div(int i, int j);
}
```
```java
@Component
public class CalculatorPureImpl implements Calculator {
	@Override
	public int add(int i, int j) {
		int result = i + j;
		System.out.println("方法内部 result = " + result);
		return result;
	}
	@Override
	public int sub(int i, int j) {
		int result = i - j;
		System.out.println("方法内部 result = " + result);
		return result;
	}

	@Override
	public int mul(int i, int j) {
		int result = i * j;
		System.out.println("方法内部 result = " + result);
		return result;
	}
	@Override
	public int div(int i, int j) {
		int result = i / j;
		System.out.println("方法内部 result = " + result);
		return result;
	}
}
```
3. 创建切面类并配置
```java
// @Aspect表示这个类是一个切面类
// @Component注解保证这个切面类能够放入IOC容器
@Aspect
@Component
public class LogAspect {
@Before("execution(public int com.atguigu.aop.annotation.CalculatorImpl.*
(..))")
	public void beforeMethod(JoinPoint joinPoint){
		String methodName = joinPoint.getSignature().getName();
		String args = Arrays.toString(joinPoint.getArgs());
		System.out.println("Logger-->前置通知，方法名："+methodName+"，参
		数："+args);
	}
@After("execution(* com.atguigu.aop.annotation.CalculatorImpl.*(..))")
	public void afterMethod(JoinPoint joinPoint){
		String methodName = joinPoint.getSignature().getName();
		System.out.println("Logger-->后置通知，方法名："+methodName);
	}
					   
@AfterReturning(value = "execution(*
com.atguigu.aop.annotation.CalculatorImpl.*(..))", returning = "result")
		public void afterReturningMethod(JoinPoint joinPoint, Object result){
		String methodName = joinPoint.getSignature().getName();
		System.out.println("Logger-->返回通知，方法名："+methodName+"，结
		果："+result);
	}

@AfterThrowing(value = "execution(*
com.atguigu.aop.annotation.CalculatorImpl.*(..))", throwing = "ex")
	public void afterThrowingMethod(JoinPoint joinPoint, Throwable ex){
		String methodName = joinPoint.getSignature().getName();
		System.out.println("Logger-->异常通知，方法名："+methodName+"，异常："+ex);
	}

@Around("execution(* com.atguigu.aop.annotation.CalculatorImpl.*(..))")
	public Object aroundMethod(ProceedingJoinPoint joinPoint){
		String methodName = joinPoint.getSignature().getName();
		String args = Arrays.toString(joinPoint.getArgs());
		Object result = null;
		try {
		System.out.println("环绕通知-->目标对象方法执行之前");
		//目标对象（连接点）方法的执行
		result = joinPoint.proceed();
		System.out.println("环绕通知-->目标对象方法返回值之后");
		} catch (Throwable throwable) {
		throwable.printStackTrace();
		System.out.println("环绕通知-->目标对象方法出现异常时");
		} finally {
		System.out.println("环绕通知-->目标对象方法执行完毕");
		}
		return result;
	}
}
```

在spring的配置文件中配置：
```xml
<!--
基于注解的AOP的实现：
1、将目标对象和切面交给IOC容器管理（注解+扫描）
2、开启AspectJ的自动代理，为目标对象自动生成代理
3、将切面类通过注解@Aspect标识
-->
<context:component-scan base-package="com.atguigu.aop.annotation">
</context:component-scan>
<aop:aspectj-autoproxy />
```

各种通知
- 前置通知：使用@Before注解标识，在被代理的目标方法前执行
- 返回通知：使用@AfterReturning注解标识，在被代理的目标方法成功结束后执行（寿终正寝）
- 异常通知：使用@AfterThrowing注解标识，在被代理的目标方法异常结束后执行（死于非命）
- 后置通知：使用@After注解标识，在被代理的目标方法最终结束后执行（盖棺定论）
- 环绕通知：使用@Around注解标识，使用try...catch...finally结构围绕整个被代理的目标方法，包括上面四种通知对应的所有位置

#### 切入点表达式语法

#### 重用切入表达式
1. 声明
```java
@PointCut("excution(* com.atguigu.aop.annotation.*.*(..))")
public void pointCut(){}
```
2. 在同一个切面中使用
```java
@Before("pointCut()")
public void beforeMethod(JoinPoint joinPoint){
	String methodName = joinPoint.getSignature().getName();
	String args = Arrays.toString(joinPoint.getArgs());
	System.out.println("Logger-->前置通知，方法名："+methodName+"，参数："+args);
}
```
4. 在不同切面中使用
```java
@Before("com.atguigu.aop.CommonPointCut.pointCut()")
public void beforeMethod(JoinPoint joinPoint){
	String methodName = joinPoint.getSignature().getName();
	String args = Arrays.toString(joinPoint.getArgs());	
	System.out.println("Logger-->前置通知，方法名："+methodName+"，参数："+args);

}
```

#### 获取通知的相关信息
1. 获取连接点信息
2. 获取目标方法返回值
3. 获取目标方法异常
#### 环绕通知

#### 切面的优先级

### 基于XML的AOP（了解）

## 声明式事务


# SpringMVC

## 什么是MVC

## 入门案例
- 配置web.xml文件
```xml
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"  
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"  
         version="4.0">  
    <!--  
        配置SpringMVC的前端控制器DispatcherServlet  
        SpringMVC的配置文件默认的位置和名称：  
        位置：WEB-INF下  
        名称：<servlet-name>-servlet.xml，当前配置下的配置文件名为SpringMVC-servlet.xml
        
        url-pattern中/和/*的区别：  
        /：匹配浏览器向服务器发送的所有请求（不包括.jsp）  
        /*：匹配浏览器向服务器发送的所有请求（包括.jsp）  
        jsp文件由tomcat的JspServlet处理
    -->  
    <servlet>
        <servlet-name>SpringMVC</servlet-name>  
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>  
        <!--设置SpringMVC配置文件的位置和名称-->  
        <init-param>  
            <param-name>contextConfigLocation</param-name>  
            <param-value>classpath:springmvc.xml</param-value>  
        </init-param>        <!--将DispatcherServlet的初始化时间提前到服务器启动时-->  
        <load-on-startup>1</load-on-startup>  
    </servlet>    
    <servlet-mapping>        
	    <servlet-name>SpringMVC</servlet-name>  
        <url-pattern>/</url-pattern>  
    </servlet-mapping>  
</web-app>

```

- 创建请求控制器
由于前端控制器对浏览器发送的请求进行了统一的处理，但是具体的请求有不同的处理过程，因此需要创建处理具体请求的类，即***请求控制器***
请求控制器中每一个处理请求的方法成为***控制器方法***
因为SpringMVC的控制器由一个POJO（普通的Java类）担任，因此需要通过`@Controller`注解将其标识为一个***控制层组件***，交给Spring的IoC容器管理，此时SpringMVC才能够识别控制器的存在。
```java
@Controller
public class HelloController{

}
```
- SpringMVC的配置文件
```xml
<!-- 自动扫描包 -->
<context:component-scan base-package="com.atguigu.mvc.controller"/>
<!-- 配置Thymeleaf视图解析器 -->
<bean id="viewResolver"
class="org.thymeleaf.spring5.view.ThymeleafViewResolver">
	<property name="order" value="1"/>
	<property name="characterEncoding" value="UTF-8"/>
	<property name="templateEngine">
	<bean class="org.thymeleaf.spring5.SpringTemplateEngine">
	<property name="templateResolver">
			<bean		class="org.thymeleaf.spring5.templateresolver.SpringResourceTemplateResolver">
			<!-- 视图前缀 -->
				<property name="prefix" value="/WEB-INF/templates/"/>
				<!-- 视图后缀 -->
				<property name="suffix" value=".html"/>
				<property name="templateMode" value="HTML5"/>
				<property name="characterEncoding" value="UTF-8" />
			</bean>
		</property>
		</bean>
	</property>
</bean>
<!--
处理静态资源，例如html、js、css、jpg
若只设置该标签，则只能访问静态资源，其他请求则无法访问
此时必须设置<mvc:annotation-driven/>解决问题
-->
<mvc:default-servlet-handler/>
<!-- 开启mvc注解驱动 -->
<mvc:annotation-driven>
	<mvc:message-converters>
		<!-- 处理响应中文内容乱码 -->
		<bean
		class="org.springframework.http.converter.StringHttpMessageConverter">
			<property name="defaultCharset" value="UTF-8" />
			<property name="supportedMediaTypes">
				<list>
					<value>text/html</value>
					<value>application/json</value>
				</list>
			</property>
		</bean>
	</mvc:message-converters>
</mvc:annotation-driven>
```

浏览器发送请求，若请求地址符合前端控制器的`url-pattern`，该请求就会被前端控制器`DispatcherServlet`处理。
前端控制器会读取SpringMVC的核心配置文件，通过扫描组件找到控制器，将请求地址和控制器中@RequestMapping注解的value属性值进行匹配，若匹配成功，该注解所标识的控制器方法就是处理请求的方法。
处理请求的方法需要返回一个字符串类型的视图名称，该视图名称会被***视图解析器***解析，加上前缀和后缀组成视图的路径，通过Thymeleaf对视图进行渲染，最终转发到视图所对应页面

## @RequestMapping注解
1. `@RequestMapping`注解标识的位置  
	* `@RequestMapping`标识一个类：设置映射请求的请求路径的初始信息  
	* `@RequestMapping`标识一个方法：设置映射请求请求路径的具体信息  
2. `@RequestMapping`注解value属性  
	* 作用：通过请求的请求路径匹配请求  
	* `value`属性是数组类型，即当前浏览器所发送请求的请求路径匹配`value`属性中的任何一个值  
	* 则当前请求就会被注解所标识的方法进行处理  
3. `@RequestMapping`注解的`method`属性  
	* 作用：通过请求的请求方式匹配请求  
	* `method`属性是`RequestMethod`类型的数组，即当前浏览器所发送请求的请求方式匹配`method`属性中的任何一中请求方式  
	* 则当前请求就会被注解所标识的方法进行处理  
	* 若浏览器所发送的请求的请求路径和`@RequestMapping`注解`value`属性匹配，但是请求方式不匹配  
	* 此时页面报错：`405 - Request method 'xxx' not supported`
	* 在@RequestMapping的基础上，结合请求方式的一些派生注解：  
	* `@GetMapping,@PostMapping,@DeleteMapping,@PutMapping ` 
4. `@RequestMapping`注解的`params`属性  
	* 作用：通过请求的请求参数匹配请求，即浏览器发送的请求的请求参数必须满足params属性的设置  
	* params可以使用四种表达式：  
	* "param"：表示当前所匹配请求的请求参数中必须携带param参数  
	* "!param"：表示当前所匹配请求的请求参数中一定不能携带param参数  
	* "param=value"：表示当前所匹配请求的请求参数中必须携带param参数且值必须为value  
	* "param!=value"：表示当前所匹配请求的请求参数中可以不携带param，若携带值一定不能是value  
	* 若浏览器所发送的请求的请求路径和@RequestMapping注解value属性匹配，但是请求参数不匹配  
	* 此时页面报错：`400 - Parameter conditions "username" not met for actual request parameters:  `
5. `@RequestMapping`注解的`headers`属性  
	* 作用：通过请求的请求头信息匹配请求，即浏览器发送的请求的请求头信息必须满足headers属性的设置  
	* 若浏览器所发送的请求的请求路径和@RequestMapping注解value属性匹配，但是请求头信息不匹配  
	* 此时页面报错：404  
6. SpringMVC支持ant风格的路径  
	* 在`@RequestMapping`注解的value属性值中设置一些特殊字符  
	* ?:任意的单个字符（不包括?）  
	* *:任意个数的任意字符（不包括?和/）  
	* **:任意层数的任意目录，注意使用方式只能**写在双斜线中，前后不能有任何的其他字符  
7. @RequestMapping注解使用路径中的占位符  
	* 传统：`/deleteUser?id=1`  
	* rest：`/user/delete/1 ` 
	* 需要在`@RequestMapping`注解的value属性中所设置的路径中，使用{xxx}的方式表示路径中的数据  
	* 在通过`@PathVariable`注解，将占位符所标识的值和控制器方法的形参进行绑定

### SpringMVC获取请求参数

- 通过控制器方法的行参获取请求参数
- `@RequestParam`
- `@RequsetHeader`
- `@CookieValue`


- 通过POJO获取
请求参数的名字与实体类属性名 一致

- 解决获取请求路径的乱码问题
配置spring的编码过滤器
``

1. 通过servletAPI获取  
	* 只需要在控制器方法的形参位置设置`HttpServletRequest`类型的形参  
	* 就可以在控制器方法中使用request对象获取请求参数  
2. 通过控制器方法的形参获取  
	* 只需要在控制器方法的形参位置，设置一个形参，形参的名字和请求参数的名字一致即可  
3. `@RequestParam`：将请求参数和控制器方法的形参绑定  
	* @RequestParam注解的三个属性：value、required、defaultValue  
	* `value`:设置和形参绑定的请求参数的名字  
	* `required`:设置是否必须传输value所对应的请求参数  
	* 默认值为true，表示value所对应的请求参数必须传输，否则页面报错：  
	* 400 - Required String parameter 'xxx' is not present  
	* 若设置为false，则表示value所对应的请求参数不是必须传输，若为传输，则形参值为null  
	* `defaultValue`:设置当没有传输value所对应的请求参数时，为形参设置的默认值，此时和required属性值无关  
4. `@RequestHeader`：将请求头信息和控制器方法的形参绑定  
5. `@CookieValue`：将cookie数据和控制器方法的形参绑定  
6. 通过控制器方法的实体类类型的形参获取请求参数  
	* 需要在控制器方法的形参位置设置实体类类型的形参，要保证实体类中的属性的属性名和请求参数的名字一致  
	* 可以通过实体类类型的形参获取请求参数  
7. 解决获取请求此参数的乱码问题      
	* 在web.xml中配置Spring的编码过滤器`org.springframework.web.filter.CharacterEncondingFilter`

## 域对象共享数据
* 向域对象共享数据：  
1. 通过ModelAndView向请求域共享数据  
	* 使用ModelAndView时，可以使用其Model功能向请求域共享数据  
	* 使用View功能设置逻辑视图，但是控制器方法一定要将`ModelAndView`作为方法的返回值  
2. 使用Model向请求域共享数据  
3. 使用ModelMap向请求域共享数据  
4. 使用map向请求域共享数据  
5. Model和ModelMap和map的关系  
	* 其实在底层中，这些类型的形参最终都是通过`BindingAwareModelMap`创建  
	* `public class BindingAwareModelMap extends ExtendedModelMap {} ` 
	* `public class ExtendedModelMap extends ModelMap implements Model {}`  
	* `public class ModelMap extends LinkedHashMap<String, Object> {}`

- 向`session`域共享数据

```java
@RequestMapping("/testSession")
public String testSession(HttpSession session){
	session.setAttribute("testSessionScope", "hello,session");
	return "success";
}
```
- 向`application`域共享数据
```java
@RequestMapping("/testApplication")
public String testApplication(HttpSession session){
	ServletContext application = session.getServletContext();
	application.setAttribute("testApplicationScope", "hello,application");
	return "success";
}
```

## springMVC的视图

`thymeleafView`

`InternalResourceViewResolver`   视图解析器

`RedirectView`
## RETFUL

REST：Representational State Transfer，表现层资源状态转移。

SpringMVC 提供了 `HiddenHttpMethodFilter` 帮助我们将 POST 请求转换为 DELETE 或 PUT 请求

HiddenHttpMethodFilter 处理put和delete请求的条件：

1. 当前请求的请求方式必须为post
2. 当前请求必须传输请求参数_method

满足以上条件，`HiddenHttpMethodFilter` 过滤器就会将当前请求的请求方式转换为
请求参数`_method`的值，因此请求参数`_method`的值才是最终的请求方式


在web.xml中注册`HiddenHttpMethodFilter`

```xml
<filter>  
    <filter-name>CharacterEncodingFilter</filter-name>  
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>  
    <init-param>        
	    <param-name>encoding</param-name>  
        <param-value>UTF-8</param-value>  
    </init-param>    
    <init-param>        
	    <param-name>forceEncoding</param-name>  
        <param-value>true</param-value>  
    </init-param>
</filter>  
<filter-mapping>  
    <filter-name>CharacterEncodingFilter</filter-name>  
    <url-pattern>/*</url-pattern>  
</filter-mapping>
```

在web.xml中注册时，必须先注册`CharacterEncodingFilter`，再注册`HiddenHttpMethodFilter`
原因：
在 CharacterEncodingFilter 中通过 `request.setCharacterEncoding(encoding) `方法设置字
符集的`request.setCharacterEncoding(encoding)` 方法要求前面不能有任何获取请求参数的操作
而 HiddenHttpMethodFilter 恰恰有一个获取请求方式的操作：
`String paramValue = request.getParameter(this.methodParam);`

一个典型的ssm web应用配置的web.xml文件如下
包括***编码过滤器，请求方式过滤器，前端控制器***

```xml
<!--设置Spring的编码过滤器-->  
<filter>  
    <filter-name>CharacterEncodingFilter</filter-name>  
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>  
    <init-param>        <param-name>encoding</param-name>  
        <param-value>UTF-8</param-value>  
    </init-param>    <init-param>        <param-name>forceEncoding</param-name>  
        <param-value>true</param-value>  
    </init-param></filter>  
<filter-mapping>  
    <filter-name>CharacterEncodingFilter</filter-name>  
    <url-pattern>/*</url-pattern>  
</filter-mapping>  
  
<!--设置处理请求方式的过滤器-->  
<filter>  
    <filter-name>HiddenHttpMethodFilter</filter-name>  
    <filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>  
</filter>  
<filter-mapping>  
    <filter-name>HiddenHttpMethodFilter</filter-name>  
    <url-pattern>/*</url-pattern>  
</filter-mapping>  
  
<!--设置SpringMVC的前端控制器-->  
<servlet>  
    <servlet-name>SpringMVC</servlet-name>  
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>  
    <init-param>        <param-name>contextConfigLocation</param-name>  
        <param-value>classpath:springmvc.xml</param-value>  
    </init-param>    <load-on-startup>1</load-on-startup>  
</servlet>  
<servlet-mapping>  
    <servlet-name>SpringMVC</servlet-name>  
    <url-pattern>/</url-pattern>  
</servlet-mapping>
```
## RESTFul案例

## 9. SpringMVC处理ajax请求
- `@RequestBody`



- `ResponseBody`

`@ResponseBody`用于标识一个控制器方法，可以将该方法的返回值直接作为响应报文的响应体响应到浏览器

- 9.5、`@RestController`注解

`@RestController`注解是springMVC提供的一个复合注解，标识在控制器的类上，就相当于为类添加了`@Controller`注解，并且为其中的每个方法添加了`@ResponseBody`注解

## 文件下载和下载

- `ResponseEntity`用于控制器方法的返回值类型，该控制器方法的返回值就是响应到浏览器的响应报文使用ResponseEntity实现下载文件的功能

- `MultipartFile`  文件上传要求`form`表单的请求方式必须为`post`，并且添加属性`enctype="multipart/form-data"`
SpringMVC中将上传的文件封装到MultipartFile对象中，通过此对象可以获取文件相关信息

1. 添加依赖
```xml
<!-- https://mvnrepository.com/artifact/commons-fileupload/commons-fileupload -->	
<dependency>
<groupId>commons-fileupload</groupId>
<artifactId>commons-fileupload</artifactId>
<version>1.3.1</version>
</dependency>
```
2. 在SpringMVC配置文件中添加配置
```xml
<!--必须通过文件解析器的解析才能将文件转换为MultipartFile对象-->
<bean id="multipartResolver"
class="org.springframework.web.multipart.commons.CommonsMultipartResolver">
</bean>
```
3. 编写控制器方法

```java

/**  
 * Date:2022/7/9 
 * Author:ybc 
 * Description: 
 * ResponseEntity:可以作为控制器方法的返回值，表示响应到浏览器的完整的响应报文  
 *  
 * 文件上传的要求：  
 * 1、form表单的请求方式必须为post  
 * 2、form表单必须设置属性enctype="multipart/form-data"  
 */
 @Controller  
public class FileUpAndDownController {  
  
    @RequestMapping("/test/up")  //上传
    public String testUp(MultipartFile photo, HttpSession session) throws IOException {  
        //获取上传的文件的文件名  
        String fileName = photo.getOriginalFilename();  
        //获取上传的文件的后缀名  
        String hzName = fileName.substring(fileName.lastIndexOf("."));  
        //获取uuid  
        String uuid = UUID.randomUUID().toString();  
        //拼接一个新的文件名  
        fileName = uuid + hzName;  
        //获取ServletContext对象  
        ServletContext servletContext = session.getServletContext();  
        //获取当前工程下photo目录的真实路径  
        String photoPath = servletContext.getRealPath("photo");  
        //创建photoPath所对应的File对象  
        File file = new File(photoPath);  
        //判断file所对应目录是否存在  
        if(!file.exists()){  
            file.mkdir();  
        }  
        String finalPath = photoPath + File.separator + fileName;  
        //上传文件  
        photo.transferTo(new File(finalPath));  
        return "success";  
    }  
  
    @RequestMapping("/test/down")  
    public ResponseEntity<byte[]> testResponseEntity(HttpSession session) throws IOException {  
        //获取ServletContext对象  
        ServletContext servletContext = session.getServletContext();  
        //获取服务器中文件的真实路径  
        String realPath = servletContext.getRealPath("img");  
        realPath = realPath + File.separator + "1.jpg";  
        //创建输入流  
        InputStream is = new FileInputStream(realPath);  
        //创建字节数组，is.available()获取输入流所对应文件的字节数  
        byte[] bytes = new byte[is.available()];  
        //将流读到字节数组中  
        is.read(bytes);  
        //创建HttpHeaders对象设置响应头信息  
        MultiValueMap<String, String> headers = new HttpHeaders();  
        //设置要下载方式以及下载文件的名字  
        headers.add("Content-Disposition", "attachment;filename=1.jpg");  
        //设置响应状态码  
        HttpStatus statusCode = HttpStatus.OK;  
        //创建ResponseEntity对象  
        ResponseEntity<byte[]> responseEntity = new ResponseEntity<>(bytes, headers, statusCode);  
        //关闭输入流  
        is.close();  
        return responseEntity;  
    }  
  
}
```


## 拦截器

## 异常处理器

SpringMVC提供了一个处理控制器方法执行过程中所出现的异常的接口：`HandlerExceptionResolver`

`HandlerExceptionResolver`接口的实现类有：`DefaultHandlerExceptionResolver`和

`SimpleMappingExceptionResolver`

SpringMVC提供了自定义的异常处理器SimpleMappingExceptionResolver，使用方式：

## 注解配置springMVC



# SSM整合
