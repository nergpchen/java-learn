IO简介

I/O就是java提供的对输入输出的接口，比如读写文件的内容、读取网络的内容、读写图像，都要通过I/O的接口.

那么学习I/O接口主要是学习有哪些I/O接口，我们怎么使用这些I/O接口.

java I/O都是基于字节流进行输入输出

Java 的 I/O 操作类在包 java.io 下，大概有将近 80 个类，但是这些类大概可以分成四组，分别是：

1. 基于字节操作的 I/O 接口：InputStream 和 OutputStream
2. 基于字符操作的 I/O 接口：Writer 和 Reader
3. 基于磁盘操作的 I/O 接口：File
4. 基于网络操作的 I/O 接口：Socket

##### 分类一：按操作方式（类结构）

* ##### **字节流和字符流：**
* * 字节流：以字节为单位，每次次读入或读出是8位数据。可以读任何类型数据。
  * 字符流：以字符为单位，每次次读入或读出是16位数据。其只能读取字符类型数据。
* **输出流和输入流：**
* * 输出流：从内存读出到文件。只能进行写操作。
  * 输入流：从文件读入到内存。只能进行读操作。

```
注意：这里的出和入，都是相对于系统内存而言的。
```

* **节点流和处理流：**
* * 节点流：直接与数据源相连，读入或读出。
  * 处理流：与节点流一块使用，在节点流的基础上，再套接一层，套接在节点流上的就是处理流。

```
为什么要有处理流？直接使用节点流，读写不方便，为了更快的读写文件，才有了处理流。
```

**按操作方式分类结构图**

![](/assets/import.png)

#### 分类二：按操作对象

#### ![](/assets/import2.png)

**分类说明：**

* 对文件进行操作（节点流）：
* * FileInputStream（字节输入流），
  * FileOutputStream（字节输出流），
  * FileReader（字符输入流），
  * FileWriter（字符输出流）
* 对管道进行操作（节点流）：
* * PipedInputStream（字节输入流）,
  * PipedOutStream（字节输出流），
  * PipedReader（字符输入流），
  * PipedWriter（字符输出流）。

    PipedInputStream的一个实例要和PipedOutputStream的一个实例共同使用，共同完成管道的读取写入操作。主要用于线程操作。
* 字节/字符数组流（节点流）：
* * ByteArrayInputStream，
  * ByteArrayOutputStream，
  * CharArrayReader，
  * CharArrayWriter；

    是在内存中开辟了一个字节或字符数组。

> 除了上述三种是节点流，其他都是处理流，需要跟节点流配合使用。

* Buffered缓冲流（处理流）：
* * BufferedInputStream，
  * BufferedOutputStream，
  * BufferedReader,
  * BufferedWriter,

    是带缓冲区的处理流，缓冲区的作用的主要目的是：避免每次和硬盘打交道，提高数据访问的效率。
* 转化流（处理流）：
* * InputStreamReader：把字节转化成字符；
  * OutputStreamWriter：把字节转化成字符。
* 基本类型数据流（处理流）：用于操作基本数据类型值。
* * DataInputStream，
  * DataOutputStream。

    因为平时若是我们输出一个8个字节的long类型或4个字节的float类型，那怎么办呢？可以一个字节一个字节输出，也可以把转换成字符串输出，但是这样转换费时间，若是直接输出该多好啊，因此这个数据流就解决了我们输出数据类型的困难。数据流可以直接输出float类型或long类型，提高了数据读写的效率。
* 打印流（处理流）：
* * PrintStream，
  * PrintWriter，

    一般是打印到控制台，可以进行控制打印的地方。
* 对象流（处理流）：
* * ObjectInputStream，对象反序列化；
  * ObjectOutputStream，对象序列化；

    把封装的对象直接输出，而不是一个个在转换成字符串再输出。
* 合并流（处理流）：
* * SequenceInputStream：可以认为是一个工具类，将两个或者多个输入流当成一个输入流依次读取。



