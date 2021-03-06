#### CAS介绍

CAS的全称是Compare And Swap 即比较和交换，其算法核心思想如下

执行函数：CAS\(V,E,N\) 

 其包含3个参数

1.  V表示需要读写的内存位置

   2.  E表示进行比较的预期原值

   3.  N表示打算写入的新值

如果内存位置的值与预期原值相匹配，那么处理器会自动将该位置值更新为新值 。否则，处理器不做任何操作.

#### 鲜为人知的指针: Unsafe类

      Unsafe类存在于`sun.misc`包中，其内部方法操作可以像C的指针一样直接操作内存，单从名称看来就可以知道该类是非安全的，毕竟Unsafe拥有着类似于C的指针操作，因此总是不应该首先使用Unsafe类，Java官方也不建议直接使用的Unsafe类，但我们还是很有必要了解该类，因为Java中CAS操作的执行依赖于Unsafe类的方法，注意Unsafe类中的所有方法都是**native修饰**的，也就是说Unsafe类中的方法都直接调用操作系统底层资源执行相应任务

  


