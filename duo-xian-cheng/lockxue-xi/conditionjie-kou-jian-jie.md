### 2.2 Condition接口简介 {#22-condition接口简介}

我们通过之前的学习知道了：synchronized关键字与wait\(\)和notify/notifyAll\(\)方法相结合可以实现等待/通知机制，ReentrantLock类当然也可以实现，但是需要借助于Condition接口与newCondition\(\) 方法。Condition是JDK1.5之后才有的，它具有很好的灵活性，比如可以实现多路通知功能也就是在一个Lock对象中可以创建多个Condition实例（即对象监视器），线程对象可以注册在指定的Condition中，从而可以有选择性的进行线程通知，在调度线程上更加灵活。

在使用notify/notifyAll\(\)方法进行通知时，被通知的线程是有JVM选择的，使用ReentrantLock类结合Condition实例可以实现“选择性通知”，这个功能非常重要，而且是Condition接口默认提供的。

而synchronized关键字就相当于整个Lock对象中只有一个Condition实例，所有的线程都注册在它一个身上。如果执行notifyAll\(\)方法的话就会通知所有处于等待状态的线程这样会造成很大的效率问题，而Condition实例的signalAll\(\)方法 只会唤醒注册在该Condition实例中的所有等待线程

**Condition接口的常见方法：**

| 方法名称 | 描述 |
| :--- | :--- |
| void await\(\) | 相当于Object类的wait方法 |
| boolean await\(long time, TimeUnit unit\) | 相当于Object类的wait\(long timeout\)方法 |
| signal\(\) | 相当于Object类的notify方法 |
| signalAll\(\) | 相当于Object类的notifyAll方法 |

  


