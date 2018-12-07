1.**字节流和字符流的区别**

Byte是8位的,字符char是2个字节16位。字符是基于字节的编码，比如UTF-8编码、GB编码,

java的I/O有基于字节的接口InputStream和OutputStream.面向字符的接口Reader和Writer.

字节流在JDK1.0中就被引进了，用于操作包含ASCII字符的文件

JAVA语言设计者在JDK1.1中引入了字符流，可以读取取包含Unicode字符的文件

ASCII作为Unicode的子集，对于英语字符的文件，可以可以使用字节流也可以使用字符流。

**3.Java中流类的超类主要由那些？**

1. * java.io.InputStream

   * java.io.OutputStream

   * java.io.Reader

   * java.io.Writer

**4. FileInputStream和FileOutputStream是什么？**

这是在拷贝文件操作的时候，经常用到的两个类。在处理小文件的时候，它们性能表现还不错，

在大文件的时候，最好使用BufferedInputstream \(或 BufferedReader\) 和 BufferedOutputStream \(或 BufferedWriter\)

**5. 字节流和字符流，你更喜欢使用拿一个？**  
个人来说，更喜欢使用字符流，因为他们更新一些。许多在字符流中存在的特性，字节流中不存在。比如使用BufferedReader而不是BufferedInputStreams或DataInputStream，使用newLine\(\)方法来读取下一行，但是在字节流中我们需要做额外的操作。

`6.System.out.println()`**是什么？**  
`println`是PrintStream的一个方法。`out`是一个静态PrintStream类型的成员变量，`System`是一个java.lang包中的类，用于和底层的操作系统进行交互

**7.什么是Filter流？**

1. Filter Stream是一种IO流主要作用是用来对存在的流增加一些额外的功能，像给目标文件增加源文件中不存在的行数，或者增加拷贝的性能。

2. 在java.io包中主要由4个可用的filter Stream。两个字节filter stream，两个字符filter stream. 分别是FilterInputStream, FilterOutputStream, FilterReader and FilterWriter.这些类是抽象类，不能被实例化的。

8.**有哪些Filter流的子类**

LineNumberInputStream 给目标文件增加行号

DataInputStream 有些特殊的方法如`readInt()`, `readDouble()`和`readLine()` 等可以读取一个 int, double和一个string一次性的

BufferedInputStream 增加性能

PushbackInputStream 推送要求的字节到系统中

**9.SequenceInputStream的作用？**

这个类的作用是将多个输入流合并成一个输入流，通过SequenceInputStream类包装后形成新的一个总的输入流。在拷贝多个文件到一个目标文件的时候是非常有用的。可用使用很少的代码实现

**10. 在文件拷贝的时候，那一种流可用提升更多的性能？**

在字节流的时候，使用BufferedInputStream和BufferedOutputStream。

在字符流的时候，使用BufferedReader 和 BufferedWriter

**11 .说说管道流\(Piped Stream\)**  
有四种管道流， PipedInputStream, PipedOutputStream, PipedReader 和 PipedWriter.在多个线程或进程中传递数据的时候管道流非常有用。

**14. 说说RandomAccessFile?**

它在java.io包中是一个特殊的类，既不是输入流也不是输出流，它两者都可以做到。他是Object的直接子类。通常来说，一个流只有一个功能，要么读，要么写。但是RandomAccessFile既可以读文件，也可以写文件。 DataInputStream 和 DataOutStream有的方法，在RandomAccessFile中都存在。

