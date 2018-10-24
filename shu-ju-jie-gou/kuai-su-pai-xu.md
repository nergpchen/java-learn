介绍

快速排序（Quicksort）是对冒泡排序的一种改进，借用了分治的思想，由C. A. R. Hoare在1962年提出。

它的基本思想是：通过一趟排序将要排序的数据分割成独立的两部分，其中一部分的所有数据都比另外一部分的所有数据都要小，然后再按此方法对这两部分数据分别进行快速排序，整个排序过程可以[递归](http://www.liuhaihua.cn/archives/tag/%e9%80%92%e5%bd%92)进行，以此达到整个数据变成有序序列。



#### 3.2 算法描述

快速排序使用分治策略来把一个序列（[list](http://www.liuhaihua.cn/archives/tag/list)）分为两个子序列（sub-lists）。步骤为：

①. 从数列中挑出一个元素，称为”基准”（pivot）。

②. 重新排序数列，所有比基准值小的元素摆放在基准前面，所有比基准值大的元素摆在基准后面（相同的数可以到任一边）。在这个分区结束之后，该基准就处于数列的中间位置。这个称为分区（partition）操作。

③. 递归地（recursively）把小于基准值元素的子数列和大于基准值元素的子数列排序。

递归到最底部时，数列的大小是零或一，也就是已经排序好了。这个算法一定会结束，因为在每次的迭代（iteration）中，它至少会把一个元素摆到它最后的位置去。

代码如下：

```
public class FastSort{

     public static void main(String []args){
        System.out.println("Hello World");
        int[] a = {12,20,5,16,15,1,30,45,23,9};
        int start = 0;
        int end = a.length-1;
        sort(a,start,end);
        for(int i = 0; i<a.length; i++){
             System.out.println(a[i]);
         }
        
     }
     
     public void sort(int[] a,int low,int high){
         int start = low;
         int end = high;
         int key = a[low];
         
         
         while(end>start){
             //从后往前比较
             while(end>start&&a[end]>=key)  //如果没有比关键值小的，比较下一个，直到有比关键值小的交换位置，然后又从前往后比较
                 end--;
             if(a[end]<=key){
                 int temp = a[end];
                 a[end] = a[start];
                 a[start] = temp;
             }
             //从前往后比较
             while(end>start&&a[start]<=key)//如果没有比关键值大的，比较下一个，直到有比关键值大的交换位置
                start++;
             if(a[start]>=key){
                 int temp = a[start];
                 a[start] = a[end];
                 a[end] = temp;
             }
         //此时第一次循环比较结束，关键值的位置已经确定了。左边的值都比关键值小，右边的值都比关键值大，但是两边的顺序还有可能是不一样的，进行下面的递归调用
         }
         //递归
         if(start>low) sort(a,low,start-1);//左边序列。第一个索引位置到关键值索引-1
         if(end<high) sort(a,end+1,high);//右边序列。从关键值索引+1到最后一个
     }
     
}
```



