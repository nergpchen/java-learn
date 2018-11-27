#### LinkedList是什么？

LinkedList实现了List和双队列的接口，支持null元素.不支持线程，如果要保证线程安全，可以使用下面代码  
`*  List list = Collections.synchronizedList(new LinkedList(...));`

#### 有什么特点？

#### LinkedList 实现 Deque 接口，即能将LinkedList当作双端队列使用。

LinkedList的采用链表来存储元素,那么存储元素和删除速度比较快.

LinkedList不支持高效的随机元素访问:查询元素需要遍历整个链表，速度会慢.

LinkedList不支持线程安全.

#### 如何正确的使用LinkedList?

  LinkedList 是一个继承于AbstractSequentialList的双向链表。它也可以被当作堆栈、队列或双端队列进行操作。

  当操作是在一列数据的后面添加数据而不是在前面或中间,并且需要随机地访问其中的元素时,使用ArrayList会提供比较好的性能，

  当你的操作是在一列数据的前面或中间添加或删除数据,并且按照顺序访问其中的元素时,就应该使用LinkedList了。

#### 核心 有哪些？



