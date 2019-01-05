CyclicBarrier简介

_\* A synchronization aid that allows a set of threads to all wait for_

_\* each other to reach a common barrier point. CyclicBarriers are_

_\* useful in programs involving a fixed sized party of threads that_

_\* must occasionally wait for each other. The barrier is called_

_\* &lt;em&gt;cyclic&lt;/em&gt; because it can be re-used after the waiting threads_

_\* are released._

看上面在文档的介绍，可以看出CyclicBarrier是一个协调多个线程的同步机制，可以让全部的线程等待，直到全部的线程达到一个屏障点\( barrier point\).



