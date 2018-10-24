### 堆排序

看堆排序之前先介绍一下面几个概念：

完全二叉树： 若设二叉树的深度为h，除第 h 层外，其它各层 \(1～h-1\) 的结点数都达到最大个数，第 h 层所有的结点都连续集中在最左边，这就是完全二叉树，很好理解如下图所示。

![](http://www.liuhaihua.cn/wp-content/uploads/2018/10/ZZFZb2E.jpg "面试必备：八种排序算法原理及Java实现")

  


堆： 堆是具有以下性质的完全二叉树，每个结点的值都大于或等于其左右孩子结点的值，称为大顶堆；或者每个结点的值都小于或等于其左右孩子结点的值，称为小顶堆。如下图：

![](http://www.liuhaihua.cn/wp-content/uploads/2018/10/32qE3uY.png "面试必备：八种排序算法原理及Java实现")

  


同时，我们对堆中的结点按层进行编号，将这种逻辑结构映射到数组中就是下面这个样子：

![](http://www.liuhaihua.cn/wp-content/uploads/2018/10/m6RriyQ.png "面试必备：八种排序算法原理及Java实现")

  


该数组从逻辑上讲就是一个堆结构，我们用简单的公式来描述一下堆的定义就是：

大顶堆：arr\[i\] &gt;= arr\[2i+1\] && arr\[i\] &gt;= arr\[2i+2\]

小顶堆：arr\[i\] &lt;= arr\[2i+1\] && arr\[i\] &lt;= arr\[2i+2\]

ok，了解了这些定义。接下来，我们来看看堆排序的基本思想及基本步骤：

#### 9.1 基本思想

堆排序的基本思想是：将待排序序列构造成一个大顶堆，此时，整个序列的最大值就是堆顶的根节点。将其与末尾元素进行交换，此时末尾就为最大值。然后将剩余n-1个元素重新构造成一个堆，这样会得到n个元素的次小值。如此反复执行，便能得到一个有序序列了。

#### 9.2 算法描述

步骤一 构造初始堆。将给定无序序列构造成一个大顶堆（一般升序采用大顶堆，降序采用小顶堆\)。

1.假设给定无序序列结构如下

![](http://www.liuhaihua.cn/wp-content/uploads/2018/10/QRzQfqn.png "面试必备：八种排序算法原理及Java实现")

  


2.此时我们从最后一个非叶子结点开始（叶结点自然不用调整，第一个非叶子结点 arr.length/2-1=5/2-1=1，也就是下面的6结点），从左至右，从下至上进行调整。

![](http://www.liuhaihua.cn/wp-content/uploads/2018/10/EfMbEbF.png "面试必备：八种排序算法原理及Java实现")

  


3.找到第二个非叶节点4，由于\[4,9,8\]中9元素最大，4和9交换。

![](http://www.liuhaihua.cn/wp-content/uploads/2018/10/2MjuMjb.png "面试必备：八种排序算法原理及Java实现")

  


这时，交换导致了子根\[4,5,6\]结构混乱，继续调整，\[4,5,6\]中6最大，交换4和6。

![](http://www.liuhaihua.cn/wp-content/uploads/2018/10/beiUzuE.png "面试必备：八种排序算法原理及Java实现")

  


此时，我们就将一个无需序列构造成了一个大顶堆。

步骤二 将堆顶元素与末尾元素进行交换，使末尾元素最大。然后继续调整堆，再将堆顶元素与末尾元素交换，得到第二大元素。如此反复进行交换、重建、交换。

![](http://www.liuhaihua.cn/wp-content/uploads/2018/10/nIbMVrY.png "面试必备：八种排序算法原理及Java实现")

  


b.重新调整结构，使其继续满足堆定义

![](http://www.liuhaihua.cn/wp-content/uploads/2018/10/NFFJvab.png "面试必备：八种排序算法原理及Java实现")

  


c.再将堆顶元素8与末尾元素5进行交换，得到第二大元素8.

![](http://www.liuhaihua.cn/wp-content/uploads/2018/10/rimieeN.png "面试必备：八种排序算法原理及Java实现")

  


后续过程，继续进行调整，交换，如此反复进行，最终使得整个序列有序

![](http://www.liuhaihua.cn/wp-content/uploads/2018/10/eEVfeez.png "面试必备：八种排序算法原理及Java实现")

  


再简单[总结](http://www.liuhaihua.cn/archives/tag/%e6%80%bb%e7%bb%93)下堆排序的基本思路：

a.将无需序列构建成一个堆，根据升序降序需求选择大顶堆或小顶堆;

b.将堆顶元素与末尾元素交换，将最大元素"沉"到数组末端;

c.重新调整结构，使其满足堆定义，然后继续交换堆顶元素与当前末尾元素，反复执行调整+交换步骤，直到整个序列有序。

#### 9.3 算法实现

```
package com.fufu.algorithm.sort;

import java.util.Arrays;

/**
 * Created by zhoujunfu on 2018/9/26.
 */
public class HeapSort {

    public static void main(String []args){
        int []arr = {4,6,8,5,9};
        sort(arr);
        System.out.println(Arrays.toString(arr));
    }
    public static void sort(int []arr){
        //1.构建大顶堆
        for(int i=arr.length/2-1;i
>
=0;i--){
            //从第一个非叶子结点从下至上，从右至左调整结构
            adjustHeap(arr,i,arr.length);
        }
        //2.调整堆结构+交换堆顶元素与末尾元素
        for(int j=arr.length-1;j
>
0;j--){
            swap(arr,0,j);//将堆顶元素与末尾元素进行交换
            adjustHeap(arr,0,j);//重新对堆进行调整
        }

    }

    /**
     * 调整大顶堆（仅是调整过程，建立在大顶堆已构建的基础上）
     * @param arr
     * @param i
     * @param length
     */
    public static void adjustHeap(int []arr,int i,int length){
        int temp = arr[i];//先取出当前元素i
        for(int k=i*2+1;k
<
length;k=k*2+1){//从i结点的左子结点开始，也就是2i+1处开始
            if(k+1
<
length 
&
&
 arr[k]
<
arr[k+1]){//如果左子结点小于右子结点，k指向右子结点
                k++;
            }
            if(arr[k] 
>
temp){//如果子节点大于父节点，将子节点值赋给父节点（不用进行交换）
                arr[i] = arr[k];
                i = k;
            }else{
                break;
            }
        }
        arr[i] = temp;//将temp值放到最终的位置
    }

    /**
     * 交换元素
     * @param arr
     * @param a
     * @param b
     */
    public static void swap(int []arr,int a ,int b){
        int temp=arr[a];
        arr[a] = arr[b];
        arr[b] = temp;
    }
}
复制代码
```

#### 9.4 算法效率

由于堆排序中初始化堆的过程比较次数较多, 因此它不太适用于小序列。同时由于多次任意下标相互交换位置, 相同元素之间原本相对的顺序被破坏了, 因此, 它是不稳定的排序。

①. 建立堆的过程, 从length/2 一直处理到0, 时间复杂度为O\(n\);

②. 调整堆的过程是沿着堆的父子节点进行调整, 执行次数为堆的深度, 时间复杂度为O\(lgn\);

③. 堆排序的过程由n次第②步完成, 时间复杂度为O\(nlgn\).

| 平均时间复杂度 | 最好情况 | 最坏情况 | 空间复杂度 |
| :--- | :--- | :--- | :--- |
| O\(nlogn\) | O\(nlogn\) | O\(nlogn\) | O\(1\) |

### 10. 总结

![](http://www.liuhaihua.cn/wp-content/uploads/2018/10/UVj6fuZ.png "面试必备：八种排序算法原理及Java实现")

  


从时间复杂度来说：

\(1\). 平方阶O\(n²\)排序：各类简单排序：直接插入、直接选择和冒泡排序；

\(2\). 线性对数阶O\(nlog₂n\)排序：快速排序、堆排序和归并排序；

\(3\). O\(n1+§\)\)排序，§是介于0和1之间的常数：希尔排序

\(4\). 线性阶O\(n\)排序：基数排序，此外还有桶、箱排序。

时间复杂度极限：

当被排序的数有一些性质的时候（比如是整数，比如有一定的范围），排序算法的复杂度是可以小于O\(nlgn\)的。比如：

计数排序 复杂度O\( k+n\) 要求：被排序的数是0~k范围内的整数

基数排序 复杂度O\( d\(k+n\) \) 要求：d位数，每个数位有k个取值

桶排序 复杂度 O\( n \) （平均） 要求：被排序数在某个范围内，并且服从均匀分布

但是，当被排序的数不具有任何性质的时候，一般使用基于比较的排序算法，而基于比较的排序算法时间复杂度的下限必须是O\( nlgn\) 。参考 很多高效排序算法的代价是 nlogn，难道这是排序算法的极限了吗 ？

说明 当原表有序或基本有序时，直接插入排序和冒泡排序将大大减少比较次数和移动记录的次数，时间复杂度可降至O（n）；

而快速排序则相反，当原表基本有序时，将蜕化为冒泡排序，时间复杂度提高为O（n2）；

原表是否有序，对简单选择排序、堆排序、归并排序和基数排序的时间复杂度影响不大

