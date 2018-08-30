Lock锁分为：

**公平锁**和**非公平锁**



公平锁表示线程获取锁的顺序是按照线程加锁的顺序来分配的，即先来先得的**FIFO先进先出顺序**。

而非公平锁就是一种获取锁的抢占机制，是

**随机获取**锁的，和公平锁不一样的就是先来的不一定先的到锁，这样可能造成某些线程一直拿不到锁，结果也就是不公平的了
