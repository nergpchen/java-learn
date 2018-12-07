#### 一 Selector（选择器）介绍

**Selector** 一般称 为**选择器** ，当然你也可以翻译为 **多路复用器** 。它是Java NIO核心组件中的一个，用于检查一个或多个NIO Channel（通道）的状态是否处于可读、可写。如此可以实现单线程管理多个channels,也就是可以管理多个网络链接。

**使用Selector的好处在于：** 使用更少的线程来就可以来处理通道了， 相比使用多个线程，避免了线程上下文切换带来的开销。



## 二 Selector（选择器）的使用方法介绍

### 1. Selector的创建

通过调用Selector.open\(\)方法创建一个Selector对象，如下：

```
Selector selector = Selector.open();
```

这里需要说明一下

### 2. 注册Channel到Selector

```
channel.configureBlocking(false); 
SelectionKey key= channel.register(selector, Selectionkey.OP_READ);
```

**Channel必须是非阻塞的**。 所以FileChannel不适用Selector，因为FileChannel不能切换为非阻塞模式，更准确的来说是因为FileChannel没有继承SelectableChannel。Socket channel可以正常使用。

**SelectableChannel抽象类** 有一个 **configureBlocking（）** 方法用于使通道处于阻塞模式或非阻塞模式。

```
    
```



