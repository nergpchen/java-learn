中断机制：

 java没有直接的方法来停止线程，而是通过一种协议，给线程一个中断的标记，让线程自己去处理中断。

  
p.p1 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px '.PingFang SC'; color: \#454545}  
p.p2 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px 'Helvetica Neue'; color: \#454545}  
p.p3 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px 'Helvetica Neue'; color: \#454545; min-height: 14.0px}  
span.s1 {font: 12.0px 'Helvetica Neue'}  
span.s2 {font: 12.0px '.PingFang SC'}  


上面说了，中断标识位是JDK源码看不到的，是虚拟机线程实现层面的。下面结合代码逐一看一下这三个方法的作用，以及为什么中断标识位是虚拟机实现层面的：

**1**、**interrupt**\(\)

  


`1 public void interrupt() {`

`2  if (this != Thread.currentThread())`

`3  checkAccess();`

`4`

`5  synchronized (blockerLock) {`

`6  Interruptible b = blocker;`

`7  if (b != null) {`

`8  interrupt0(); // Just to set the interrupt flag`

`9  b.interrupt();`

`10  return;`

`11  }`

`12  }`

`13  interrupt0();`

`14  }`

