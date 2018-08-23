**Channel（通道）介绍**

1. * 通常来说NIO中的所有IO都是从 Channel（通道） 开始的。
   * NIO Channel通道和流的区别：
2. **FileChannel的使用**
3. **SocketChannel和ServerSocketChannel的使用**
4. **️DatagramChannel的使用**
5. **Scatter / Gather**
   * Scatter: 从一个Channel读取的信息分散到N个缓冲区中\(Buufer\).
   * Gather: 将N个Buffer里面内容按照顺序发送到一个Channel.
6. **通道之间的数据传输**
   * 在Java NIO中如果一个channel是FileChannel类型的，那么他可以直接把数据传输到另一个channel。
   * transferFrom\(\) :transferFrom方法把数据从通道源传输到FileChannel
   * transferTo\(\) :transferTo方法把FileChannel数据传输到另一个channel



