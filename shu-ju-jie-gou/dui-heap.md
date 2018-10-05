简介:

二叉堆是一种特殊的堆，二叉堆是完全二元树（二叉树）或者是近似完全二元树（二叉树\)

分类

二叉堆有两种：[最大堆](https://baike.baidu.com/item/%E6%9C%80%E5%A4%A7%E5%A0%86/4633143)和[最小堆](https://baike.baidu.com/item/%E6%9C%80%E5%B0%8F%E5%A0%86/9139372)

最大堆：[父结点](https://baike.baidu.com/item/%E7%88%B6%E7%BB%93%E7%82%B9/9796346)的键值总是大于或等于任何一个子[节点](https://baike.baidu.com/item/%E8%8A%82%E7%82%B9/865052)的键值；

最小堆：父结点的键值总是小于或等于任何一个子节点的键值。

实现

二叉堆一般用[数组](https://baike.baidu.com/item/%E6%95%B0%E7%BB%84/3794097)来表示。

如果根节点在数组中的位置是1，第n个位置的子节点分别在2\n和 2n+1。

因此，第1个位置的子节点在2和3，第2个位置的子节点在4和5。

以此类推。这种基于1的数组存储方式便于寻找父节点和子节点。



package

 com.bird.six;



/\*\*

\* 

@category

 二叉堆的实现

\* 

@author

 Bird

\*

\*/

public

class

BinaryHeap

 {



private

static

final

int

 DEAFAULT\_CAPACITY = 

100

;

private

int

 currentSize;

//堆中的元素个数

private

 Compare\[\] array;

//存储堆中的元素使用数组存储方式



public

BinaryHeap

\(\)

{

this

\(DEAFAULT\_CAPACITY\);

 }



public

BinaryHeap

\(

int

 capacity\)

{

 currentSize = 

0

;

 array = 

new

 Compare\[capacity+

1

\];



 }



public

boolean

isEmpty

\(\)

{

return

 currentSize == 

0

;

 }



public

boolean

isFull

\(\)

{

return

 currentSize == array.length-

1

;

 }



public

void

makeEmpty

\(\)

{

 currentSize = 

0

;

 }



/\*\*

\* 插入使用“上移”法

\* 

@param

 x

\*/

public

void

insert

\(Compare x\)

{

if

\(isFull\(\)\)

throw

new

 RuntimeException\(

"溢出"

\);



int

 hole = ++currentSize;

for

\(; hole 

&gt;

1

&

&

 x.compareTo\(array\[hole/

2

\]\) 

&lt;

0

; hole /= 

2

\)

 array\[hole\] = array\[hole/

2

\];

 array\[hole\] = x;

 }



/\*\*

\* 使用下溢法进行删除操作

\* 

@return

\*/

public

 Compare 

deleteMin

\(\)

{

if

\(isEmpty\(\)\)

return

null

;



 Compare minItem = array\[

1

\];

 array\[

1

\] = array\[currentSize--\];

 percolateDown\(

1

\);



return

 minItem;

 }



private

void

percolateDown

\(

int

 hole\)

{

int

 child = 

0

;

 Compare tmp = array\[hole\];



for

\(; hole \* 

2

&lt;

= currentSize; hole = child\){

 child = hole \* 

2

;

if

\(child != currentSize 

&

&

 array\[child+

1

\].compareTo\(array\[child\]\)

&lt;

0

\)

 child++;

if

\(array\[child\].compareTo\(tmp\)

&lt;

0

\)

 array\[hole\] = array\[child\];

else

break

;

 }

 array\[hole\] = tmp;

 }

}



class

Compare

implements

Comparable

&lt;

Object

&gt;

{



public

int

compareTo

\(Object o\)

 {

return

 \(\(Integer\)

this

.compareTo\(o\)\);

 }





 --------------------- 本文来自 Bird 的CSDN 博客 ，全文地址请点击：https://blog.csdn.net/a352193394/article/details/7210435?utm\_source=copy

