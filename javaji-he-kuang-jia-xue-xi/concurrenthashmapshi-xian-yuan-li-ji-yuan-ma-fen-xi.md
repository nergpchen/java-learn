#### ConcurrentHashMap实现原理

HashTable性能差主要是由于所有操作需要竞争同一把锁，而如果容器中有多把锁，每一把锁锁一段数据，这样在多线程访问时不同段的数据时，就不会存在锁竞争了，这样便可以有效地提高并发效率。这就是ConcurrentHashMap所采用的"**分段锁**"思想。  


源码分析:

concurrentHashMap的主干是个Segment数组用来支持分段锁:

final Segment&lt;K,V&gt;\[\] segments;

 



