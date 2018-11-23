CountDownLatch

CountDownLatch是用来 多个线程工作的时候，1个线程等其他线程完成的时候再开始运行。

CountDownLatch主要提供的机制是当多个（具体数量等于初始化CountDownLatch时count参数的值）线程都达到了预期状态或完成预期工作时触发事件，其他线程可以等待这个事件来触发自己的后续工作。值得注意的是，CountDownLatch是可以唤醒多个等待的线程的。

用法

A线程调用 countDown.countDown\(\)  方法，会释放共享锁,计数器减一.

B线程调用countDown.await\(\)用来获取共享锁，当计算器为0的时候，成功获取共享锁，执行B线程

用法:

看CountDonwLatch的应用场景可以用于多个线程工作的情况，比如要分别统计C D F G盘的文件数，可以启动四个线程分别统计文件数，在4个线程都结束的时候，由另外一个线程来统计文件.



