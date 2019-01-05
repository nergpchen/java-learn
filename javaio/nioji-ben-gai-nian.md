NIO主要有**三个核心部分组成**：

* **buffer缓冲区**
* **Channel管道**
* **Selector选择器**

Channel:

Channel有点像流,用来传输数据到Buffer,或者从Buffer读取数据

重要类:

* FileChannel
* DatagramChannel
* SocketChannel
* ServerSocketChannel

FileChannel 从文件中读写数据。

DatagramChannel 能通过UDP读写网络中的数据。

SocketChannel 能通过TCP读写网络中的数据。

ServerSocketChannel可以监听新进来的TCP连接，像Web服务器那样。对每一个新进来的连接都会创建一个SocketChannel。

下面是一个使用FileChannel读取数据到Buffer中的示例：

RandomAccessFile aFile = **new** RandomAccessFile\("data/nio-data.txt", "rw"\);

FileChannel inChannel = aFile.getChannel\(\);

ByteBuffer buf = ByteBuffer.allocate\(48\);

**int** bytesRead = inChannel.read\(buf\);

**while**\(bytesRead != -1\) {

System.out.println\("Read " + bytesRead\);

buf.flip\(\);

**while**\(buf.hasRemaining\(\)\){

System.out.print\(\(**char**\) buf.get\(\)\);

}

buf.clear\(\);

bytesRead = inChannel.read\(buf\);

}

aFile.close\(\)

#### Buffer的基本用法

#### 使用Buffer读写数据一般遵循以下四个步骤：

1. 写入数据到Buffer
2. 调用
   `flip()`
   方法
3. 从Buffer中读取数据
4. 调用
   `clear()`
   方法或者
   `compact()`
   方法

当向buffer写入数据时，buffer会记录下写了多少数据。一旦要读取数据，需要通过flip\(\)方法将Buffer从写模式切换到读模式。在读模式下，可以读取之前写入到buffer的所有数据。

一旦读完了所有的数据，就需要清空缓冲区，让它可以再次被写入。有两种方式能清空缓冲区：调用clear\(\)或compact\(\)方法。clear\(\)方法会清空整个缓冲区。compact\(\)方法只会清除已经读过的数据。任何未读的数据都被移到缓冲区的起始处，新写入的数据将放到缓冲区未读数据的后面。





评论:

java nio的selector主要的问题是效率，当并发连接数达到数万甚至数十万的时候 ，单线程的selector会是一个瓶颈；另一个问题就是再线上运行过程中经常出现cpu占用100%的情况，原因也是由于selector依赖的操作系统底层机制bug 导致的selector假死，需要程序重建selector来解决，这个问题再jdk中似乎并没有很好的解决，netty成为了线上更加可靠的网络框架。不知理解的是否正确，请老师指教。

