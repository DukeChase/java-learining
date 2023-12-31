# 进程管理

## 2.1 进程与线程

## 2.2 处理机调度

### 调度的层次

作业调度

中级调度

进程调度

### 进程调度方式：

剥夺式调度方式
非剥夺式调度方式

调度基本准则
- CPU利用率
- 系统吞吐量
- 周转时间 
- 周转时间 = 作业完成时间-作业提交时间  
- 平均周转时间 = $\frac{（作业1的周转时间+作业2的周转时间+···作业n的周转时间）}{n}$
- 带权周转时间 = $\frac{作业周转时间}{作业实际运行时间}$
- 平均带权周转时间 = $\frac{(作业1的带权周转时间+···作业2的带权周转时间)}{n}$
- 等待时间 
- 指进程处于等处理机状态的时间之和
- 响应时间
- 指用户请求提交到系统首次产生响应所用的时间

### 典型的调度算法

- 先来先服务
- 短作业优先
- 优先级调度
- 高响应比优先调度算法
- 时间片轮转调度算法
- 多级反馈队列调度算法

## 2.3 进程同步

进程执行的先后顺序
- **临界资源**  将一次仅允许一个进程使用的资源称为**临界资源**
- 同步 直接制约关系
- 互斥 间接制约关系

1. 空闲让进
2. 忙则等待
3. 有限等待
4. 让权等待

实现临界区互斥的基本方法

1. 软件实现方法	
2. 硬件实现方法
    - 中断屏蔽方法
    - 硬件指令方法
### 2.3.3 信号量
信号量机制是一种功能较强的机制，可用来解决互斥和同步的问题，他只能被两个标准的原语`wait(S)`和`signal(S)`访问，可标记为`P操作`和`V操作`。
 
1. 整型信号量
2. 记录型信号量
3. 利用信号量实现同步
4. 利用信号量实现进程互斥
5. 利用信号量实现前驱关系

## 2.4 死锁

概念

原因

四个必要条件

* 互斥条件    进程对所分配的资源进行排他性控制

* 不剥夺条件  进程所获得的资源在未使用完之前，不被其他进程剥夺

* 请求并保持  进程已经保持至少一个资源，有提出新的资源请求，而该资源已被其他进程占有，此时请求进程被阻塞，但对自己获得的资源保持不放。

* 循环等待    存在一种进程资源的循环等待链，链中的每个进程已获得的资源同时被链中下一个进程所请求。

处理策略

预防：破坏四个必要条件之一

避免：

分配资源前计算安全性，

银行家算法

检测及解除

# 内存管理
