NIO和IO的差别：

IO :面向流  阻塞 无选择器

NIO:面向缓冲 非阻塞 有选择器



**面向流与面向缓冲**

IO面向流,NIO面向缓冲的。 

Java IO面向流意味着每次从流中读一个或多个字节，直至读取所有字节，它们没有被缓存在任何地方.

Java NIO的缓冲导向方法略有不同。数据读取到一个它稍后处理的缓冲区，需要时可在缓冲区中前后移动。这就增加了处理过程中的灵活性。但是，还需要检查是否该缓冲区中包含所有您需要处理的数据。而且，需确保当更多的数据读入缓冲区时，不要覆盖缓冲区里尚未处理的数据



**阻塞与非阻塞IO**

Java IO的各种流是阻塞的。这意味着，当一个线程调用read\(\) 或 write\(\)时，该线程被阻塞，直到有一些数据被读取，或数据完全写入。该线程在此期间不能再干任何事情了。 Java NIO的非阻塞模式，使一个线程从某通道发送请求读取数据，但是它仅能得到目前可用的数据，如果目前没有数据可用时，就什么都不会获取。而不是保持线程阻塞，所以直至数据变的可以读取之前，该线程可以继续做其他的事情。 非阻塞写也是如此。一个线程请求写入一些数据到某通道，但不需要等待它完全写入，这个线程同时可以去做别的事情。 线程通常将非阻塞IO的空闲时间用于在其它通道上执行IO操作，所以一个单独的线程现在可以管理多个输入和输出通道（channel）。

阻塞IO :   线程在读写操作的时候不能做其他事情，直到IO完成

非阻塞IO: 线程在读写操作的时候，可以做其他的事情

**选择器（**Selectors**）**

Java NIO的选择器允许一个单独的线程来监视多个输入通道，你可以注册多个通道使用一个选择器，然后使用一个单独的线程来“选择”通道：这些通道里已经有可以处理的输入，或者选择已准备写入的通道。这种选择机制，使得一个单独的线程很容易来管理多个通道

## **数据处理**

使用纯粹的NIO设计相较IO设计，数据处理也受到影响。

在IO设计中，我们从InputStream或 Reader逐字节读取数据。假设你正在处理一基于行的文本数据流，例如：

> InputStream input = … ; // get the InputStream from the client socket

> 1 BufferedReader reader = **new** BufferedReader\(**new** InputStreamReader\(input\)\);
>
> 2
>
> 3 String nameLine   = reader.readLine\(\);
>
> 4 String ageLine    = reader.readLine\(\);
>
> 5 String emailLine  = reader.readLine\(\);
>
> 6 String phoneLine  = reader.readLine\(\);



  
p.p1 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px '.PingFang SC'; color: \#454545}  
p.p2 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px '.PingFang SC'; color: \#e4af0a}  
p.p3 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px 'Helvetica Neue'; color: \#454545; min-height: 14.0px}  
p.p4 {margin: 0.0px 0.0px 0.0px 0.0px; font: 12.0px 'Helvetica Neue'; color: \#454545}  
span.s1 {font: 12.0px 'Helvetica Neue'}  
span.s2 {text-decoration: underline}  
span.s3 {font: 12.0px '.PingFang SC'}  
span.Apple-tab-span {white-space:pre}  


而一个NIO的实现会有所不同，下面是一个简单的例子：

> 1 ByteBuffer buffer = ByteBuffer.allocate\(48\);
>
>  2 **int** bytesRead = inChannel.read\(buffer\);
>
> **while**\(! bufferFull\(bytesRead\)\) {

> 7 bytesRead = inChannel.read\(buffer\);

> 9 }

数据是读到缓冲区，所以必须要时刻检查缓冲区，直到读取万为止.





