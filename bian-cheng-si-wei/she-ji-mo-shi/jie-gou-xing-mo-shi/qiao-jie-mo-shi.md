#### 什么 是桥接模式

桥接模式是一种很实用的，如果软件系统中某个类存在两个独立变化的维度，通过该模式可以将这两个维度分离出来，使两者可以独立扩展，让系统更加符合“单一职责原则”。与多层继承方案不同，它将两个独立变化的维度设计为两个独立的继承等级结构，并且在抽象层建立一个抽象关联，该关联关系类似一条连接两个独立继承结构的桥，故名桥接模

#### 桥接 模式优缺点

#### 桥接模式用一种巧妙的方式处理多层继承存在的问题，`用抽象关联取代了传统的多层继承`，将类之间的静态继承关系转换为动态的对象组合关系，使得系统更加灵活，并易于扩展。

* **对象间的组合关系**
  解耦了抽象和实现之间固有的绑定关系，使得抽象和实现可以沿着各自的维度来变化。
* 所谓抽象和实现沿着各自维度的变化，即
  **子类化**
  它们，得到各个子类之后，便可以任意它们，从而获得不同路上的不同汽车。
* Bridge模式有时候类似于多继承方案，但是多继承方案往往违背了类的单一职责原则（即一个类只有一个变化的原因），复用性比较差。Bridge模式是比多继承方案更好的解决方法。
* Bridge模式的应用一般在
  **两个非常强的变化维度**
  ，有时候，即使两个维度存在变化，但是变化的地方影响并不大，换而言之两个变化不会导致纵横交错的结果，并不一定要使用Bridge模式。

#### 桥接模式角色

1.Client 调用端

这是Bridge模式的调用者。

2.抽象类（Abstraction）

抽象类接口（接口这货抽象类）维护队行为实现（implementation）的引用。它的角色就是桥接类。

3.Refined Abstraction

这是Abstraction的子类。

4.Implementor

行为实现类接口（Abstraction接口定义了基于Implementor接口的更高层次的操作）

5.ConcreteImplementor

Implementor的子类

#### 桥接模式适用场景

1. #### 如果一个系统需要在构件的抽象化角色和具体化角色之间增加更多的灵活性，避免在两个层次之间建立静态的联系。
2. 设计要求实现化角色的任何改变不应当影响客户端，或者说实现化角色的改变对客户端是完全透明的。

3. 一个构件有多于一个的抽象化角色和实现化角色，系统需要它们之间进行动态耦合。
4. 虽然在系统中使用继承是没有问题的，但是由于抽象化角色和具体化角色需要独立变化，设计要求需要独立管理这两者。

实现代码:

1.接口

```
public interface Implementor {

public  void
 operation();

 }
```

下面定义Implementor接口的两个实现类：

```
1
public class ConcreateImplementorA implements Implementor {

@Override public void operation() {

         System.out.println("this is concreteImplementorA's operation..."
);


    }

 }
```

```
public class ConcreateImplementorB  implements
 Implementor {

@Override
public void operation() {


         System.out.println("this is concreteImplementorB's operation..."
);


    }

 }
```

下面定义桥接类Abstraction，其中有对Implementor接口的引用：

[![](https://common.cnblogs.com/images/copycode.gif "复制代码")](javascript:void%280%29;)

```
 1
public abstract class Abstraction {

private Implementor implementor;

public  Implementor getImplementor() {

return implementor;

}

public void
 setImplementor(Implementor implementor) {

this .implementor = implementor;
}
protected  void operation(){

        implementor.operation();


    }

 }

```

下面是Abstraction类的子类RefinedAbstraction：

```
1
public class RefinedAbstraction  extends Abstraction {

@Override
protected void
 operation() {
super.getImplementor().operation();

}
 }
```

案例

引用:

[http://blog.battcn.com/2017/11/09/java/design-pattern/brideg-pattern/\#合成复用原则](http://blog.battcn.com/2017/11/09/java/design-pattern/brideg-pattern/#合成复用原则)

