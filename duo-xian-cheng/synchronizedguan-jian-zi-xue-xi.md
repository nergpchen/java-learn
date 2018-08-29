#### 一 介绍

synchronized1.6之前是“重量级锁”。但是，在JavaSE 1.6之后引入的偏向锁和轻量级锁进行了优化,变得没有那么重.

二实现 原理

Java中每一个对象都可以作为锁，这是synchronized实现同步的基础：

1. 普通同步方法，锁是当前实例对象
2. 静态同步方法，锁是当前类的class对象
3. 同步方法块，锁是括号里面的对象

`public class`

`SynchronizedTest {`

`public synchronized void test1(){`

`}`

`public void test2(){`

 `synchronized(this){ }`

    `}`

`}`

同步代码块：monitorenter指令插入到同步代码块的开始位置，monitorexit指令插入到同步代码块的结束位置，JVM需要保证每一个monitorenter都有一个monitorexit与之相对应。任何对象都有一个monitor与之相关联，当且一个monitor被持有之后，他将处于锁定状态。线程执行到monitorenter指令时，将会尝试获取对象所对应的monitor所有权，即尝试获取对象的锁；

  


同步方法：synchronized方法则会被翻译成普通的方法调用和返回指令如:invokevirtual、areturn指令，在VM字节码层面并没有任何特别的指令来实现被synchronized修饰的方法，而是在Class文件的方法表中将该方法的access\_flags字段中的synchronized标志位置1，表示该方法是同步方法并使用调用该方法的对象或该方法所属的Class在JVM的内部对象表示Klass做为锁对象。\(摘自：

[http://www.cnblogs.com/javaminer/p/3889023.html](http://www.cnblogs.com/javaminer/p/3889023.html)

\)  


### 二 synchronized锁重入 {#六-synchronized锁重入}

“可重入锁”概念是：自己可以再次获取自己的内部锁。比如一个线程获得了某个对象的锁，此时这个对象锁还没有释放，当其再次想要获取这个对象的锁的时候还是可以获取的，如果不可锁重入的话，就会造成死锁。

### 三 同步不具有继承性 {#七-同步不具有继承性}

如果父类有一个带synchronized关键字的方法，子类继承并重写了这个方法。  
但是同步不能继承，所以还是需要在子类方法中添加synchronized关键字.

### 四 synchronized（this）同步代码块的使用 {#二-synchronizedthis同步代码块的使用}

当一个线程访问一个对象的synchronized同步代码块时，另一个线程任然可以访问该对象非synchronized同步代码块.

对象监视器  






