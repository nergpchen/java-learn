JDK1.8之前HashMap底层是数组和链表结合在一起使用也就是链表散列。

HashMap通过key的hashCode来计算hash值，当hashCode相同时，通过“拉链法”解决冲突。

相比于之前的版本，jdk1.8在解决哈希冲突时有了较大的变化，当链表长度大于阈值（默认为8）时，将链表转化为红黑树，以减少搜索时间。

#### HashMap因素:

\(1\)loadFactor加载因子

loadFactor加载因子是控制数组存放数据的疏密程度，loadFactor越趋近于1，那么 数组中存放的数据\(entry\)也就越多，也就越密，也就是会让链表的长度增加，load Factor越小，也就是趋近于0，

**loadFactor太大导致查找元素效率低，太小导致数组的利用率低，存放的数据会很分散。loadFactor的默认值为0.75f是官方给出的一个比较好的临界值**。

\(2\)threshold

**threshold = capacity \* loadFactor**，**当Size&gt;=threshold**的时候，那么就要考虑对数组的扩增了，也就是说，这个的意思就是 **衡量数组是否需要扩增的一个标准**。

作者：Snailclimb

链接：[https://juejin.im/post/5ab0568b5188255580020e56](https://juejin.im/post/5ab0568b5188255580020e56)



