1.Exception 和Error都是java的错误处理机制,都继承了Throwable类。

Exception是正常程序运行中，可以预料到的情况，可以捕获并且可以进行处理的。

Error是非正常的情况，会导致程序处于不正常，不可恢复的状态，不可捕获，比如OutofMemoryError.

2.异常的分类

![](/assets/java2.png)

熟练的掌握异常是写好java程序的基础，我们要掌握Exception、 Error的设计和分类，了解常用的异常类。

try \(BufferedReader br = new BufferedReader\(…\);

     BufferedWriter writer = new BufferedWriter\(…\)\) {// Try-with-resources

// do something

catch \( IOException \| XEception e\) {// Multiple catch

   // Handle it

} 

三:使用原则

1.不要捕获通用异常，而要特定的异常

比如下面:

`try {`

`  // 业务代码`

`  // …`

`  Thread.sleep(1000L);`

`} catch (Exception e) {`

`  // Ignore it`

`}`

2.不要swallow异常，要记录异常的信息

  `  try {`

`   // 业务代码`

`   // …`

`} catch (IOException e) {`

`    e.printStackTrace();`

`}`

不要使用`e.printStackTrace(),`而是要把异常记录到日志中去.

3.try-catch代码性能比较低

会影响jvm对代码的优化，所以尽量不要用嗲吗包住一大块代码









