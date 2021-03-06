#### 什么是原型模式

Specify the kind of objects to create using a prototypical instance, and create new objects by copying this prototype. （使用原型实例指定将要创建的对象类型，通过复制这个实例创建新的对象。）

也就是  首先创建一个对象，然后通过复制这个类来创建一个新类

优点 和缺点

1.通过 复制来创建对象，效率更高

2.可运行时指定动态创建的对象

缺点：

1.需要实现Cloneable接口,clone位于内部，不容易扩展

2.默认的clone只是浅拷贝,在实现深克隆时需要编写较为复杂的代码

使用 注意:

通过内存拷贝的方式构建出来的，会忽略构造函数限制

* 需要注意`深拷贝`
  和
  `浅拷贝`
  ，默认
  `Cloneable`
  是
  `浅拷贝`
  ，只拷贝当前对象而不会拷贝引用对象，除非自己实现
  `深拷贝`
* 与`单例模式`冲突，`clone`是直接通过`内存拷贝`的方式，绕过构造方法
* 常用克隆不可变对象,如果你克隆的对象10个字段改9个还不如实例化算了
* clone只是一个语法，非强制方法命名
* 很少单独出现，常与`工厂模式`相伴

角色

通过上面的例子，相信大家对于原型模式有了更进一步的认识，下面我们看看原型模式的几个登场角色。

3.1 Prototype（抽象原型类）

Product角色负责定义用于复制现有实例来生成新实例的方法。在示例程序中的Product接口就是该角色。

3.2 ConcretePrototype（具体原型类）

ConcretePrototype角色负责实现复制现有实例并生成新实例的方法。在示例程序中，MessageBox和UnderlinePen都是该角色。

3.3 Client（客户类/使用者）

Client角色负责使用复制实例的方法生成新的实例。在示例程序中，Manager类扮演的就是该角色。

应用场景

**1\) 对象种类繁多，无法将他们整合到一个类的时候；**

**2\) 难以根据类生成实例时；**

**3\) 想解耦框架与生成的实例时。**

如果想要让生成实例的框架不再依赖于具体的类，这时，不能指定类名来生成实例，而要事先“注册”一个“原型”实例，然后通过复制该实例来生成新的实例。

案例:

原文：[https://blog.csdn.net/qq\_34337272/article/details/80706444?utm\_source=copy](https://blog.csdn.net/qq_34337272/article/details/80706444?utm_source=copy)

