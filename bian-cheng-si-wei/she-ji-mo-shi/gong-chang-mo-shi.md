#### 一.什么是工厂模式

Define an interface for creating an object, but let subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.”\(在基类中定义创建对象的一个接口，让子类决定实例化哪个类。工厂方法让一个类的实例化延迟到子类中进行.

工厂模式就是提供创建对象的接口，是常见的创建对象的模式，可以把对象的创建和使用分离开了，提供代码的扩展性和复用程度.

工厂模式分为简单工厂模式、工厂方法模式、抽象工厂模式.在Spring中容器工厂用的就是工厂模式。

#### 二.工厂模式的好处

   1.解耦：把对象的创建和使用分开  
   2.降低代码重复:  
   3.降低维护成本  
   4.把产品和需求分开

#### 三.怎么实现

一个工厂模式有4个角色：

```
       1.抽象工厂角色:是工厂方法模式的核心，与应用程序无关。任何在模式中创建的对象的工厂类必须实现这个接口。

       2.具体工厂角色:这是实现抽象工厂接口的具体工厂类，包含与应用程序密切相关的逻辑，并且受到应用程序调用以创建某一种产品对象。

       3.抽象产品角色: 工厂方法模式所创建的对象的超类型，也就是产品对象的共同父类或共同拥有的接口。

       4.具体产品角色: 这个角色实现了抽象产品角色所定义的接口。某具体产品有专门的具体工厂创建，它们之间往往一一对应
```

抽象工厂:

`public interface Factory {`

`public Shape getShape();`

`}`

具体工厂：

`public class CircleFactory implements Factory {`

`@Override`

`public Shape  getShape() {`

`// TODO Auto-generated method stub`

`return new`

`Circle();`

`} }`

**）测试：**

```
public class Test {
public static void main (String[] args) {
        Factory circlefactory =  new  CircleFactory();
        Shape circle = circlefactory.getShape();
        circle.draw();
    }

}
```

四:实用场景

五.

引用:http://blog.jobbole.com/109594/

