**Callable**

Callable和rRunnable差不多，两者都是为那些其实例可能被另一个线程执行的类而设计的，最主要的差别在于Runnable不会返回线程运算结果，Callable可以（假如线程需要返回运行结果）

**Future**

Future是一个接口表示异步计算的结果，它提供了检查计算是否完成的方法，以等待计算的完成，并获取计算的结果。Future提供了get\(\)、cancel\(\)、isCancel\(\)、isDone\(\)四种方法，表示Future有三种功能：

1、判断任务是否完成

2、中断任务

3、获取任务执行结果

**FutureTask**

FutureTask是Future的实现类，它提供了对Future的基本实现。可使用FutureTask包装Callable或Runnable对象，因为FutureTask实现了Runnable，所以也可以将FutureTask提交给Executor。

**使用方法**

Callable、Future、FutureTask一般都是和线程池配合使用的，因为线程池ThreadPoolExecutor的父类AbstractExecutorService提供了三种submit方法：

1、public Future&lt;?&gt; subit\(Runnable task\){...}

2、public &lt;T&gt; Future&lt;T&gt; submit&lt;Runnable task, T result&gt;{...}

3、public &lt;T&gt; Future&lt;T&gt; submit&lt;Callable&lt;T&gt; task&gt;{...}

第2个用得不多，第1个和第3个比较有用

  
`public static class CallableThread implements Callable<String>`

`{`

`    public String call() throws Exception`

`    {`

`        System.out.println("进入CallableThread的call()方法, 开始睡觉, 睡觉时间为" + System.currentTimeMillis());`

`        Thread.sleep(10000);`

`        return "123";`

`    }`

`}`

`    `

`public static void main(String[] args) throws Exception`

`{`

`    ExecutorService es = Executors.newCachedThreadPool();`

`    CallableThread ct = new CallableThread();`

`    Future<String> f = es.submit(ct);`

`    es.shutdown();`

`        `

`    Thread.sleep(5000);`

`    System.out.println("主线程等待5秒, 当前时间为" + System.currentTimeMillis());`

`        `

`    String str = f.get();`

`    System.out.println("Future已拿到数据, str = " + str + ", 当前时间为" + System.currentTimeMillis());`

`}`

