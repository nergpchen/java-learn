读写锁 介绍：

在程序中，读写是非常常见的一种操作 ,如果在读的时候是不会有安全问题的 ，所以在JDK中提供了一种读写锁ReentrantReadWriteLock，使用它可以加快运行效率。

读写锁表示两个锁，一个是读操作相关的锁，称为**共享锁**；另一个是写操作相关的锁，称为**排他锁**。我把这两个操作理解为三句话：

1、读和读之间不互斥，因为读操作不会有线程安全问题

2、写和写之间互斥，避免一个写操作影响另外一个写操作，引发线程安全问题

3、读和写之间互斥，避免读操作的时候写操作修改了内容，引发线程安全问题

总结起来就是，**多个Thread可以同时进行读取操作，但是同一时刻只允许一个Thread进行写入操作**。



### 3.2 ReentrantReadWriteLock的特性与常见方法 {#32-reentrantreadwritelock的特性与常见方法}

**ReentrantReadWriteLock的特性：**

| 特性 | 说明 |
| :--- | :--- |
| 公平性选择 | 支持非公平（默认）和公平的锁获取方式，吞吐量上来看还是非公平优于公平 |
| 重进入 | 该锁支持重进入，以读写线程为例：读线程在获取了读锁之后，能够再次获取读锁。而写线程在获取了写锁之后能够再次获取写锁也能够同时获取读锁 |
| 锁降级 | 遵循获取写锁、获取读锁再释放写锁的次序，写锁能够降级称为读锁 |

**ReentrantReadWriteLock常见方法：**  
构造方法

| 方法名称 | 描述 |
| :--- | :--- |
| ReentrantReadWriteLock\(\) | 创建一个 ReentrantReadWriteLock\(\)的实例 |
| ReentrantReadWriteLock\(boolean fair\) | 创建一个特定锁类型（公平锁/非公平锁）的ReentrantReadWriteLock的实例 |

常见方法：  
和ReentrantLock类 类似这里就不列举了。

### 3.3 ReentrantReadWriteLock的使用 {#33-reentrantreadwritelock的使用}

1.**读读共享**

两个线程同时运行read方法，你会发现两个线程可以同时或者说是几乎同时运行lock\(\)方法后面的代码，输出的两句话显示的时间一样。这样提高了程序的运行效率。

```
private
 ReentrantReadWriteLock lock = 
new
 ReentrantReadWriteLock();


public
void
read
() {

try
 {

try
 {
                lock.readLock().lock();
                System.out.println(
"获得读锁"
 + Thread.currentThread().getName()
                        + 
" "
 + System.currentTimeMillis());
                Thread.sleep(
10000
);
            } 
finally
 {
                lock.readLock().unlock();
            }
        } 
catch
 (InterruptedException e) {

// TODO Auto-generated catch block

            e.printStackTrace();
        }
    }
```



