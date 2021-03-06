#### 一.什么是建造者模式

建造者模式（Builder Pattern**）** 又名生成器模式，是一种对象构建模式。它可以将复杂对象的建造过程抽象出来（抽象类别），使这个抽象过程的不同实现方法可以构造出不同表现（属性）的对象。

构建者模式是把复杂对象的过程和他的部件解耦.

**建造者模式** 是一步一步创建一个复杂的对象，它允许用户只通过指定复杂对象的类型和内容就可以构建它们，用户不需要知道内部的具体构建细节。

#### 二.建造者模式的优点和缺点

**1\) 客户端不必知道产品内部组成的细节，将产品本身与产品的创建过程解耦，使得相同的创建过程可以创建不同的产品对象。**

**2\)**每一个具体建造者都相对独立，而与其他的具体建造者无关，因此可以很方便地替换具体建造者或增加新的具体建造者，

**用户使用不同的具体建造者即可得到不同的产品对象 。**

**3\) 可以更加精细地控制产品的创建过程**。将复杂产品的创建步骤分解在不同的方法中，使得创建过程更加清晰，也更方便使用程序来控制创建过程。

**4\) 增加新的具体建造者无须修改原有类库的代码**，指挥者类针对抽象建造者类编程，系统扩展方便，符合**“开闭原则”**

#### 三.建造者模式的缺点

**\) 产品之间差异性很大的情况：**建造者模式所创建的产品一般具有较多的共同点，其组成部分相似，如果产品之间的差异性很大，则不适合使用建造者模式，因此其使用范围受到一定的限制。

**2\) 产品内部变化很复杂的情况：** 如果产品的内部变化复杂，可能会导致需要定义很多具体建造者类来实现这种变化，导致系统变得很庞大。

#### 四.实现

建造者模式总共有4个角色

Builder:创建产品的抽象接口  
ConcreateBuilder:具体构建者  
Producr:产品  
Directeor:指挥者,创建产品，隔离了客户端和对象d生产过程，负责控制产品的生产。

![](/assets/builder.png)

builder：构建接口

```
public interface Builder {


void build_CPU();

void build_mainboard();

 }
```

实现构建接口

```
public class ConreatorBuilder{
private Product product = new product();
 public void build_CPU(){

 }

 public void build_mainboard(){
 }

 }
```

指导者

```
 public class ProductDirector
 private Builder builder ;

 ProductDirector(Builder builder){
  builder = builder
 } 

  public Product newInstance(){
     builder.
     builder.
     return builder.getInstance()

  }

 }
```

总结:

构建者用于构建相对比较复杂的对象,使用者只需要通过Director角色来生成对象.

