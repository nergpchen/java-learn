什么是适配器模式

将1个类的接口转换成城另一个类希望的接口,使两个接口可以一起工作,具体就是重新创建1个类，包含类A的接口，同时提供接口供类B使用.

![](/assets/adapter.png)

#### 二:优点和缺点

#### 可以让任何两个没有关联的类一起运行

* 提高了类的复用，想使用现有的类，而此类的接口标准又不符合现有系统的需要。通过适配器模式就可以让这些功能得到更好的复用。
* 增加了类的透明度，客户端只关注结果
* 使用适配器的时候，可以调用自己开发的功能，从而自然地扩展系统的功能

过多使用会导致系统凌乱，追溯困难（内部转发导致，调用A适配成B）



#### 三使用场景

#### 系统需要使用一些现有的类，而这些类的接口（如方法名）不符合系统的需要，甚至没有这些类的源代码。

* 想创建一个可以重复使用的类，用于与一些彼此之间没有太大关联的一些类，包括一些可能在将来引进的类一起工作。



#### 四:案例

Java I/O 库大量使用了适配器模式，如`ByteArrayInputStream`是一个适配器类，它继承了`InputStream`的接口，并且封装了一个 byte 数组。换言之，它将一个 byte 数组的接口适配成 InputStream 流处理器的接口。

在`OutputStream`类型中，所有的原始流处理器都是适配器类。`ByteArrayOutputStream`继承了`OutputStream`类型，同时持有一个对 byte 数组的引用。它一个 byte 数组的接口适配成 OutputString 类型的接口，因此也是一个对象形式的适配器模式的应用。

`FileOutputStream`继承了`OutputStream`类型，同时持有一个对`FileDiscriptor`对象的引用。这是一个将`FileDiscriptor`接口适配成`OutputStream`接口形式的对象型适配器模式。

`Reader`类型的原始流处理器都是适配器模式的应用。`StringReader`是一个适配器类，`StringReader`类继承了`Reader`类型，持有一个对 String 对象的引用。它将 String 的接口适配成`Reader`类型的接口。





总结

引用 :https://segmentfault.com/a/1190000011856448\#articleHeader5



