

# 类与对象 

# 封装

# 构造方法

# 继承

# super this

# 抽象类

# 接口

```java
public interface InterfaceName{
    public abstract void methdoName();   //抽象方法      
    public default void methdoName(){
        // do something
    } //默认方法
    //静态方法       InterfaceName.method()
    //私有方法  只有默认方法可以调用
    //  私有静态防方法 默认方法和静态方法可以调用
}
```

# 多态

```java
Fu f = new Zi();
f.method()
```

首先检查父类中是否有该方法，如果没有，则编译错误；如果有，执行的是子类重写后的方法。

## 类型转换

`instanceof`

# final关键字

修饰类，方法和变量

# 权限修饰符

|权限| public | protect | default | private |
|---| -------- | ------- | ------- | ------- |
|同一类中| √ | √ | √ | √ |
|同一包中√| √ | √ | √ | |
|不同包的子类| √ | √ | | |
|不同包的无关类| √ | | | |

# 内部类

* 内部类可以直接访问外部类的成员，包括私有成员。

* 外部类要访问内部类的成员，必须要建立内部类的对象。

## 匿名内部类



# IO流

字节流

1. InputStream

2. OutputStream

字符流

1. Reader
2. Writer

# 异常处理





# 属性表

`public Properties()`



# 缓存流 转化流 序列化流 打印流



# 网络编程

socket类



# 反射 注解



# MySQL



# JDBC

Java DataBase Connectivity 

JDBCUtils