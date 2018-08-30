一什么 是线程池？

线程池是用来集中管理线程的启动、执行,提供系统的效率，因为每启动一个线程都会有相应的性能开支，如果并发的线程数量很多，频繁的创建线程会降低系统的效率，那么我们可以设想当启动一个线程执行完任务后，可以继续执行其他的任务

当要执行任务的时候，我们像线程池请求线程，当有空闲线程的时候，就会分配一个线程来执行任务。

线程池经常应用在多线程服务器上。每个通过网络到达服务器的连接都被包装成一个任务并且传递给线程池。线程池的线程会并发的处理连接上的请求。

二好处：

使用线程池可以对线程进行统一的分配，调优和监控,提供系统资源的使用效率.

三：怎么使用？

1.创建固定数目线程的线程池。  
public static ExecutorService newFixedThreadPool\(int nThreads\)

2.创建一个可缓存的线程池，调用execute将重用以前构造的线程（如果线程可用）。如果现有线程没有可用的，则创建一个新线 程并添加到池中。终止并从缓存中移除那些已有 60 秒钟未被使用的线程。

public static ExecutorService newCachedThreadPool\(\)

3.创建一个单线程化的Executor。  
public static ExecutorService newSingleThreadExecutor\(\)

4.创建一个支持定时及周期性的任务执行的线程池，多数情况下可用来替代Timer类。  
public static ScheduledExecutorService newScheduledThreadPool\(int corePoolSize\)

**newCachedThreadPool\(\)**

* 缓存型池子，先查看池中有没有以前建立的线程，如果有，就 reuse 如果没有，就建一个新的线程加入池中
* 缓存型池子通常用于执行一些生存期很短的异步型任务 因此在一些面向连接的 daemon 型 SERVER 中用得不多。但对于生存期短的异步任务，它是 Executor 的首选。
* 能 reuse 的线程，必须是 timeout IDLE 内的池中线程，缺省 timeout 是 60s,超过这个 IDLE 时长，线程实例将被终止及移出池。

  > 注意，放入 CachedThreadPool 的线程不必担心其结束，超过 TIMEOUT 不活动，其会自动被终止。

**newFixedThreadPool\(int\)**

* newFixedThreadPool 与 cacheThreadPool 差不多，也是能 reuse 就用，但不能随时建新的线程。
* 其独特之处:任意时间点，最多只能有固定数目的活动线程存在，此时如果有新的线程要建立，只能放在另外的队列中等待，直到当前的线程中某个线程终止直接被移出池子。
* 和 cacheThreadPool 不同，FixedThreadPool 没有 IDLE 机制（可能也有，但既然文档没提，肯定非常长，类似依赖上层的 TCP 或 UDP IDLE 机制之类的），所以 FixedThreadPool 多数针对一些很稳定很固定的正规并发线程，多用于服务器。
* 从方法的源代码看，cache池和fixed 池调用的是同一个底层 池，只不过参数不同:
  * fixed 池线程数固定，并且是0秒IDLE（无IDLE）。
  * cache 池线程数支持 0-Integer.MAX\_VALUE\(显然完全没考虑主机的资源承受能力），60 秒 IDLE 。

**newScheduledThreadPool\(int\)**

* 调度型线程池
* 这个池子里的线程可以按 schedule 依次 delay 执行，或周期执行

**SingleThreadExecutor\(\)**

* 单例线程，任意时间池中只能有一个线程
* 用的是和 cache 池和 fixed 池相同的底层池，但线程数目是 1-1,0 秒 IDLE（无 IDLE）

一般来说，CachedTheadPool 在程序执行过程中通常会创建与所需数量相同的线程，然后在它回收旧线程时停止创建新线程，因此它是合理的 Executor 的首选，只有当这种方式会引发问题时（比如需要大量长时间面向连接的线程时），才需要考虑用 FixedThreadPool。

