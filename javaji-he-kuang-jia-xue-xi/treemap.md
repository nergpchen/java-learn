TreeMap

TreeMap是一个实现了红黑树数据结构的可排序的Map集合,实现了NavigableMap接口,检索和添加的时间开销成本是log\(n\).

TreeMap的排序由Comparator来定义,也可以自己定义一个Comparator.

特点

怎么用?

#### 数据结构:

TreeMap定义了 Entry root根节点.root是一个树的根节点，我们来看看Entry是如何定义一个树的节点的，我们可以把这个代码存放在自己的代码笔记里，学习如何设计一个红-黑二叉树的节点

TreeMapd定义了Entry来存储元素，我们看看Entry的代码:

  `K key;`

` V value;`

` Entry<K,V>left;`

` Entry<K,V>right;`

` Entry<K,V>parent;`

`booleancolor = BLACK;`

每个节点除了key-value值外, 定义了left、right、parent3个指针。

Put

TreeMap是如何添加元素的?看下面的代码 

`/**`

` * Associates the specified value with the specified key in this map.`

` * If the map previously contained a mapping for the key, the old`

` * value is replaced.`

` */`

`public V put(K key, V value) {`

` Entry<K,V>t = root;`

`if (t == null) {`

` compare(key,key); // type (and possibly null) check`

`root = new Entry<>(key, value, null);`

`size = 1;`

`modCount++;`

`returnnull;`

` }`

`intcmp;`

` Entry<K,V>parent;`

` // split comparator and comparable paths`

` Comparator<? super K>cpr = comparator;`

`if (cpr != null) {`

`do {`

`parent = t;`

`cmp = cpr.compare(key, t.key);`

`if (cmp< 0)`

`t = t.left;`

`elseif (cmp> 0)`

`t = t.right;`

`else`

`returnt.setValue(value);`

` } while (t != null);`

` }`

`else {`

`if (key == null)`

`thrownew NullPointerException();`

` @SuppressWarnings("unchecked")`

` Comparable<? super K>k = (Comparable<? super K>) key;`

`do {`

`parent = t;`

`cmp = k.compareTo(t.key);`

`if (cmp< 0)`

`t = t.left;`

`elseif (cmp> 0)`

`t = t.right;`

`else`

`returnt.setValue(value);`

` } while (t != null);`

` }`

` Entry<K,V>e = new Entry<>(key, value, parent);`

`if (cmp< 0)`

`parent.left = e;`

`else`

`parent.right = e;`

` fixAfterInsertion(e);`

`size++;`

`modCount++;`

`returnnull;`

` }`

来看看大概的代码逻辑:

1.

