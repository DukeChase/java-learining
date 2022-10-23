# Java Learning

# 基础语法

常量 变量

数据类型

* 基本数据类型 整数浮点数 字符 布尔

* 引用数据类型 类 数组 接口

基本数据类型

| 数据类型 | 关键字     | 内存占用 | 默认值|取值范围             |
| ---- | ------- | ---- | ---------------- |---|
| 字节型  | int     | 1byte    |                  | |
| 短整型  | short   | 2byte    |                  | |
| 整型   | int     | 4byte    |  |-2的31次方~2的31次方-1 |
| 长整型  | long    | 8byte    |  |-2的63次方~2的63次方-1 |
| 单精度  | float   | 4byte    |                  |   |
| 双精度  | double  | 8byte    |                  |   |
	| 字符型  | char    | 2byte    |                  |   |
| 布尔型  | boolean | 1byte    |                  |   |

 >long类型：建议数据后加L表示 不加L默认为int
> 
> float类型：建议数据后加F表示。

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

java都是值传递，基本类型是传递的是值，引用类型是传递的是对象的地址

> 方法的参数为基本类型时,传递的是数据值. 方法的参数为引用类型时,传递的是地址值.

# 类与对象 封装 构造方法

## 对象内存图

两个对象，调用同一方法内存图

## 构造方法

方法名与它所在的类名相同。它没有返回值，所以不需要返回值类型，甚至不需要void。

```java
public ConstructorName(){
    // 空构造器
}
```

### JavaBean

`JavaBean` 是 `Java`语言编写类的一种标准规范。符合 `JavaBean` 的类，要求类必须是具体的和公共的，并且具有无参数的构造方法，提供用来操作成员变量的 set 和 get 方法。

# 常用API第一部分

## 1. Scanner Random ArrayList

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
ArrayList<String> list = new ArrayList<>(); // 泛型
```

`public ArrayList()`

成员方法

* `public boolean add(E e)`

* `public E remove(int Index)`

* `public E get(int index)`

* `public int size()`

## 2. String static Arrayas Math类

day08【String类、static、Arrays类、Math类】.pdf

### String

[String性能提升10倍的几个方法](https://mp.weixin.qq.com/s/KRRLt0EaIwDEPCTGvqnWJA)

官方为我们提供了两种字符串拼加的方案：`StringBuffer` 和 `StringBuilder`，其中 `StringBuilder` 为非线程安全的，而 `StringBuffer` 则是线程安全的。

1. 概述
* 字符串不变

* 因为String对象是不可变的，所以它们可以被共享。

* `"abc"`等效于`char[] data = {'a','b','c'}`
2. 使用步骤

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

1. 常用方法
* 判断功能的方法
  
  * equals
  
  * equalsIgnoreCase

* 获取功能的方法
  
  * `public int length()`
  
  * `public String concat(String str)`
  
  * `public char charAt(int index)`
  
  * `public int indexOf(String str)`返回指定子字符串第一次出现在该字符串内的索引。
  
  * `public String substring(int beginIndex)`返回一个子字符串，从beginIndex开始截取字符串到字符
    
    串结尾。
  
  * `public String substring(int beginIndex, int endIndex)`返回一个子字符串，从beginIndex到
    
    endIndex截取字符串。含beginIndex，不含endIndex。

* 转换功能的方法
  
  * `public char[] toCharrArray()`
  
  * `public byte[] getBytes()`使用平台的默认字符集将该 String编码转换为新的字节数组。
  
  * `public String replace(CharSequence target, CharSequence replacement)`将与target匹配的字符串使
    
    用replacement字符串替换。

* 分割功能的方法
  
  * `public String[] split(String regex)`将此字符串按照给定的regex（规则）拆分为字符串数组。

### static

* 概述

修饰成员变量和成员方法，被修饰的成员是属于类的，而不是单单是属于某个对象的。

* 定义和使用方法
1. 类变量
2. 静态方法
   * 注意事项
     * 静态方法可以直接访问类变量和静态方法
     * 静态方法**不能直接访问**普通成员变量和方法。反之，成员方法可以直接访问类变量和静态方法。
     * 静态方法中，不能使用this关键字。
3. 静态代码块
	* 静态代码块在类加载时执行，并且只执行一次
	* 静态代码块在一个类中可以编写多个，并且遵循自上而下的顺序依次执行。
	* 静态代码块在构造方法之前执行
4. 实例代码块
	- 实例代码块在构造方法执行之前执行，构造方法执行依次，实例代码块对应执行一次
5. [实例代码块与静态代码块](https://blog.csdn.net/weixin_51755941/article/details/123153754)

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

## Object类 常用API

### Object类

1. `public String toString`

2. `public boolean equals(Object obj)`

默认地址比较

如果没有覆盖重写equals方法，那么Object类中默认进行`==`运算符的对象地址比较，只要不是同一个对象，结果必然为false。

对象内容比较
如果希望进行对象的内容比较，即所有或指定的部分成员变量相同就判定两个对象相同，则可以覆盖重写equals方法。例如：

```java
public class Person {    
    private String name;
    private int age;

    @Override
    public boolean equals(Object o) {
        // 如果对象地址一样，则认为相同
        if (this == o)
            return true;
        // 如果参数为空，或者类型信息不一样，则认为不同
        if (o == null || getClass() != o.getClass())
            return false;
        // 转换为当前类型
        Person person = (Person) o;
        // 要求基本类型相等，并且将引用类型交给java.util.Objects类的equals静态方法取用结果
        return age == person.age && Objects.equals(name, person.name);
    }
}
```

### 日期时间类

### System类

- `public static long currentTimeMillis()`：返回以毫秒为单位的当前时间。

- `public static void arraycopy(Object src, int srcPos, Object dest, int destPos, int length)`：将数组中指定的数据拷贝到另一个数组中。

### StringBuilder类

StringBuilder常用的方法有2个：

- `public StringBuilder append(...)`：添加任意类型数据的字符串形式，并***返回当前对象自身***。

- `public String toString()`：将当前StringBuilder对象转换为**String对象**。

### 包装类

| 基本类型    | 对应的包装类（位于java.lang包中） |
| ------- | --------------------- |
| byte    | Byte                  |
| short   | Short                 |
| int     | **Integer**           |
| long    | Long                  |
| float   | Float                 |
| double  | Double                |
| char    | **Character**         |
| boolean | Boolean               |

# 集合

## Collection 泛型

### Collection集合

1. 集合概述
   
   * 集合与数组的区别
     
     * 数组长度固定。集合长度可变。
     
     * 数组中存储的是同一类型的元素，可以存储基本数据类型值。集合存储的都是对象。而且对象的类型可以不一致。在开发中一般当对象多的时候，使用集合进行存储。

2. 集合框架

集合按照其存储结构可以分为两大类，分别是单列集合 `java.util.Collection` 和双列集合`java.util.Map`

**Collection**:单列集合类的根接口，用于存储一系列符合某种规则的元素，它有两个重要的子接口，分别是 `java.util.List` 和` java.util.Set` 。其中，`List` 的特点是元素有序、元素可重复。 Set 的特点是元素无序，而且不可重复。 

* `List` 接口的主要实现类有 `java.util.ArrayList`和 `java.util.LinkedList` ，

* ` Set` 接口的主要实现类有 `java.util.HashSet` 和`java.util.TreeSet`
3. Collection常用功能
   
   * `public boolean add(E e)`
   
   * `public void clear()`
   
   * `public boolean remove(E e)`
   
   * `public boolean contains(E e)`
   
   * `public boolean isEmpty()`
   
   * `public int size()`
   
   * `public object[] toArray()`

### Iterator迭代器

#### Iterator接口

* `public Iterator iterator()`获取集合对应的迭代器，用来遍历集合中的元素的

* `public E next()`  返回迭代的下一个元素

* `public boolean hasNext()`如果仍有元素可以迭代，则返回 true。

```java
Collection<String> coll = new ArrayList<>();
coll.add();

Iterator it = coll.iterator();
while(it.hasNext()){
    String s = it.next();
    System.out.println(s)
}
```

#### 迭代器的实现原理

#### 增强for

```java
for (元素的数据类型 变量 ：Collection集合或数组){
    doSomething();
}
```

### 泛型

1 定义和使用含有泛型的类

`修饰符 class 类名<代表泛型的变量> { }`

2 含有泛型的方法

`修饰符 <代表泛型的变量> 返回值类型 方法名(参数){ }`

3 含有泛型的接口

`修饰符 interface接口名<代表泛型的变量> { }`

## List Set

* List接口中常用方法，List作为Collection集合的子接口，不但继承了Collection接口中的全部方法，而且还增加了一些根据元素索引来操作集合的特有方法
  
  * `public void add(int index,E element)`
  
  * `public E get(index)`
  
  * `public E remove(index)`
  
  * `public E set(int index ,E element)`

* `List`
  
  * ArrayList
  
  * LinkedList
    
    * `public void addFirst(E e)`
    
    * `public void addLast(E e)`
    
    * `public E getFirst()`
    
    * `public E getLast()`
    
    * `public E removeFirst()`
    
    * `public E removeLast()`
    
    * `public E pop`
    
    * `public void push`
    
    * `public boolean isEmpty()`

* `Set`
  
  同样继承自`Collection`接口
  
  * `HashSet`
    
    * `HashSet`是根据对象的哈希值来确定元素在集合中存在位置，因此具有良好的存取和查找性能。保证元素唯一性的方式依赖于：`hashCode`与`equals`方法
    
    * 如果我们往集合中存放自定义的对象，那么保证其唯一，就必须复写`hashCode`和`equals`方法建立属于当前对象的比较方式。
    
    * hashCode相等，不一定equals
    
    * equals则hashCode一定相等；
  
  * `LinkedSet`

### 可变参数

`修饰符 返回值类型 methodName(参数类型... 形参名){ }`

`修饰符 返回值类型 methodName(参数类型[] 形参名){ }`

后面这种定义，在调用时必须传递**数组**，而前者可以**直接传递数据**即可

### Collections

* Collections是集合工具类，用来对集合进行操作。

* `puclic static <T> bollean addAll(Collection<T> c,T...elements)`

* `public static void shuffle(List<?> list) `

* `public static <T> void sort(List<T> list)`

* `public static <T> void sort(List<T> list ,Comparator<? super <T>)`

## Map

### Map集合

 [面试官：为什么要重写hashcode和equals方法？](https://mp.weixin.qq.com/s/QZPezSruj0qvBUJEM4jB0g)

Map常用子类

* HashMap

* LinkedHashMap

Map中常用的方法

* `public V put(K key, V value)`

* `public V remove(object key)`

* `public V get(object key)`

* `public Set<k> keySet()`

* `public Set<Map.Entry<K,V>> entrySet()`

# 异常与多线程

## 异常 线程

### 异常

* 概念

* 体系

异常的根类是 `java.lang.Throwable` ，其下有两个子类：  
`java.lang.Error` 与 `java.lang.Exception` ，平常所说的异常指 `java.lang.Exception`。

分类`Throwable`中的常用方法

* `public void printStackTrace()`

* `public String getMessage()`

* `public String toString()`

### 异常的处理

`throw`

`throws`

`try catch`

`finally`

### 自定义异常

### 线程

* 并发：指两个或多个事件在同一个时间段内发生。

* 并行：指两个或多个事件在同一时刻发生（同时发生）。

程序计数器 虚拟机栈 本地方法栈 是线程私有的。
堆和方法区是线程共享的。

## 线程 同步

多线程的两种方式

1. `extends Thread`
2. `implement Runnable`
```java
public class MyThread extends Thread{

	public MyThread(String name){
		super(name);
	}
	@Override
	public void run(){
		for(int i=0;i<10;i++){
		System.out.println("")
		}
	}
}
```

```java
public static void MultiThreadTest(){  
    //   创建自定义线程对象  
    test.MyThread mt = new test.MyThread("新的线程！");  
    //开启新线程  
    mt.start();  
    // 在主方法中执行for循环  
    for (int i = 0; i < 10; i++) {  
        System.out.println("main线程！"+ i);  
    }  
}
```

```java
public class MyRunnable implements Runnable{  
  
    @Override  
    public void run() {  
        for (int i = 0; i < 20; i++) {  
            System.out.println(Thread.currentThread().getName()+" "+i);  
        }  
    }  
}
``` 

```java
public static void MultiThreadRunnableTest(){  
    test.MyRunnable mr = new test.MyRunnable();  
    Thread t = new Thread(mr,"小强");  
    t.start();  
    for (int i = 0; i < 20; i++) {  
        System.out.println("旺财"+i);  
    }  
  
}
```

实现Runnable接口比继承Thread类所具有的**优势**：

1. 适合多个相同的程序代码的线程去**共享一个资源**。
2. 可以避免java中的单继承的局限性。
3. 增加程序的健壮性，实现解耦操作，代码可以被多个线程共享，代码和线程独立。
4. 线程池只能放入Runnable或Callable类线程，不能直接放入继承Thread的类

### 线程安全

线程同步
- 同步代码块 `synchronize`
- 同步方法 `synchronize`
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

### 等待唤醒机制

### 线程池

线程池概念：其实就是一个容纳多个线程的容器，其中的线程可以反复使用，省去了频繁创建线程对象的操作，

无需反复创建线程而消耗过多资源

线程池的使用

`public static ExecutorService newFixedThreadPool(int nThreads)` 返回线程池对象。(创建的是有界线程池,也就是池中的线程个数可以指定最大数量)

获取到了一个线程池`ExecutorService`对象，那么怎么使用呢，在这里定义了一个使用线程池对象的方法如下：

`public Future<?> submit(Runnable task)`获取线程池中的某一个线程对象，并执行

### Lambda表达式

# File类与 IO流

## File类 递归

### File类

1. 构造方法

 `public File(String pathname)` ：通过将给定的路径名字符串转换为抽象路径名来创建新的 File实例。

`public File(String parent, String child)` ：从父路径名字符串和子路径名字符串创建新的 File实例。

`public File(File parent, String child)` ：从父抽象路径名和子路径名字符串创建新的 File实例

2. 常用方法

获取功能的方法

* `public String getAbsolutePath()`：返回此File的绝对路径名字符串

* `public String getPath() `：将此File转换为路径名字符串。

* `public String getName()` ：返回由此File表示的文件或目录的名称。

* `public long length()`：返回由此File表示的文件的长度。

绝对路径和相对路径

判断功能的方法

* `public boolean exists() `：此File表示的文件或目录是否实际存在。

* `public boolean isDirectory() `：此File表示的是否为目录。

* `public boolean isFile()`：此File表示的是否为文件。

创建删除功能的方法

* `public boolean createNewFile()` ：当且仅当具有该名称的文件尚不存在时，创建一个新的空文件。
* `public boolean delete()` ：删除由此File表示的文件或目录。
* `public boolean mkdir() `：创建由此File表示的目录。
* `public boolean mkdirs()`：创建由此File表示的目录，包括任何必需但不存在的父目录。

3. 目录的遍历
* `public String[] list()` 返回一个String数组，表示该File目录中的所有子文件或目录。
* `public File listFiles()`返回一个File数组，表示该File目录中的所有的子文件或目录。

### 递归

## 字节流 字符流

### IO概述

|     | 输入流         | 输出流          |
| --- | ----------- | ------------ |
| 字节流 | InputStream | OutputStream |
| 字符流 | Reader      | Writer       |

### 字节流

#### 字节输出流

java.io.OutputStream 抽象类是表示字节输出流的所有类的超类，将指定的字节信息写出到目的地。它定义了字节输出流的基本共性功能方法。

* `public void close()`

* `public void flush()` 刷新此输出流并强制任何缓冲的输出字节被写出。

* `public void write(byte[] b)` 

* `public void write(byte[] b, int off,int len)` 


`FileOutputStream` OutputStream的子类
构造方法
`public FileOutputStream(File file)`
`public FileOutpotStream(String name)`
写出字节数
`write(int b)`
`write(byte[] b)`
`write(byte[] b, int off, int len)`

数据追加续写
`public FileOutputStream(File file, boolean append)`
`public FileOutputStream(String name,boolean append)`

#### 字节输入流

`java.io.InputStream` 抽象类是表示字节输入流的所有类的超类，可以读取字节信息到内存中。它定义了字节输入流的基本共性功能方法。

* `public void close()`

* `public abstract int read()`

* `public int read(byte[] b) `：从输入流中读取一些字节数，并将它们存储到字节数组 b中 。

`FileInputStream`  InputStream子类
构造方法
`FileInputStream(File file)`
`FileInputStream(String name)`
读入字节数据
read()   读取一个字节数据，提升为int类型，读到文件末尾，返回-1
read(byte[] b)  每次读取b的长度个字节到数组中，返回**读取到的有效字节个数**，读取到末尾时，返回 -1

>tips:使用数组读取，每次读取多个字节，减少了系统间的IO操作次数，从而提高了读写的效率，建议开发中使用。




### 字符流

1. Reader
   
   * `public void close()` ：关闭此流并释放与此流相关联的任何系统资源。
   
   * `public int read()` ：从输入流读取一个字符。
   
   * `public int read(char[] cbuf)` ：从输入流中读取一些字符，并将它们存储到字符数组 cbuf中 。
   
	FileReader

2. Writer
   
   * `void write(int c)` 写入单个字符。
   
   * `void write(char[] cbuf)` 写入字符数组。
   
   * `abstract void write(char[] cbuf, int off, int len)` 写入字符数组的某一部分,offff数组的开始索引,len写的字符个数。
   
   * `void write(String str)` 写入字符串。
   
   * `void write(String str, int off, int len)` 写入字符串的某一部分,off字符串的开始索引,len写的字符个数。
   
   * `void flush()` 刷新该流的缓冲。
   
   * `void close() `关闭此流，但要先刷新它。
   
   FileWriter

### 属性集

`public Properties()`

`public Object setProperty(String key, String value) `：保存一对属性。

`public String getProperty(String key) `：使用此属性列表中指定的键搜索属性值。

`public Set<String> stringPropertyNames() `：所有键的名称的集合。

`public void load(InputStream inStream) `：从字节输入流中读取键值对

```java
public class ProDemo2 { 
    public static void main(String[] args) throws FileNotFoundException { 
        // 创建属性集对象 
        Properties pro = new Properties(); 
        // 加载文本中信息到属性集 
        pro.load(new FileInputStream("read.txt")); 
        // 遍历集合并打印 
        Set<String> strings = pro.stringPropertyNames(); 
        for (String key : strings ) { 
            System.out.println(key+" ‐‐ "+pro.getProperty(key)); 
        } 
    } 
}
输出结果： 
filename ‐‐ a.txt 
length ‐‐ 209385038 
location ‐‐ D:\a.txt
```

## 缓冲流 转换流 序列化流 打印流

### 缓冲流

字节缓冲流： `BufferedInputStream` ，`BufferedOutputStream`

字符缓冲流： `BufferedReader` ，`BufferedWriter`

字节缓冲流
`public BufferedInputStream(InputStream in)`
`public BufferedOutputStream(OutputStream out)`

字符缓冲流
`public BufferedReader(Reader in)`
`public BufferedWriter(Writer out)`
特有方法
BufferedReader  `public String readLint()`
BufferedWriter `public void newLine()`

### 转换流

Character Encoding
Charset

`InputStreamReader`   Reader的子类

`InputStreamReader(InputStream in, String charsetName) `: 创建一个指定字符集的字符流

`OutPutStreamWriter`  Writer的子类

`OutputStreamWriter(OutputStream in, String charsetName)` : 创建一个指定字符集的字符流。

### 序列化

`public ObjectOutputStream(OutputStream out) `：创建一个指定OutputStream的ObjectOutputStream。

`public final void writeObject (Object obj) `: 将指定的对象写出。

`public ObjectInputStream(InputStream in) `：创建一个指定InputStream的ObjectInputStream

`public final Object readObject () `: 读取一个对象

### 打印流

`public PrintStream(String fileName) `：使用指定的文件名创建一个新的打印流

# 网络编程

## 入门

软件结构

c/s b/s

协议分类

tcp  面向连接的通信协议  

三次握手

第一次握手，客户端向服务器端发出连接请求，等待服务器确认。

第二次握手，服务器端向客户端回送一个响应，通知客户端收到了连接请求。

第三次握手，客户端再次向服务器端发送确认信息，确认连接。整个交互过程如下图所示。

udp 无连接

网络编程三要素

协议 地址 端口号

## TCP通信程序
* Socket

`public Socket(String host,int port)`创建套接字对象并将其连接到指定主机上的指定端口号。如果指定的host是null ，则相当于指定地址为回送地址。

method

`public InputStream getInputStream()` 返回此套接字的输入流`

`public OutputStream getOutputStream()` ：返回此套接字的输出流。

`public void close()` ：关闭此套接字

`public void shutdownOutput()` ：禁用此套接字的输出流。

* ServerSocket

`public ServerSocket(int port) `：使用该构造方法在创建ServerSocket对象时，就可以将其绑定到一个指定的端口号上，参数port就是端口号。

method

`public Socket accept()` ：侦听并接受连接，返回一个新的Socket对象，用于和客户端实现通信。该方法会一直阻塞直到建立连接。

TCP通信图解

1. 【服务端】启动,创建ServerSocket对象，等待连接。

2. 【客户端】启动,创建Socket对象，请求连接。

3. 【服务端】接收连接,调用accept方法，并返回一个Socket对象。

4. 【客户端】Socket对象，获取OutputStream，向服务端写出数据。

5. 【服务端】Scoket对象，获取InputStream，读取客户端发送的数据。

# 基础加强

## Junit单元测试

步骤：
  
1. 定义一个测试类(测试用例)
   * 建议：
	   * 测试类名：被测试的类名Test        CalculatorTest
	   * 包名：xxx.xxx.xx.test        cn.itcast.test

2. 定义测试方法：可以独立运行
   * 建议：
	   * 方法名：test测试的方法名        testAdd()  
	   * 返回值：void
	   * 参数列表：空参

3. 给方法加@Test
4. 导入junit依赖环境

@Before
@After

## 反射

* 获取Class对象的方式：
  
  1. Class.forName("全类名")：将字节码文件加载进内存，返回Class对象
     
     - 多用于配置文件，将类名定义在配置文件中。读取文件，加载类
  
  2. 类名.class：通过类名的属性class获取
     
     - 多用于参数的传递
  
  3. 对象.getClass()：getClass()方法在Object类中定义着。
     
     - 多用于对象的获取字节码的方式

* 结论： 同一个字节码文件(*.class)在一次程序运行过程中，只会被加载一次，不论通过哪一种方式获取的Class对象都是同一个

* **Class对象**功能：
  
  * 获取功能：
    
    1. 获取成员变量们
       
       * `Field[] getFields()` ：获取所有public修饰的成员变量
       
       * `Field getField(String name)`   获取指定名称的 public修饰的成员变量
       
       * `Field[] getDeclaredFields()`  获取所有的成员变量，不考虑修饰符
       
       * `Field getDeclaredField(String name)  `
    
    2. 获取构造方法们
       
       * `Constructor<?>[] getConstructors()  `
       
       * `Constructor<T> getConstructor(类<?>... parameterTypes)  `
       
       * `Constructor<T> getDeclaredConstructor(类<?>... parameterTypes)  `
       
       * `Constructor<?>[] getDeclaredConstructors()  `
    
    3. 获取成员方法们：
       
       * `Method[] getMethods()  `
       
       * `Method getMethod(String name, 类<?>... parameterTypes)  `
       
       * `Method[] getDeclaredMethods()  `
       
       * `Method getDeclaredMethod(String name, 类<?>... parameterTypes)  `
    
    4. 获取全类名    
       
       * `String getName()`

* Field：成员变量
  
  * 操作：
    
    1. 设置值
       
       * `void set(Object obj, Object value)  `
    
    2. 获取值
       
       * `get(Object obj)`
    
    3. 忽略访问权限修饰符的安全检查
       
       * `setAccessible(true)`:暴力反射

* Constructor:构造方法
  
  * 创建对象：
    
    * T newInstance(Object... initargs)  
    
    * 如果使用空参数构造方法创建对象，操作可以简化：Class对象的newInstance方法

* Method：方法对象
  
  * 执行方法：
    
    * Object invoke(Object obj, Object... args)  
  
  * 获取方法名称：
    
    * String getName:获取方法名

## 注解

# MySQL

## 基础

SQL分类
- DDL(Data Definition Language)数据定义语言
	用来定义数据库对象：数据库，表，列等。关键字：`create`, `drop`,`alter` 等
- DML(Data Manipulation Language)数据操作语言
	用来对数据库中表的数据进行增删改。关键字：`insert`, `delete`, `update` 等
- DQL(Data Query Language)数据查询语言
	用来查询数据库中表的记录(数据)。关键字：`select`, `where` 等
- DCL(Data Control Language)数据控制语言(了解)
## 查询 约束 设计
### 查询

### 约束
- 概念： 对表中的数据进行限定，保证数据的正确性、有效性和完整性。
- 分类： 
	1. 主键约束：primary key
	2. 非空约束：not null
	3. 唯一约束：unique,值不能重复
	4. 外键约束：foreign key
	5. 非空约束：not null，值不能为null

- 非空约束：not null，值不能为null
1.  创建表时添加约束 
```sql
CREATE TABLE stu(
	 id INT,
	 NAME VARCHAR(20) NOT NULL -- name为非空
	);
```

2.  创建表完后，添加非空约束 
```sql
ALTER TABLE stu MODIFY NAME VARCHAR(20) NOT NULL;
```

3.  删除name的非空约束 
```sql
ALTER TABLE stu MODIFY NAME VARCHAR(20);
```

- 唯一约束：unique，值不能重复     
1. 创建表时，添加唯一约束 
 ```sql
CREATE TABLE stu(  id INT,  phone_number VARCHAR(20) UNIQUE -- 添加了唯一约束  );
    * 注意mysql中，**唯一约束限定的列的值可以有多个null**
    ```
2.  删除唯一约束     
```sql
ALTER TABLE stu DROP INDEX phone_number; 
```
3. 在创建表后，添加唯一约束     
```sql
ALTER TABLE stu MODIFY phone_number VARCHAR(20) UNIQUE;
```

- 主键约束：primary key 
1. 注意
	1. 含义：非空且唯一 
	2. 一张表只能有一个字段为主键 
	3. 主键就是表中记录的唯一标识 
2. 在创建表时，添加主键约束 
```sql
create table stu( id int primary key, name varchar(20)  );-- 给id添加主键约束
```
3. 删除主键  
```sql
-- 错误 alter table stu modify id int ;  
ALTER TABLE stu DROP PRIMARY KEY;   
```
4. 创建完表后，添加主键  
```sql
ALTER TABLE stu MODIFY id INT PRIMARY KEY;
```

* 自动增长：  
1.  概念：如果某一列是数值类型的，使用 `auto_increment` 可以来完成值得自动增长
2. 在创建表时，添加主键约束，并且完成主键自增长
```sql
create table stu(
 id int primary key auto_increment,-- 给id添加主键约束
 name varchar(20)
);
```   
3. 删除自动增长          
```sql
ALTER TABLE stu MODIFY id INT;         
```
5. 添加自动增长          
```sql
ALTER TABLE stu MODIFY id INT AUTO_INCREMENT;
```

* 外键约束 `foreign key` 让表于表产生关系，从而保证数据的正确性。
1. 在创建表时，可以添加外键
```sql
create table 表名( .... 外键列 constraint 外键名称 foreign key (外键列名称) references 主表名称(主表列名称) );
```
2. 删除外键
```sql
ALTER TABLE 表名 DROP FOREIGN KEY 外键名称;
```
4. 创建表之后，添加外键
```sql
ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段名称) REFERENCES 主表名称(主表列名称);
```

- 级联操作
1. 添加级联操作  
	语法：
	ALTER TABLE 表名 ADD CONSTRAINT 外键名称  
	FOREIGN KEY (外键字段名称) REFERENCES 主表名称(主表列名称) ON UPDATE CASCADE ON DELETE CASCADE ;
2. 分类：  
	1. 级联更新：ON UPDATE CASCADE  
	2. 级联删除：ON DELETE CASCADE
### 数据库设计
多表之间的关系
	1. 分类
		1. 一对一   人和身份证，一个人只有一个身份证，一个身份证只能对应一个人
		2. 一对多（多对一） 部门和员工 一个部门有多个员工，一个员工只能对应一个部门
		3. 多对多  一个学生可以选择很多门课程，一个课程也可以被很多学生选择

实现关系
- 一对多(多对一)：
    - 如：部门和员工
    - 实现方式：在多的一方建立外键，指向一的一方的主键。
- 多对多：
    - 如：学生和课程
    - 实现方式：多对多关系实现需要借助第三张中间表。中间表至少包含两个字段，这两个字段作为第三张表的外键，分别指向两张表的主键 使用联合主键
- 一对一(了解)：
    - 如：人和身份证
        - 实现方式：一对一关系实现，可以在任意一方添加唯一外键指向另一方的主键。


### 数据库设计的范式
  -   概念：设计数据库时，需要遵循的一些规范。要遵循后边的范式要求，必须先遵循前边的所有范式要求   
	设计关系数据库时，遵从不同的规范要求，设计出合理的关系型数据库，这些不同的规范要求被称为不同的范式，各种范式呈递次规范，越高的范式数据库冗余越小。  
	目前关系数据库有六种范式：第一范式（1NF）、第二范式（2NF）、第三范式（3NF）、巴斯-科德范式（BCNF）、第四范式(4NF）和第五范式（5NF，又称完美范式）。
    * 分类： 
    1. 第一范式（1NF）：每一列都是不可分割的原子数据项  
    2. 第二范式（2NF）：在1NF的基础上，非码属性必须完全依赖于码（在1NF基础上消除非主属性对主码的部分函数依赖）  
	    - 几个概念：  
	    1. 函数依赖：A-->B,如果通过A属性(属性组)的值，可以确定唯一B属性的值。则称B依赖于A  
			    例如：学号-->姓名。 （学号，课程名称） --> 分数 
	    2. 完全函数依赖：A-->B， 如果A是一个属性组，则B属性值得确定需要依赖于A属性组中所有的属性值。  
			    例如：（学号，课程名称） --> 分数 
	    3. 部分函数依赖：A-->B， 如果A是一个属性组，则B属性值得确定只需要依赖于A属性组中某一些值即可。  
			    例如：（学号，课程名称） -- > 姓名 
	    4. 传递函数依赖：A-->B, B -- >C . 如果通过A属性(属性组)的值，可以确定唯一B属性的值，在通过B属性（属性组）的值可以确定唯一C属性的值，则称 C 传递函数依赖于A  
			    例如：学号-->系名，系名-->系主任  
	    5. 码：如果在一张表中，一个属性或属性组，被其他所有属性所完全依赖，则称这个属性(属性组)为该表的码  
				    例如：该表中码为：（学号，课程名称）  
				    * 主属性：码属性组中的所有属性  
				    * 非主属性：除过码属性组的属性   
    3. 第三范式（3NF）：在2NF基础上，任何非主属性不依赖于其它非主属性（在2NF基础上消除传递依赖）

## 多表 事务

### 多表查询
笛卡尔积：

1. 内连接查询
	1. 隐式内连接
	2. 显式内连接
2. 外连接查询
		1. 左外连接
		2. 右外连接
3. 子查询

### 事务

1. 事务基本介绍
	1. 概念
		- 如果一个包含多个步骤的业务操作，被事务管理，那么这些操作要么同时成功，要么同时失败。
	2. 操作：
        1. 开启事务： start transaction;
        2. 回滚：rollback;
        3. 提交：commit;
    3. 例子：
		```sql
        CREATE TABLE account (
            id INT PRIMARY KEY AUTO_INCREMENT,
            NAME VARCHAR(10),
            balance DOUBLE
        );
        -- 添加数据
        INSERT INTO account (NAME, balance) VALUES ('zhangsan', 1000), ('lisi', 1000);
        SELECT * FROM account;
        UPDATE account SET balance = 1000;
        
        -- 张三给李四转账 500 元
        
        -- 0. 开启事务
        START TRANSACTION;
        -- 1. 张三账户 -500

        UPDATE account SET balance = balance - 500 WHERE NAME = 'zhangsan';
        -- 2. 李四账户 +500
        -- 出错了...
        UPDATE account SET balance = balance + 500 WHERE NAME = 'lisi';

        -- 发现执行没有问题，提交事务
        COMMIT;

        -- 发现出问题了，回滚事务
        ROLLBACK;
		```

	4. MySQL数据库中事务默认自动提交
        * 事务提交的两种方式：
            * 自动提交：
                * mysql就是自动提交的
                * 一条DML(增删改)语句会自动提交一次事务。
            * 手动提交：
                * Oracle 数据库默认是手动提交事务
                * 需要先开启事务，再提交
        * 修改事务的默认提交方式：
            * 查看事务的默认提交方式：`SELECT @@autocommit; -- 1 代表自动提交  0 代表手动提交`
            * 修改默认提交方式： `set @@autocommit = 0;`

2. 事务的四大特征
**ACID**，是指数据库管理系统（DBMS）在写入或更新资料的过程中，为保证**事务**（transaction）是正确可靠的，所必须具备的四个特性：
- 原子性（atomicity，或称不可分割性）、
- 一致性（consistency）、
- 隔离性（isolation，又称独立性）、
- 持久性（durability）。

3. 事务的隔离级别（了解）

**索引**


# JDBC

[JDBC笔记_清风徐来ya的博客-CSDN博客](https://blog.csdn.net/weixin_45775746/article/details/108890862)

Java DataBase Connectivity 

c3p0
德鲁伊
JDBCTemplate