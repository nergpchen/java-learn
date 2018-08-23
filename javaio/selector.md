**Selector（选择器）介绍**

1. * Selector 一般称 为选择器 ，当然你也可以翻译为 多路复用器 。它是Java NIO核心组件中的一个，用于检查一个或多个NIO Channel（通道）的状态是否处于可读、可写。如此可以实现单线程管理多个channels,也就是可以管理多个网络链接。
   * 使用Selector的好处在于： 使用更少的线程来就可以来处理通道了， 相比使用多个线程，避免了线程上下文切换带来的开销。
2. **Selector（选择器）的使用方法介绍**

   * Selector的创建

   ```
   Selector
    selector 
   =
   Selector
   .
   open();
   ```

   * 注册Channel到Selector\(Channel必须是非阻塞的\)

   ```
   channel
   .
   configureBlocking(
   false
   );

   SelectionKey
    key 
   =
    channel
   .
   register(selector, 
   Selectionkey
   .
   OP_READ
   );
   ```

   * SelectionKey介绍

     一个SelectionKey键表示了一个特定的通道对象和一个特定的选择器对象之间的注册关系。

   * 从Selector中选择channel\(Selecting Channels via a Selector\)

     选择器维护注册过的通道的集合，并且这种注册关系都被封装在SelectionKey当中.

   * 停止选择的方法

     wakeup\(\)方法 和close\(\)方法。

3. **模板代码**

   有了模板代码我们在编写程序时，大多数时间都是在模板代码中添加相应的业务代码。

4. **客户端与服务端简单交互实例**



