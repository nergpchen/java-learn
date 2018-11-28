#### Java8 ConcurrentHashMap实现原理

在1.8中,Concurrent采用Node数组+ 链表+TreeNode来存储元素，这是和1.7完全不同，1.7是采用Segment数组+ HashEntry来存储元素.当数组上的链表元素个数到8个的时候，会自动转换成二叉树结构，在这些位置进行查找的时候可以降低时间复杂度为**O\(logN\)**

。

在并发技术上,在put的时候，使用synchronized锁住元素保障线程安全或者调用Unsafe进行元素替换.



#### Java7 ConcurrentHashMap实现原理



HashTable性能差主要是由于所有操作需要竞争同一把锁，而如果容器中有多把锁，每一把锁锁一段数据，这样在多线程访问时不同段的数据时，就不会存在锁竞争了，这样便可以有效地提高并发效率。这就是ConcurrentHashMap所采用的"**分段锁**"思想。

Segment对象用RetreenLock锁来保证线程安全

源码分析:

concurrentHashMap的主干是个Segment数组用来支持分段锁:

final Segment&lt;K,V&gt;\[\] segments;

引用:[https://blog.csdn.net/moakun/article/details/80231067](https://blog.csdn.net/moakun/article/details/80231067)

