<<<<<<< HEAD

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

| 权限      | public | protect | default | private |
| ------- | ------ | ------- | ------- | ------- |
| 同一类中    | √      | √       | √       | √       |
| 同一包中√   | √      | √       | √       |         |
| 不同包的子类  | √      | √       |         |         |
| 不同包的无关类 | √      |         |         |         |

# 内部类

* 内部类可以直接访问外部类的成员，包括私有成员。

* 外部类要访问内部类的成员，必须要建立内部类的对象。

## 匿名内部类

# 常用API

# 集合

# 多线程

## 多线程的两种方式

* extends Thread
* implement Runnable

实现Runnable接口比继承Thread类所具有的优势：

1. 适合多个相同的程序代码的线程去共享一个资源。

2. 可以避免java中的单继承的局限性。

3. 增加程序的健壮性，实现解耦操作，代码可以被多个线程共享，代码和线程独立。

4. 线程池只能放入Runnable或Callable类线程，不能直接放入继承Thread的类

## 线程安全

* 同步代码块 synchronize
* 同步方法
* 锁机制

## 线程状态

| 线程状态          | 导致状态发生条件                                                                                                      |
| ------------- | ------------------------------------------------------------------------------------------------------------- |
| NEW           | 线程刚被创建，但是并未启动。还没调用start方法                                                                                     |
| Runable       | 线程可以在java虚拟机中运行的状态，可能正在运行自己代码，也可能没有，这取决于操 作系统处理器。                                                             |
| Blocked       | 当一个线程试图获取一个对象锁，而该对象锁被其他的线程持有，则该线程进入Blocked状 态；当该线程持有锁时，该线程将变成Runnable状态。                                      |
| Waiting       | 一个线程在等待另一个线程执行一个（唤醒）动作时，该线程进入Waiting状态。进入这个 状态后是不能自动唤醒的，必须等待另一个线程调用notify或者notifyAll方法才能够唤醒。                  |
| Timed Waiting | 同waiting状态，有几个方法有超时参数，调用他们将进入Timed Waiting状态。这一状态 将一直保持到超时期满或者接收到唤醒通知。带有超时参数的常用方法有Thread.sleep 、 Object.wait。 |
| Terminated    | 因为run方法正常退出而死亡，或者因为没有捕获的异常终止了run方法而死亡。                                                                        |

# IO流

## 字节流

1. InputStream

2. OutputStream

## 字符流

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

=======

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

| 权限      | public | protect | default | private |
| ------- | ------ | ------- | ------- | ------- |
| 同一类中    | √      | √       | √       | √       |
| 同一包中√   | √      | √       | √       |         |
| 不同包的子类  | √      | √       |         |         |
| 不同包的无关类 | √      |         |         |         |

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

> > > > > > > 9d311266095ae1d1097ba757b8d3ddcb6043cc89
> > > > > > > JDBCUtils