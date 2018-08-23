**Buffer\(缓冲区\)介绍:**

1. * Java NIO Buffers用于和NIO Channel交互。 我们从Channel中读取数据到buffers里，从Buffer把数据写入到Channels；
   * Buffer本质上就是一块内存区；
   * 一个Buffer有三个属性是必须掌握的，分别是：capacity容量、position位置、limit限制。
2. **Buffer的常见方法**

   * Buffer clear\(\)
   * Buffer flip\(\)
   * Buffer rewind\(\)
   * Buffer position\(int newPosition\)

3. **Buffer的使用方式/方法介绍:**

   1. * 分配缓冲区（Allocating a Buffer）:

      ```
      ByteBuffer
       buf 
      =
      ByteBuffer
      .
      allocate(
      28
      );
      //
      以ByteBuffer为例子
      ```

      * 写入数据到缓冲区（Writing Data to a Buffer）

      **写数据到Buffer有两种方法：**

      1.从Channel中写数据到Buffer

      ```
      int
       bytesRead 
      =
       inChannel
      .
      read(buf); 
      //
      read into buffer.
      ```

      2.通过put写数据：

      ```
      buf
      .
      put(
      127
      );
      ```

   2. **Buffer常用方法测试**

      说实话，NIO编程真的难，通过后面这个测试例子，你可能才能勉强理解前面说的Buffer方法的作用。



