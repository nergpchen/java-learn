1.JVM数据区域:

如下图，分为方法区、Stack、本地方法Stack、堆、程序计数器

![](/assets/jvm1.png)

**线程私有的：**

* 程序计数器
* 虚拟机栈
* 本地方法栈

**线程共享的：**

* 堆
* 方法区
* 直接内存

### 2.1 程序计数器

程序计数器是一块较小的内存空间，可以看作是当前线程所执行的字节码的行号指示器。

**字节码解释器工作时通过改变这个计数器的值来选取下一条需要执行的字节码指令，分支、循环、跳转、异常处理、线程恢复等功能都需要依赖这个计数器来完。**

### 2.2 Java 虚拟机栈

  
**与程序计数器一样，Java虚拟机栈也是线程私有的，它的生命周期和线程相同，描述的是 Java 方法执行的内存模型。**




