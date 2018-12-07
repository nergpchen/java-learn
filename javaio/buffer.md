**Buffer\(缓冲区\)介绍:**

_A container for data of a specific primitive type._

_ A buffer is a linear, finite sequence of elements of a specific_

_ primitive type. Aside from its content, the essential properties of a_

_ buffer are its capacity, limit, and position:_

Buffer是基本原始类型的容器,用来存储比如byte、char、int等基本类型的集合，具有线性、有限容量的特点，基本属性包括content、capacity、limit、position.

 capcatiy是集合的容量、limit表示还可以写或者读多少个元素,position是下一个元素读取的位置.一般在初始化的时候,limit=0;position=0.

特点

1.每个buffer都是可读的，但是不一定是可写的，可读的buffer的内容是不会变的.

2.不是线程安全,如果在多线程使用的话，必须加上锁.

3.链式调用

**Buffer的常见方法**

1. * Buffer clear\(\)
   * Buffer flip\(\)
   * Buffer rewind\(\)
   * Buffer position\(int newPosition\)
2. **Buffer的使用方式/方法介绍:**

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



