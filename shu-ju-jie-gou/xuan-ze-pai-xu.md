#### 6.1 基本思想

在未排序序列中找到最小（大）元素，存放到未排序序列的起始位置。在所有的完全依靠交换去移动元素的排序方法中，选择排序属于非常好的一种。

#### 6.2 算法描述

①. 从待排序序列中，找到关键字最小的元素；

②. 如果最小元素不是待排序序列的第一个元素，将其和第一个元素互换；

③. 从余下的 N – 1 个元素中，找出关键字最小的元素，重复①、②步，直到排序结束。

