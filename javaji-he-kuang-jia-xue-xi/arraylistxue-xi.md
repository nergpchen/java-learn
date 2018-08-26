#### 1:ArrayList介绍

ArrayList是实现List接口的动态数组，所谓动态就是它的大小是可变的。实现了所有可选列表操作，并允许包括 null 在内的所有元素

     每个ArrayList实例都有一个容量，该容量是指用来存储列表元素的数组的大小。默认初始容量为10。随着ArrayList中元素的增加，它的容量也会不断的自动增长。

     在每次添加新的元素时，ArrayList都会检查是否需要进行扩容操作，扩容操作带来数据向新数组的重新拷贝，所以如果我们知道具体业务数据量，在构造ArrayList时可以给ArrayList指定一个初始容量，这样就会减少扩容时数据的拷贝问题。当然在添加大量元素前，应用程序也可以使用ensureCapacity操作来增加ArrayList实例的容量，这可以减少递增式再分配的数

    

#### 2: 线程不同步

#### **注意，ArrayList实现不是同步的**。如果多个线程同时访问一个ArrayList实例，而其中至少一个线程从结构上修改了列表，那么它必须保持外部同步。所以为了保证同步，最好的办法是在创建时完成，以防止意外对列表进行不同步的访问：

```
        List list = Collections.synchronizedList(new ArrayList(...)); 
```



#### 二、ArrayList源码分析    

  
数据结构:  用数组存储元素

```
 private transient Object[] elementData;
```

  
ArrayList新增：

```
public boolean
 add(E e) {
    ensureCapacity(size 
+ 1);  
//
 Increments modCount!!

    elementData[size++] =
 e;
    
return
true
;
    }
```

这里ensureCapacity\(\)方法是对ArrayList集合进行扩容操作，elementData\(size++\) = e，将列表末尾元素指向e。

在这个方法中最根本的方法就是System.arraycopy\(\)方法，该方法的根本目的就是将index位置空出来以供新数据插入，这里需要进行数组数据的右移，这是非常麻烦和耗时的，所以如果指定的数据集合需要进行大量插入（中间插入）操作，推荐使用LinkedList.





三**扩容**

      使用 ensureCapacity\(\)，该方法就是ArrayList的扩容方法。

  

[![](https://common.cnblogs.com/images/copycode.gif "复制代码")](javascript:void%280%29;)代码如下：

```
public
void
 ensureCapacity(
int
 minCapacity) {
        
//
修改计时器

        modCount++
;
        
//
ArrayList容量大小
int
 oldCapacity =
 elementData.length;
        
/*

         * 若当前需要的长度大于当前数组的长度时，进行扩容操作
         
*/
if
 (minCapacity 
>
 oldCapacity) {
            Object oldData[] 
=
 elementData;
            
//
计算新的容量大小，为当前容量的1.5倍
int
 newCapacity = (oldCapacity * 3) / 2 + 1
;
            
if
 (newCapacity 
<
 minCapacity)
                newCapacity 
=
 minCapacity;
            
//
数组拷贝，生成新的数组

            elementData =
 Arrays.copyOf(elementData, newCapacity);
        }
    }
```

[![](https://common.cnblogs.com/images/copycode.gif "复制代码")](javascript:void%280%29;)

      在这里有一个疑问，为什么每次扩容处理会是1.5倍，而不是2.5、3、4倍呢？通过google查找，发现1.5倍的扩容是最好的倍数。因为一次性扩容太大\(例如2.5倍\)可能会浪费更多的内存\(1.5倍最多浪费33%，而2.5被最多会浪费60%，3.5倍则会浪费71%……\)。但是一次性扩容太小，需要多次对数组重新分配内存，对性能消耗比较严重。所以1.5倍刚刚好，既能满足性能需求，也不会造成很大的内存消耗。

      处理这个ensureCapacity\(\)这个扩容数组外，ArrayList还给我们提供了将底层数组的容量调整为当前列表保存的实际元素的大小的功能。它可以通过trimToSize\(\)方法来实现。该方法可以最小化ArrayList实例的存储量。

[![](https://common.cnblogs.com/images/copycode.gif "复制代码")](javascript:void%280%29;)

```
public
void
 trimToSize() {
        modCount
++
;
        
int
 oldCapacity =
 elementData.length;
        
if
 (size 
<
 oldCapacity) {
            elementData 
=
 Arrays.copyOf(elementData, size);
        }
    }
```

[![](https://common.cnblogs.com/images/copycode.gif "复制代码")](javascript:void%280%29;)



