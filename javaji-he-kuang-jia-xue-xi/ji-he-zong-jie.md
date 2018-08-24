## 集合框架底层数据结构总结

### - Collection

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



