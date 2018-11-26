java集合框架思考学习

如何学习集合框架?

java集合框架是什么？

java集合框架是对数据结构和算法用法的实现的封装，包括map、set、list、tree、array、hastabel等其他的集合类型.

在C++中类似的是标准模板库.

根据

[维基百科](http://en.wikipedia.org/wiki/Java_collections_framework)

了解到,JCF框架是从1.2版本才出现的，主要是java大牛

[Joshua\_Bloch](http://en.wikipedia.org/wiki/Joshua_Bloch)

设计开发,这个人也就是Google首席工程软件师,同时也是《

Effective Java

》的作者.

java集合框架解决了什么问题？

我们在程序设计中，需要处理的数据分为基本数据和复合数据，后者常见的组织形式就是类。类对象通常是以动态形式分配的。

譬如在内存空间分配new一个对象。我们在处理的时候，面对的不是单个基本对象或者单个基本类，而是多个数据类型，那么用什么来处理多个对象呢？就是数组。数组也是一种实现集合的数据结构，可以存放多个数据。

数组的优点

是通过下标检索元素非常方便，但是

缺点

也是显而易见：空间固定而且不能够稳定增长。所以不是解决一切集合问题的工具。我们可能需要一些新的数据结构的工具来处理集合，其实数组本身就是一种线下有序的数据结构。

数据结构的基础就是集合论.

为什么这么说呢

？上面说过，现在我们要研究的不是单个的基 本类型或对象，多个对象的整体不就是集合吗？从OO的角度上看，集合也是一种对象，但它是一种特殊的对象：对象的容器（注意，我们这里没有继续讨论基本类 型的集合，因为基本类型和存储分配方式与对象有着本质的差别）。集合论的一个根本问题就是：给定一个元素，集合必须能够回答该元素是或者不是属于这个集 合。还有一个问题也很重要，就是：如果元素是属于一个集合，那该元素在集合中的地位应该是唯一的，或者说它是

唯一确定

的。当然还有其它问题，譬如查找、遍历、排序等等，这和具体的集合类型相关，后面将会讲到。

JCF框架的结构介绍和一些基本概念

一：结构

下面这张图是常见的JCF框架的结构图

![](//note.youdao.com/src/C14EE12B04734B8F931F9075C7BCA10C)

上面图看起来非常的多，比较乱，其实很多的软件的一个模块的设计都比这复杂。

上面黑色背景的表示是接口，我们可以看到

java提供了以下接口

第一级：Collection、

二级：

List接口、Set接口、Map接口

三级：

RandomAcess、SortedSet、SortedMap

如果我们学过数学或者没有忘记的话，应该知道,List、Set、Map其实是对数学集合概念的抽象和封装。

我们把

[Collection](http://java.sun.com/j2se/1.4.2/docs/api/java/util/Collection.html)

接口置于最顶上，意思是想说：Collection其实是整个JCF家族中的“祖宗”，几乎所有的JCF成员都源自该接口，或者和它有密切的关系，看过Collection接口的文档或者源码就可以知道,Collection提供关于集合的一些通用操作的接口，包括插入（

[add](http://java.sun.com/j2se/1.4.2/docs/api/java/util/Collection.html#add%28java.lang.Object%29)

\(\)方法）、删除（

[remove](http://java.sun.com/j2se/1.4.2/docs/api/java/util/Collection.html#remove%28java.lang.Object%29)

\(\)方法）、判断一个元素是不是其成员（

[contains](http://java.sun.com/j2se/1.4.2/docs/api/java/util/Collection.html#contains%28java.lang.Object%29)

\(\)方法）、遍历（

[iterator](http://java.sun.com/j2se/1.4.2/docs/api/java/util/Collection.html#iterator%28%29)

\(\)方法）等等。注意了，前面的“废话”在这里将得到体现：

[Set](http://java.sun.com/j2se/1.4.2/docs/api/java/util/Set.html)

接口体现的是“无序集”的概念，它是不允许有重复元素出现的；

[List](http://java.sun.com/j2se/1.4.2/docs/api/java/util/List.html)

接口代表“有序集”；而

[Map](http://java.sun.com/j2se/1.4.2/docs/api/java/util/Map.html)

接口则是“映射” ，其实

[Map.Entry](http://java.sun.com/j2se/1.4.2/docs/api/java/util/Map.Entry.html)

接口就是代表一个“元素对”我们可以通过Map的

[entrySet](http://java.sun.com/j2se/1.4.2/docs/api/java/util/Map.html#entrySet%28%29)

\(\) 方法得到这样一个由“元素对”组成的Set对象。我们注意到Set和List都是从“祖宗”Collection派生的，而Map不是，毕竟对一对元素的 操作与对单个元素的操作还是有区别的，但是如果你仔细对照一下Collection和Map的源代码，以及它们的直接后代

[AbstractCollection](http://java.sun.com/j2se/1.4.2/docs/api/java/util/AbstractCollection.html)

和

[AbstractMap](http://java.sun.com/j2se/1.4.2/docs/api/java/util/AbstractMap.html)

的源代码，你将会发现很多相似的地方，所以我们仍然可以把Map看成是和Collection有着血缘关系的接口，而和Set，List一起处于并列的位置。

有了“无序集”，“有序集”和“映射”，我们就可以定义各种各样的抽象数据结构了，譬如常见的向量，链表，堆栈，哈希表，平衡二叉树等。

从上我们了解到了,java集合框架的本质是对数据结构的抽象



#### 集合框架底层数据结构总结

#### - Collection

#### 1. List

* Arraylist：数组（查询快,增删慢 线程不安全,效率高 ）
* Vector：数组（查询快,增删慢 线程安全,效率低 ）
* LinkedList：链表（查询慢,增删快 线程不安全,效率高 ）

#### 2. Set

* HashSet（无序，唯一）:哈希表或者叫散列集\(hash table\)
* LinkedHashSet：链表和哈希表组成 。 由链表保证元素的排序 ， 由哈希表证元素的唯一性
* TreeSet（有序，唯一）：红黑树\(自平衡的排序二叉树。\)

### - Map

* HashMap：基于哈希表的Map接口实现（哈希表对键进行散列，Map结构即映射表存放键值对）
* LinkedHashMap:HashMap 的基础上加上了链表数据结构
* HashTable:哈希表
* TreeMap:红黑树（自平衡的排序二叉树）



