TreeMap

TreeMap是一个实现了红黑树数据结构的可排序的Map集合,实现了NavigableMap接口,检索和插入的时间开销成本是Olog\(n\).

TreeMap的排序由Comparator来定义,也可以自己定义一个Comparator.

特点

怎么用?

#### 数据结构:

TreeMap定义了 Entry root根节点.root是一个树的根节点，我们来看看Entry是如何定义一个树的节点的，我们可以把这个代码存放在自己的代码笔记里，学习如何设计一个红-黑二叉树的节点

TreeMapd定义了Entry来存储元素，我们看看Entry的代码:

`K key;`

`V value;`

`Entry<K,V>left;`

`Entry<K,V>right;`

`Entry<K,V>parent;`

`booleancolor = BLACK;`

每个节点除了key-value值外, 定义了left、right、parent3个指针。

Put

TreeMap是如何添加元素的?看下面的代码

`/**`

`* Associates the specified value with the specified key in this map.`

`* If the map previously contained a mapping for the key, the old`

`* value is replaced.`

`*/`

`public V put(K key, V value) {`

`Entry<K,V>t = root;`

`if (t == null) {`

`compare(key,key); // type (and possibly null) check`

`root = new Entry<>(key, value, null);`

`size = 1;`

`modCount++;`

`returnnull;`

`}`

`intcmp;`

`Entry<K,V>parent;`

`// split comparator and comparable paths`

`Comparator<? super K>cpr = comparator;`

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

`} while (t != null);`

`}`

`else {`

`if (key == null)`

`thrownew NullPointerException();`

`@SuppressWarnings("unchecked")`

`Comparable<? super K>k = (Comparable<? super K>) key;`

`do {`

`parent = t;`

`cmp = k.compareTo(t.key);`

`if (cmp< 0)`

`t = t.left;`

`elseif (cmp> 0)`

`t = t.right;`

`else`

`returnt.setValue(value);`

`} while (t != null);`

`}`

`Entry<K,V>e = new Entry<>(key, value, parent);`

`if (cmp< 0)`

`parent.left = e;`

`else`

`parent.right = e;`

`fixAfterInsertion(e);`

`size++;`

`modCount++;`

`returnnull;`

`}`

来看看大概的代码逻辑:

1.如果还没有根节点,则设置新加的元素节点为根节点.

2.如果当前已经有了根节点,则就判断需要把当前元素添加到树的左边还是右边呢？

3.如果有比较器,则和root节点的key比较大小，遍历树，找到当前节点的父节点.

4.生成新节点，根据key的大小添加到父节点的左边或者右边.

5.调用fixAfterInsertion\(\)确定红黑节点,这个也是一段很关键的代码.

下面代码是遍历二叉树的节点，先对比key的大小，选择遍历是左边树还是右边树，直到遍历的节点为空，就表示遍历到了最后的位置,停止循环.  
`do {`

`parent = t;`

`cmp = cpr.compare(key, t.key);`

`if (cmp< 0)`

`t = t.left;`

`elseif (cmp> 0)`

`t = t.right;`

`else`

`returnt.setValue(value);`

`} while (t != null);`

#### 红黑树介绍:

先了解下红黑树的特性:

1. 节点是红色或黑色。

2. 根节点是黑色。

3 每个叶节点（NIL节点，空节点）是黑色的。

4 每个红色节点的两个子节点都是黑色。\(从每个叶子到根的所有路径上不能有两个连续的红色节点\)

5. 从任一节点到其每个叶子的所有路径都包含相同数目的黑色节点。

java中TreeMap数据结构采用红黑树实现；put方法每次新加元素后，都要调用fixAfterInsertion重新维持红黑树的平衡

贴源码：

    `private void fixAfterInsertion(Entry<K,V> x) {`

`x.color = RED;`

`while (x != null && x != root && x.parent.color == RED) {`

`if (parentOf(x) == leftOf(parentOf(parentOf(x)))) {`

`Entry<K,V> y = rightOf(parentOf(parentOf(x)));`

`if (colorOf(y) == RED) {`

`setColor(parentOf(x), BLACK);`

`setColor(y, BLACK);`

`setColor(parentOf(parentOf(x)), RED);`

`x = parentOf(parentOf(x));`

`} else {`

`if (x == rightOf(parentOf(x))) {`

`x = parentOf(x);`

`rotateLeft(x);`

`}`

`setColor(parentOf(x), BLACK);`

`setColor(parentOf(parentOf(x)), RED);`

`rotateRight(parentOf(parentOf(x)));`

`}`

`} else {`

`Entry<K,V> y = leftOf(parentOf(parentOf(x)));`

`if (colorOf(y) == RED) {`

`setColor(parentOf(x), BLACK);`

`setColor(y, BLACK);`

`setColor(parentOf(parentOf(x)), RED);`

`x = parentOf(parentOf(x));`

`} else {`

`if (x == leftOf(parentOf(x))) {`

`x = parentOf(x);`

`rotateRight(x);`

`}`

`setColor(parentOf(x), BLACK);`

`setColor(parentOf(parentOf(x)), RED);`

`rotateLeft(parentOf(parentOf(x)));`

`}`

`}`

`}`

`root.color = BLACK;`

`}`

新插入节点为红色

一、父节点是黑色，直接插入不需要重构

二、父节点是红色 （基准节点不是根节点）

1、父亲是祖父的左儿子

①叔叔（右）节点是红色：表示祖父节点必然是黑色。直接开始变色（父亲和叔叔变黑，祖父变红。把基准节点定位到祖父节点，重复这步操作）

②叔叔（右）节点是黑色：

check：该节点是父亲的右儿子，则执行左旋操作（该节点变为父亲，原父亲节点变为左儿子）；此时基准节点变为他的原父亲节点，也就是左旋后新的左儿子\(最左儿子\)

父亲变黑，祖父变红；此时的情况是父亲黑、叔叔黑、祖父红。导致从祖父到叔叔的路径黑色节点变少1个，以祖父节点为基点来一个右旋

2、父亲是祖父的右儿子

①叔叔（左）节点是红色：表示祖父节点必然是黑色。职介开始变色（父亲和叔叔变黑，祖父变红。把基准节点定位到祖父节点，重复这步操作）

②叔叔（左）节点是黑色：

check: 该节点是父亲的左儿子，则执行右旋操作（该节点变为父亲，原父亲节点变为右儿子）；此时基准节点变为他的原父亲节点，也就是右旋后新的右儿子\(最右儿子\)

父亲变黑，祖父变红；此时的情况是父亲黑，叔叔黑，祖父红。导致从祖父到叔叔的路径黑色节点少了1个，以祖父节点为基准来一个左旋

---

作者：m0\_38022622

来源：CSDN

原文：[https://blog.csdn.net/m0\_38022622/article/details/78865265](https://blog.csdn.net/m0_38022622/article/details/78865265)

版权声明：本文为博主原创文章，转载请附上博文链接！

