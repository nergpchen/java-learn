二叉查找树

二叉查找树（Binary Search Tree，简称BST）是一棵二叉树，它的左子节点的值比父节点的值要小，右节点的值要比父节点的值大。它的高度决定了它的查找效率。

在理想的情况下，二叉查找树增删查改的时间复杂度为O\(logN\)（其中N为节点数），最坏的情况下为O\(N\)。当它的高度为logN+1时，我们就说二叉查找树是平衡的



### BST的查找操作

```
T  key = a search key
Node root = point to the root of a BST

while(true){
    if(root==null){
        break;
    }
    if(root.value.equals(key)){
        return root;
    }
    else if(key.compareTo(root.value)<0){
        root = root.left;
    }
    else{
        root = root.right;
    }
}
return null;
```

从程序中可以看出，当BST查找的时候，先与当前节点进行比较：

* 如果相等的话就返回当前节点；
* 如果少于当前节点则继续查找当前节点的左节点；
* 如果大于当前节点则继续查找当前节点的右节点。

直到当前节点指针为空或者查找到对应的节点，程序查找结束。



BST的插入操作

```
Node node = create a new node with specify value
```

```
Node root = point the root node of a BST
Node parent = null;

//find the parent node to append the new node
while(true){
   if(root==null)break;
   parent = root;
   if(node.value.compareTo(root.value)<=0){
      root = root.left;  
   }else{
      root = root.right;
   } 
}
if(parent!=null){
   if(node.value.compareTo(parent.value)
<
=0){//append to left
      parent.left = node;
   }else{//append to right
      parent.right = node;
   }
}
```

1.先判断根节点是否为空，如果是则中断,如果不是,则父节点=根节点.  
2.如果值 &gt; 根节点,则移到右节点  
3.如果值&lt;根节点，则移到左边.  
4.直到当前节点为空，则结束  
5.然后和父节点判断.改放在那边

### BST的删除操作

删除操作的步骤如下:

1. 查找到要删除的节点。
2. 如果待删除的节点是叶子节点，则直接删除。
3. 如果待删除的节点不是叶子节点，则先找到待删除节点的中序遍历的后继节点，用该后继节点的值替换待删除的节点的值，然后删除后继节点。

### BST存在的问题

BST存在的主要问题是，数在插入的时候会导致树倾斜，不同的插入顺序会导致树的高度不一样，而树的高度直接的影响了树的查找效率。理想的高度是logN，最坏的情况是所有的节点都在一条斜线上，这样的树的高度为N。

## RBTree

基于BST存在的问题，一种新的树——平衡二叉查找树\(Balanced BST\)产生了。平衡树在插入和删除的时候，会通过旋转操作将高度保持在logN。其中两款具有代表性的平衡树分别为AVL树和红黑树。AVL树由于实现比较复杂，而且插入和删除性能差，在实际环境下的应用不如红黑树



红黑树（Red-Black Tree，以下简称RBTree）的实际应用非常广泛，比如Linux内核中的完全公平调度器、高精度计时器、ext3文件系统等等，各种语言的函数库如Java的TreeMap和TreeSet，C++ STL的map、multimap、multiset等。

**java 8中HashMap的实现也因为用RBTree取代链表，性能有所提升。**

### RBTree的定义

RBTree的定义如下:

1. 任何一个节点都有颜色，黑色或者红色
2. 根节点是黑色的
3. 父子节点之间不能出现两个连续的红节点
4. 任何一个节点向下遍历到其子孙的叶子节点，所经过的黑节点个数必须相等

数据结构表示如下:

```
{
   public  T value;
   public   Node<T>parent;
   public   boolean isRed;
   public   Node<T> left;
   public   Node<T> right;
   
```





https://zhuanlan.zhihu.com/p/24367771

