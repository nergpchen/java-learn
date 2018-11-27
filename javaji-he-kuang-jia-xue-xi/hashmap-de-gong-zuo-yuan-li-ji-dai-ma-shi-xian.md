#### HashMap介绍:

HashMap是Map接口的实现,是非线程安全，影响HashMap性能有两个因素：初始容量和加载因子.

JDK1.8之前HashMap底层是数组和链表结合在一起使用也就是链表散列。

HashMap通过key的hashCode来计算hash值，当hashCode相同时，通过“拉链法”解决冲突。

相比于之前的版本，jdk1.8在解决哈希冲突时有了较大的变化，当链表长度大于阈值（默认为8）时，将链表转化为红黑树，以减少搜索时间。

#### HashMap因素:

\(1\)loadFactor加载因子

loadFactor加载因子是控制数组存放数据的疏密程度，loadFactor越趋近于1，那么 数组中存放的数据\(entry\)也就越多，也就越密，也就是会让链表的长度增加，load Factor越小，也就是趋近于0，

**loadFactor太大导致查找元素效率低，太小导致数组的利用率低，存放的数据会很分散。loadFactor的默认值为0.75f是官方给出的一个比较好的临界值**。

\(2\)threshold

**threshold = capacity \* loadFactor**，**当Size&gt;=threshold**的时候，那么就要考虑对数组的扩增了，也就是说，这个的意思就是 **衡量数组是否需要扩增的一个标准**。

HashMap数据结构:

HashMap由数据和链表组成，也就是一个链表散列。HashMap由数组组成，数组的成员是一条链。

存储实现:

```
//
```

```java
当key为null，调用putForNullKey方法，保存null与table第一个位置中，这是HashMap允许为null的原因
if
 (key == 
null
)

return
 putForNullKey(value);

//
计算key的hash值
int
 hash = hash(key.hashCode());                  ------(1
)

//
计算key hash 值在 table 数组中的位置
int
 i = indexFor(hash, table.length);             ------(2
)

//
从i出开始迭代 e,找到 key 保存的位置
for
 (Entry
<
K, V
>
 e = table[i]; e != 
null
; e =
 e.next) {
            Object k;

//
判断该条链上是否有hash值相同的(key相同)

//
若存在相同，则直接覆盖value，返回旧value
if
 (e.hash == hash 
&
&
 ((k = e.key) == key ||
 key.equals(k))) {
                V oldValue 
= e.value;    
//
旧值 = 新值

                e.value =
 value;
                e.recordAccess(
this
);

return
 oldValue;     
//
返回旧值
            }
        }

//
修改次数增加1

        modCount++
;

//
将key、value添加至i位置处
        addEntry(hash, key, value, i);

return
null
;
    }
```

2、 在看（1）、（2）处。这里是HashMap的精华所在。首先是hash方法，该方法为一个纯粹的数学计算，就是计算h的hash值。

```
static
int
 hash(
int
 h) {
        h 
^= (h 
>
>
>
 20) ^ (h 
>
>
>
 12
);

return
 h ^ (h 
>
>
>
 7) ^ (h 
>
>
>
 4
);
    }
```

```
  我们知道对于HashMap的table而言，数据分布需要均匀（最好每项都只有一个元素，这样就可以直接找到），不能太紧也不能太松，太紧会导致查询速度慢，太松则浪费空间。计算hash值后，怎么才能保证table元素分布均与呢？我们会想到取模，但是由于取模的消耗较大，HashMap是这样处理的：调用indexFor方法。
```

```
static
int
 indexFor(
int
 h, 
int
 length) {

return
 h 
&
 (length-1
);
    }
```

ashMap的底层数组长度总是2的n次方，在构造函数中存在：capacity &lt;&lt;= 1;这样做总是能够保证HashMap的底层数组长度为2的n次方。当length为2的n次方时，h&\(length - 1\)就相当于对length取模，而且速度比直接取模快得多，这是HashMap在速度上的一个优化。至于为什么是2的n次方下面解释。

```
  我们回到indexFor方法，该方法仅有一条语句：h&\(length - 1\)，这句话除了上面的取模运算外还有一个非常重要的责任：均匀分布table数据和充分利用空间。
```

所以说当length = 2^n时，不同的hash值发生碰撞的概率比较小，这样就会使得数据在table数组中分布较均匀，查询速度也较快。

```
  这里我们再来复习put的流程：当我们想一个HashMap中添加一对key-value时，系统首先会计算key的hash值，然后根据hash值确认在table中存储的位置。若该位置没有元素，则直接插入。否则迭代该处元素链表并依此比较其key的hash值。如果两个hash值相等且key值相等\(e.hash == hash && \(\(k = e.key\) == key \|\| key.equals\(k\)\)\),则用新的Entry的value覆盖原来节点的value。如果两个hash值相等但key值不等 ，则将该节点插入该链表的链头。具体的实现过程见addEntry方法，如下：
```

**二、扩容问题。**

当HashMap长度达到一个临界点的时候，必须扩容，扩容的大小是oldCapacity&lt;&lt;1,左移一位，就是新空间为旧空间的两倍.

这个时候还要重新计算每个元素的位置.因为元素在hash表中的定位是通过代码: \(n-1\)&hash计算出来的，n表示表的容量,是和表容量相关的，所以需要重新计算.

```
  随着HashMap中元素的数量越来越多，发生碰撞的概率就越来越大，所产生的链表长度就会越来越长，
  这样势必会影响HashMap的速度，为了保证HashMap的效率，系统必须要在某个临界点进行扩容处理。
  该临界点在当HashMap中元素的数量等于table数组长度\*加载因子。
  但是扩容是一个非常耗时的过程，因为它需要重新计算这些数据在新table数组中的位置并进行复制处理。
  所以如果我们已经预知HashMap中元素的个数，那么预设元素的个数能够有效的提高HashMap的性能。
```



