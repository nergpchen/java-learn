## 基础知识 {#2基础知识}

* [Java](http://lib.csdn.net/base/java)基本类型哪些，所占字节和范围

* Set、List、Map的区别和联系

* 什么时候使用Hashmap

* 什么时候使用Linkedhashmap、Concurrenthashmap、Weakhashmap

* 哪些集合类是线程安全的

* 为什么Set、List、map不实现Cloneable和Serializable接口

* Concurrenthashmap的实现，1.7和1.8的实现

* Arrays.sort的实现

* 什么时候使用CopyOnArrayList

* volatile的使用

* synchronied的使用

* reentrantlock的实现和Synchronied的区别

* CAS的实现原理以及问题

* AQS的实现原理

* 接口和抽象类的区别，什么时候使用

* 类加载机制的步骤，每一步做了什么，static和final修改的成员变量的加载时机

* 双亲委派模型

* 反射机制：反射动态擦除泛型、反射动态调用方法等

* 动态绑定：父类引用指向子类对象

* JVM内存管理机制：有哪些区域，每个区域做了什么

* JVM垃圾回收机制：垃圾回收算法 垃圾回收器 垃圾回收策略

* jvm参数的设置和jvm调优

* 什么情况产生年轻代内存溢出、什么情况产生年老代内存溢出

* 内部类：静态内部类和匿名内部类的使用和区别

* [Redis](http://lib.csdn.net/base/redis)和memcached：什么时候选择[redis](http://lib.csdn.net/base/redis)，什么时候选择memcached，内存模型和存储策略是什么样的

* [MySQL](http://lib.csdn.net/base/mysql)的基本操作 主从[数据库](http://lib.csdn.net/base/mysql)一致性维护

* [mysql](http://lib.csdn.net/base/mysql)的优化策略有哪些

* mysql索引的实现 B+树的实现原理

* 什么情况索引不会命中，会造成全表扫描

* java中bio nio aio的区别和联系

* 为什么bio是阻塞的 nio是非阻塞的 nio是模型是什么样的

* [Java ](http://lib.csdn.net/base/java)io的整体[架构](http://lib.csdn.net/base/architecture)和使用的设计模式

* Reactor模型和Proactor模型

* http请求报文结构和内容

* http三次握手和四次挥手

* rpc相关：如何设计一个rpc框架，从io模型 传输协议 序列化方式综合考虑

* [Linux](http://lib.csdn.net/base/linux)命令 统计，排序，前几问题等

* StringBuff 和StringBuilder的实现，底层实现是通过byte数据，外加数组的拷贝来实现的

* cas操作的使用

* 内存缓存和数据库的一致性同步实现

* [微服务](http://lib.csdn.net/base/microservice)的优缺点

* 线程池的参数问题

* ip问题 如何判断ip是否在多个ip段中

* 判断数组两个中任意两个数之和是否为给定的值

* 乐观锁和悲观锁的实现

* synchronized实现原理

* 你在项目中遇到的困难和怎么解决的

* 你在项目中完成的比较出色的亮点

* 消息队列广播模式和发布/订阅模式的区别

* 生产者消费者代码实现

* 死锁代码实现

* 线程池：参数，每个参数的作用，几种不同线程池的比较，阻塞队列的使用，拒绝策略

* Future和ListenableFuture 异步回调相关

* 算法相关：判断能否从数组中找出两个数字和为给定值，随机生成1~10000不重复并放入数组，求数组的子数组的最大和，二分查找算法的实现及其时间复杂计算

一、Java基础

  


1.String类为什么是final的。

  


2.HashMap的源码，实现原理，底层结构。

  


3.反射中，Class.forName和classloader的区别

  


4.session和cookie的区别和联系，session的生命周期，多个服务部署时session管理。

  


5.Java中的队列都有哪些，有什么区别。

  


6.Java的内存模型以及GC算法

  


7.Java7、Java8的新特性\(baidu问的,好BT\)

  


8.Java数组和链表两种结构的操作效率，在哪些情况下\(从开头开始，从结尾开始，从中间开始\)，哪些操作\(插入，查找，删除\)的效率高

  


9.Java内存泄露的问题调查定位：jmap，jstack的使用等等

