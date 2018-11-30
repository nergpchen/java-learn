ReentrantLock

ReentrantLock是1.5后提供的可重入锁对象，可以实现和syn关键字一样的锁功能，只是在用法上会更加的灵活。

需要自己获取锁和释放锁，获取锁可以指定获取时间,在多少时间内获取锁，如果没有获取的话，就退出.

ReentrantLock可以指定公平锁还是非公平锁.

获取锁有几种方式:

lock\(\):一直等待到获取锁为止.

trylock\(\):不等待，立即返回,不管是否获取到.

lockInterruptibly\(\):可中断锁,线程在获取锁的过程中，如果被设置为中断，会先处理中断.



实现原理:

ReentrantLock实现有公平锁和非公平锁.   
NonfairSync用来实现非公平锁,FairSync用来实现公平锁.

NoffairSync获取锁的代码:

  
`/**`

` * Performs lock. Try immediate barge, backing up to normal`

` * acquire on failure.`

` */`

`finalvoid lock() {`

`if (compareAndSetState(0, 1))`

` setExclusiveOwnerThread(Thread.currentThread());`

`else`

` acquire(1);`

` }`

compareAndSetState\(0,1\)方法里调用 unsafe.compareAndSwapInt\(\)来进行获取锁,逻辑是把原来的state=0值修改为1,如果修改成功，则获得控制权.如果失败，则调用acquire\(1\)方法来获取锁. acquire方法会先判断state=0,如果为0，则表示当前锁可以获取，如果不为 0，则锁被别人占用，则进入等待队列.



  


  


