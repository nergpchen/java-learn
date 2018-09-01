学习ArrayBlockingQueue的实现原理

成员变量

`/** The queued items  */`

`private final E[] items;`

 `/** items index for next take, poll or remove */`

`private int  takeIndex;`

`/** items index for next put, offer, or add. */`

`private int putIndex;`

`/** Number of items in the queue */`

`private int count;`

存储元素的是数组 



  
public void put\(E e\) throws InterruptedException {

    if \(e == null\) throw new NullPointerException\(\);

    final E\[\] items = this.items;

    final ReentrantLock lock = this.lock;

    lock.lockInterruptibly\(\);

    try {

        try {

            while \(count == items.length\)

                notFull.await\(\);

        } catch \(InterruptedException ie\) {

            notFull.signal\(\); // propagate to non-interrupted thread

            throw ie;

        }

        insert\(e\);

    } finally {

        lock.unlock\(\);

    }

}



使用 场景:

阻塞队列使用最经典的场景就是socket客户端数据的读取和解析，读取数据的线程不断将数据放入队列，然后解析线程不断从队列取数据解析。还有其他类似的场景，只要符合生产者-消费者模型的都可以使用阻塞队列。



