**Channel（通道）介绍**

Channel表示连接一个I/O对象，比如硬件设备、文件、网络Socket或者其他的I/O操作，通常来说NIO中的所有IO都是从 Channel（通道） 开始的。



NIO Channel通道和流的区别：

1. **FileChannel的使用**
2. **SocketChannel和ServerSocketChannel的使用**
3. **️DatagramChannel的使用**
4. **Scatter / Gather**
   * Scatter: 从一个Channel读取的信息分散到N个缓冲区中\(Buufer\).
   * Gather: 将N个Buffer里面内容按照顺序发送到一个Channel.
5. **通道之间的数据传输**
   * 在Java NIO中如果一个channel是FileChannel类型的，那么他可以直接把数据传输到另一个channel。
   * transferFrom\(\) :transferFrom方法把数据从通道源传输到FileChannel
   * transferTo\(\) :transferTo方法把FileChannel数据传输到另一个channel
6. Java NIO中最重要的几个Channel的实现：

   * **FileChannel：** 用于文件的数据读写

   * **DatagramChannel：** 用于UDP的数据读写

   * **SocketChannel：** 用于TCP的数据读写，一般是客户端实现

   * **ServerSocketChannel:** 允许我们监听TCP链接请求，每个请求会创建会一个SocketChannel，一般是服务器实现

**使用FileChannel读取数据到Buffer（缓冲区）以及利用Buffer（缓冲区）写入数据到FileChannel：**

```
package
 filechannel
;


import
 java
.
io
.
IOException
;

import
 java
.
io
.
RandomAccessFile
;

import
 java
.
nio
.
ByteBuffer
;

import
 java
.
nio
.
channels
.
FileChannel
;


public

class

FileChannelTxt

{


public

static

void
 main
(
String
 args
[])

throws

IOException

{


//1.创建一个RandomAccessFile（随机访问文件）对象，


RandomAccessFile
 raf
=
new

RandomAccessFile
(
"D:\\niodata.txt"
,

"rw"
);


//通过RandomAccessFile对象的getChannel()方法。FileChannel是抽象类。


FileChannel
 inChannel
=
raf
.
getChannel
();


//2.创建一个读数据缓冲区对象


ByteBuffer
 buf
=
ByteBuffer
.
allocate
(
48
);


//3.从通道中读取数据


int
 bytesRead 
=
 inChannel
.
read
(
buf
);


//创建一个写数据缓冲区对象


ByteBuffer
 buf2
=
ByteBuffer
.
allocate
(
48
);


//写入数据

        buf2
.
put
(
"filechannel test"
.
getBytes
());

        buf2
.
flip
();

        inChannel
.
write
(
buf
);


while

(
bytesRead 
!=

-
1
)

{



System
.
out
.
println
(
"Read "

+
 bytesRead
);


//Buffer有两种模式，写模式和读模式。在写模式下调用flip()之后，Buffer从写模式变成读模式。

            buf
.
flip
();


//如果还有未读内容


while

(
buf
.
hasRemaining
())

{


System
.
out
.
print
((
char
)
 buf
.
get
());


}


//清空缓存区

            buf
.
clear
();

            bytesRead 
=
 inChannel
.
read
(
buf
);


}


//关闭RandomAccessFile（随机访问文件）对象

        raf
.
close
();


}

}
```

## 三 SocketChannel和ServerSocketChannel的使用

**利用SocketChannel和ServerSocketChannel实现客户端与服务器端简单通信：**

**SocketChannel** 用于创建基于tcp协议的客户端对象，因为SocketChannel中不存在accept\(\)方法，所以，它不能成为一个服务端程序。通过 **connect\(\)方法** ，SocketChannel对象可以连接到其他tcp服务器程序。

客户端:

```

```

**ServerSocketChannel** 允许我们监听TCP链接请求，通过ServerSocketChannelImpl的 **accept\(\)方法** 可以创建一个SocketChannel对象用户从客户端读/写数据。

服务端：

```

```



