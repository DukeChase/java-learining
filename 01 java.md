# Java Learning

# 基础语法

# 数组

```java
int[] a = new int[3];
int[] b = new int[]{1,3,5};
int[] c = {1,3,5};
```

## 数组在内存中的存储

| 区域名称  | 作用                             |
| ----- | ------------------------------ |
| 寄存器   | 给CPU使用，和我们开发无关。                |
| 本地方法栈 | JVM在使用操作系统功能的时候使用，和我们开发无关。     |
| 方法区   | 存储可以运行的class文件。                |
| 堆内存   | 存储对象或者数组，new来创建的，都存储在堆内存。      |
| 方法栈   | 方法运行时使用的内存，比如main方法运行，进入方法栈中执行 |

## 数组作为方法参数和返回值

# 类与对象 封装 构造方法

对象内存图

两个对象，调用同一方法内存图

构造方法

方法名与它所在的类名相同。它没有返回值，所以不需要返回值类型，甚至不需要void。

```java
public ConstructorName(){

}
```

JavaBean

# 常用API第一部分

## Scanner Random ArrayList

day07【Scanner类、Random类、ArrayList类】.pdf

### Scanner

```java
Scanner sc = new Scanner(System.in);
sc.nextInt();
```

### Random

`java.util.Random`

```java
Random r = new Random();
r.nextInt();
```

### ArrayList

```java
ArrayList<String> list = new ArrayList<>();
```

`public ArrayList()`

成员方法

* `public boolean add(E e)`

* `public E remove(int Index)`

* `public E get(int index)`

* `public int size()`

## String static Arrayas Math类

day08【String类、static、Arrays类、Math类】.pdf

### String

[String性能提升10倍的几个方法](https://mp.weixin.qq.com/s/KRRLt0EaIwDEPCTGvqnWJA)

官方为我们提供了两种字符串拼加的方案：`StringBuffer` 和 `StringBuilder`，其中 `StringBuilder` 为非线程安全的，而 `StringBuffer` 则是线程安全的

#### 概述

* 字符串不变

* 因为String对象是不可变的，所以它们可以被共享。

* `"abc"`等效于`char[] data = {'a','b','c'}`

#### 使用步骤

```java
// 无参构造 
String str = new String（）； 
// 通过字符数组构造 
char chars[] = {'a', 'b', 'c'}; 
String str2 = new String(chars); 
// 通过字节数组构造 
byte bytes[] = { 97, 98, 99 }; 
String str3 = new String(bytes);
```

#### 常用方法

1. 判断功能的方法
   
   * equals
   
   * equalsIgnoreCase

2. 获取功能的方法
   
   * `public int length()`
   
   * `public String concat(String str)`
   
   * `public char charAt(int index)`
   
   * `public int indexOf(String str)`返回指定子字符串第一次出现在该字符串内的索引。
   
   * `public String substring(int beginIndex)`返回一个子字符串，从beginIndex开始截取字符串到字符
     
     串结尾。
   
   * `public String substring(int beginIndex, int endIndex)`返回一个子字符串，从beginIndex到
     
     endIndex截取字符串。含beginIndex，不含endIndex。

3. 转换功能的方法
   
   * `public char[] toCharrArray()`
   
   * `public byte[] getBytes()`使用平台的默认字符集将该 String编码转换为新的字节数组。
   
   * `public String replace(CharSequence target, CharSequence replacement)`将与target匹配的字符串使
     
     用replacement字符串替换。

4. 分割功能的方法
   
   * `public String[] split(String regex)`将此字符串按照给定的regex（规则）拆分为字符串数组。

### static

#### 概述

修饰成员变量和成员方法，被修饰的成员是属于类的，而不是单单是属于某个对象的。

#### 定义和使用方法

1. 类变量

2. 静态方法
   
   * 注意事项
     
     * 静态方法可以直接访问类变量和静态方法
     
     * 静态方法**不能直接访问**普通成员变量和方法。反之，成员方法可以直接访问类变量和静态方法。
     
     * 静态方法中，不能使用this关键字。

### Arrays类

* `public static String toString(int[] a)`

* `public static void sort(int[] a)`

### Math类

* `public static double abs(double e)`

* `public static double ceil(double e)`

* `public static double floor(double a)`

* `public static long round(double a)`

# 继承与多态

## 继承 super this 抽象类

day09【继承、super、this、抽象类】.pdf

### 继承

### 抽象类

## 接口 多态

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

### 多态

```java
Fu f = new Zi();
f.method()
```

首先检查父类中是否有该方法，如果没有，则编译错误；如果有，执行的是子类重写后的方法。

### 类型转换

`instanceof`

## final 权限 内部类

修饰类，方法和变量

### 权限修饰符

| 权限      | public | protect | default | private |
| ------- | ------ | ------- | ------- | ------- |
| 同一类中    | √      | √       | √       | √       |
| 同一包中√   | √      | √       | √       |         |
| 不同包的子类  | √      | √       |         |         |
| 不同包的无关类 | √      |         |         |         |

### 内部类

* 内部类可以直接访问外部类的成员，包括私有成员。

* 外部类要访问内部类的成员，必须要建立内部类的对象。

### 匿名内部类

# 常用API第二部分

## Object类

## 常用API

# 集合

## Collection 泛型

## List Set

## Map

# 异常与多线程

## 异常 线程

### 异常

## 线程 同步

多线程的两种方式

- extends Thread
- implement Runnable

实现Runnable接口比继承Thread类所具有的优势：

1. 适合多个相同的程序代码的线程去共享一个资源。

2. 可以避免java中的单继承的局限性。

3. 增加程序的健壮性，实现解耦操作，代码可以被多个线程共享，代码和线程独立。

4. 线程池只能放入Runnable或Callable类线程，不能直接放入继承Thread的类

### 线程安全

- 同步代码块 synchronize
- 同步方法
- 锁机制

### 线程状态

| 线程状态          | 导致状态发生条件                                                                                                      |
| ------------- | ------------------------------------------------------------------------------------------------------------- |
| NEW           | 线程刚被创建，但是并未启动。还没调用start方法                                                                                     |
| Runable       | 线程可以在java虚拟机中运行的状态，可能正在运行自己代码，也可能没有，这取决于操 作系统处理器。                                                             |
| Blocked       | 当一个线程试图获取一个对象锁，而该对象锁被其他的线程持有，则该线程进入Blocked状 态；当该线程持有锁时，该线程将变成Runnable状态。                                      |
| Waiting       | 一个线程在等待另一个线程执行一个（唤醒）动作时，该线程进入Waiting状态。进入这个 状态后是不能自动唤醒的，必须等待另一个线程调用notify或者notifyAll方法才能够唤醒。                  |
| Timed Waiting | 同waiting状态，有几个方法有超时参数，调用他们将进入Timed Waiting状态。这一状态 将一直保持到超时期满或者接收到唤醒通知。带有超时参数的常用方法有Thread.sleep 、 Object.wait。 |
| Terminated    | 因为run方法正常退出而死亡，或者因为没有捕获的异常终止了run方法而死亡。                                                                        |

## 线程池、Lambda表达式

# File类与 IO流

## File类 递归

## 字节流 字符流

#### 字节流

1. InputStream

2. OutputStream

#### 字符流

1. Reader
2. Writer

## 缓冲流 转换流 序列化流 打印流

# 属性表

`public Properties()`

# 缓存流 转化流 序列化流 打印流

# 网络编程

socket类

# 反射 注解

# MySQL

# JDBC

Java DataBase Connectivity 