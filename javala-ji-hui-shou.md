#### 什么是垃圾回收

GC是java垃圾回收器对识别正在使用的对象和未使用的对象，并且删除未使用的对象.

那么Java是在什么时候,怎么判断需要回收的对象,怎么进行回收的?

#### 什么时候回收？

最后总结一下什么时候会触发一次GC，个人经验看，有三种场景会触发GC：

1、第一种场景应该很明显，当年轻代或者老年代满了，Java虚拟机无法再为新的对象分配内存空间了，那么Java虚拟机就会触发一次GC去回收掉那些已经不会再被使用到的对象

2、手动调用System.gc\(\)方法，通常这样会触发一次的Full GC以及至少一次的Minor GC

3、程序运行的时候有一条低优先级的GC线程，它是一条守护线程，当这条线程处于运行状态的时候，自然就触发了一次GC了。这点也很好证明，不过要用到WeakReference的知识，后面写WeakReference的时候会专门讲到这个。

  


#### 那些内存需要回收?

GC动作发生之前，需要确定堆内存中哪些对象是存活的，一般有两种方法：引用计数法和可达性分析法。

1. 引用计数法：通过测试，引用计数法实现简单，判定高效，但不能解决对象之间相互引用的问题。

2.  可达性分析法：通过一系列的GC Roots的对象作为起点,从这些节点开始往下搜,搜索路径称为'引用链',当一个对象到 GC Roots 没有任何引用链时，意味着该对象可以被回收。

#### 怎么回收?

#### 3.1 标记-清除算法

算法分为“标记”和“清除”阶段：首先标记出所有需要回收的对象，在标记完成后统一回收所有被标记的对象。它是最基础的收集算法，会带来两个明显的问题；1：效率问题和2：空间问题（标记清除后会产生大量不连续的碎片）![](https://mmbiz.qpic.cn/mmbiz_png/hvUCbRic69sDOMkMYwE1nhEJFZN46xicicaw1iaSkaHmorye79qTka8Ew8mY4zkvG80Dx4DgdxpwX6osZZQ13bgC4g/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

### 3.2 复制算法

为了解决效率问题，“复制”收集算法出现了。它可以将内存分为大小相同的两块，每次使用其中的一块。当这一块的内存使用完后，就将还存活的对象复制到另一块去，然后再把使用的空间一次清理掉。这样就使每次的内存回收都是对内存区间的一半进行回收。

![](https://mmbiz.qpic.cn/mmbiz_png/hvUCbRic69sDOMkMYwE1nhEJFZN46xicicaSia9w6GX34d7VYicWgyec1wiaF47ibicvibkLZBfn6XVvibcnI6XMZaw2ZBCw/640?wx_fmt=png&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

#### 垃圾回收器

#### 



引用:[https://mp.weixin.qq.com/s?\_\_biz=MzU4NDQ4MzU5OA==∣=2247483914&idx=1&sn=9aa157d4a1570962c39783cdeec7e539&chksm=fd98546bcaefdd7d9f61cd356e5584e56b64e234c3a403ed93cb6d4dde07a505e3000fd0c427&scene=21\#wechat\_redirect](https://mp.weixin.qq.com/s?__biz=MzU4NDQ4MzU5OA==&mid=2247483914&idx=1&sn=9aa157d4a1570962c39783cdeec7e539&chksm=fd98546bcaefdd7d9f61cd356e5584e56b64e234c3a403ed93cb6d4dde07a505e3000fd0c427&scene=21#wechat_redirect)

