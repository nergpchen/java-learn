#### 一、NIO介绍

NIO是在jdk1.4引入的接口，他的性能优化比IO有显著的提升.

那么我们就要想知道有哪些方面的提升？

他是怎么做到提升的？代码怎么设计的？

1:NIO和IO的对比.

IO是面向流的、堵塞的、单线程的接口；

而NIO是面向缓冲的、非阻塞的、通过选择器可以支持多个通道.

通过缓冲、非阻塞I/O和多个通道可以显著提升读写多性能和CPU的使用,而且NIO还提供了内存映射技术.

#### 二. 内存映射 {#2-内存映射}

内存映射就是把文件映射到进程的内存空间，然后通过操作内存来操作文件，其实就是使用虚拟内存将磁盘的文件数据加载到虚拟内存的内存页，然后可以直接操作内存数据。

而标准的I/O在读写文件的时候，需要把数据读取到OS的缓存区，然后程序再读取数据；而映射是直接 读取内存的文件，这样的速度会显著的提高。

内存映射技术是解决大文件的读写速度问题，因为大文件是无法直接一次性读写到内存的，而通过memory-mappedfile技术，就可以当作把文件当作一次性读写到内存，从而把文件当作

引用

#### 四、如何使用

我们看看实现的代码

下面我们通过一个例子来看一下内存映射读取文件和普通的IO流读取一个150M大文件的速度对比：



`public class MemMap {`

`    public static void main(String[] args) {`

`        try {`

`            RandomAccessFile file = new RandomAccessFile("c://1.pdf","rw");`

`            FileChannel channel = file.getChannel();`

`            MappedByteBuffer buffer = channel.map(FileChannel.MapMode.READ_ONLY,0,channel.size());`

`            ByteBuffer buffer1 = ByteBuffer.allocate(1024);`

`            byte[] b = new byte[1024];`



`            long len = file.length();`

`            long startTime = System.currentTimeMillis();`

`            //读取内存映射文件`

`            for(int i=0;i<file.length();i+=1024*10){`

`                if (len - i > 1024) {`

`                    buffer.get(b);`

`                } else {`

`                    buffer.get(new byte[(int)(len - i)]);`

`                }`

`            }`

`            long endTime = System.currentTimeMillis();`

`            System.out.println("使用内存映射方式读取文件总耗时： "+(endTime - startTime));`





`            //普通IO流方式`

`            long startTime1 = System.currentTimeMillis();`

`            while(channel.read(buffer1) > 0){`

`                buffer1.flip();`

`                buffer1.clear();`

`            }`



`            long endTime1 = System.currentTimeMillis();`

`            System.out.println("使用普通IO流方式读取文件总耗时： "+(endTime1 - startTime1));`



`        } catch (Exception e) {`

`            e.printStackTrace();`

`        }`

`    }`

`}`



1.[https://blog.csdn.net/a953713428/article/details/64907250](https://blog.csdn.net/a953713428/article/details/64907250)

2.https://www.cnblogs.com/lyftest/p/6564547.html

