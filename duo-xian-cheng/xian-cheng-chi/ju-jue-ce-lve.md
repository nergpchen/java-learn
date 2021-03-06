#### 任务源源不断的过来，而我们的系统又处理不过来的时候，我们要采取的策略是拒绝服务。RejectedExecutionHandler接口提供了拒绝任务处理的自定义方法的机会。

#### 在ThreadPoolExecutor中已经包含四种处理策略。

1. CallerRunsPolicy：线程调用运行该任务的 execute 本身。此策略提供简单的反馈控制机制，能够减缓新任务的提交速度。

   public void rejectedExecution\(Runnable r, ThreadPoolExecutor e\) { if \(!e.isShutdown\(\)\) { r.run\(\); }}

   这个策略显然不想放弃执行任务。但是由于池中已经没有任何资源了，那么就直接使用调用该execute的线程本身来执行。（开始我总不想丢弃任务的执行，但是对某些应用场景来讲，很有可能造成当前线程也被阻塞。如果所有线程都是不能执行的，很可能导致程序没法继续跑了。需要视业务情景而定吧。）

2. AbortPolicy：处理程序遭到拒绝将抛出运行时 RejectedExecutionException

   public void rejectedExecution\(Runnable r, ThreadPoolExecutor e\) {throw new RejectedExecutionException\(\);}

   这种策略直接抛出异常，丢弃任务。（jdk默认策略，队列满并线程满时直接拒绝添加新任务，并抛出异常，所以说有时候放弃也是一种勇气，为了保证后续任务的正常进行，丢弃一些也是可以接收的，记得做好记录）

3. DiscardPolicy：不能执行的任务将被删除

   public void rejectedExecution\(Runnable r, ThreadPoolExecutor e\) {}

   这种策略和AbortPolicy几乎一样，也是丢弃任务，只不过他不抛出异常。

4. DiscardOldestPolicy：如果执行程序尚未关闭，则位于工作队列头部的任务将被删除，然后重试执行程序（如果再次失败，则重复此过程）

   public void rejectedExecution\(Runnable r, ThreadPoolExecutor e\) { if \(!e.isShutdown\(\)\) {e.getQueue\(\).poll\(\);e.execute\(r\); }}

   该策略就稍微复杂一些，在pool没有关闭的前提下首先丢掉缓存在队列中的最早的任务，然后重新尝试运行该任务。这个策略需要适当小心。



