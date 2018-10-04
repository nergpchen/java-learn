优先队列:优先队列中，元素被赋予优先级。当访问元素时，具有最高优先级的元素最先删除。优先队列具有最高级先出 （first in, largest out）的行为特征。通常采用堆数据结构来实现。  
 

实现

class PriQueues extends Compares&lt;Key&gt;{

  private Key\[\] pq;

  private int N;

public PriQueues\(int N\){

this.N = N;

}

 public void insert\(Key x\){

   pq\[N++\] = x;

}  
public void delete\(\){

//优先级大的先删除

}

}









