JDK 1.5以后，Java提供一个线程池ThreadPoolExecutor类。下面从构造函数来分析一下这个线程池的使用方法。

  


public ThreadPoolExecutor\(int corePoolSize, int maximumPoolSize, long keepAliveTime, TimeUnit unit, BlockingQueue workQueue, ThreadFactory threadFactory, RejectedExecutionHandler handler\);

  


参数名、说明：

  


\* corePoolSize 线程池维护线程的最少数量

  


\* maximumPoolSize 线程池维护线程的最大数量

  


\* keepAliveTime 线程池维护线程所允许的空闲时间

  


\* workQueue 任务队列，用来存放我们所定义的任务处理线程

  


\* threadFactory 线程创建工厂

  


\* handler 线程池对拒绝任务的处理策略

  


ThreadPoolExecutor将根据corePoolSize和maximumPoolSize设置的边界自动调整池大小。当新任务在方法execute\(Runnable\) 中提交时， 如果运行的线程少于corePoolSize，则创建新线程来处理请求。

  


如果正在运行的线程等于corePoolSize时，ThreadPoolExecutor优先往队列中添加任务，直到队列满了，并且没有空闲线程时才创建新的线程。如果设置的corePoolSize 和 maximumPoolSize 相同，则创建了固定大小的线程池。

  


keepAliveTime：当线程数达到maximumPoolSize时，经过某段时间，发现多出的线程出于空闲状态，就进行线程的回收。keepAliveTime就是线程池内最大的空闲时间。

  


workQueue：当核心线程不能都在处理任务时，新进任务被放在Queue里

