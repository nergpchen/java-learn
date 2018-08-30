读写锁 介绍：

读写锁维护了两个锁，一个是读操作相关的锁也成为共享锁，一个是写操作相关的锁 也称为排他锁。通过分离读锁和写锁，其并发性比一般排他锁有了很大提升。

ReadWriteLock接口的实现类-ReentrantReadWriteLock读写锁。

多个读锁之间不互斥，读锁与写锁互斥，写锁与写锁互斥（只要出现写操作的过程就是互斥的。）。



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

  




