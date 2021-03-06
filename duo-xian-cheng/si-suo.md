死锁

#### 什么是死锁?

  例如，如果线程1锁住了A，然后尝试对B进行加锁，同时线程2已经锁住了B，接着尝试对A进行加锁，这时死锁就发生了。线程1永远得不到B，线程2也永远得不到A，并且它们永远也不会知道发生了这样的事情。为了得到彼此的对象（A和B），它们将永远阻塞下去。这种情况就是一个死锁。

怎么产生的？

  一个代码会发生死锁，并不表示每次都会发生，通常在高并发的情况下发生死锁？

怎么避免死锁

首先 jps获得当前Java虚拟机进程的pid

![](https://images2015.cnblogs.com/blog/801753/201510/801753-20151003182242605-2032401948.png)

其次 运行Jstack pid 打印堆栈日志



#### 怎么避免呢？

既然可能产生死锁，那么接下来，讲一下如何避免死锁。

1、让程序每次至多只能获得一个锁。当然，在多线程环境下，这种情况通常并不现实

2、设计时考虑清楚锁的顺序，尽量减少嵌在的加锁交互数量

3、既然死锁的产生是两个线程无限等待对方持有的锁，那么只要等待时间有个上限不就好了。当然synchronized不具备这个功能，但是我们可以使用Lock类中的tryLock方法去尝试获取锁，这个方法可以指定一个超时时限，在等待超过该时限之后变回返回一个失败信息.

#### 数据库的死锁 {#DatabaseDeadlock}

更加复杂的死锁场景发生在数据库事务中。一个数据库事务可能由多条SQL更新请求组成。当在一个事务中更新一条记录，这条记录就会被锁住避免其他事务的更新请求，直到第一个事务结束。同一个事务中每一个更新请求都可能会锁住一些记录。

当多个事务同时需要对一些相同的记录做更新操作时，就很有可能发生死锁，例如：

```
Transaction 1, request 1, locks record 1 for update
Transaction 2, request 1, locks record 2 for update
Transaction 1, request 2, tries to lock record 2 for update.
Transaction 2, request 2, tries to lock record 1 for update.

```

因为锁发生在不同的请求中，并且对于一个事务来说不可能提前知道所有它需要的锁，因此很难检测和避免数据库事务中的死锁。

  




