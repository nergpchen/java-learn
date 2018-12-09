设计模式学习

什么是设计模式？

我们学习设计模式是为了什么？

有哪些设计模式？

如何运用这些设计模式?

什么是设计模式？

设计模式是一套被反复使用的、多数人知晓的、经过分类编目的、代码设计经验的总结。

使用设计模式是为了重用代码、让代码更容易被他人理解、保证代码可靠性。

#### 设计原则：

面向对象有几个原则：

[单一职责原则](https://baike.baidu.com/item/单一职责原则)

（Single Responsiblity Principle SRP）

[开闭原则](https://baike.baidu.com/item/开闭原则)

（Open Closed Principle，OCP）、

[里氏代换原则](https://baike.baidu.com/item/里氏代换原则)

（Liskov Substitution Principle，LSP）、

[依赖倒转原则](https://baike.baidu.com/item/依赖倒转原则)

（Dependency Inversion Principle，DIP）、

[接口隔离原则](https://baike.baidu.com/item/接口隔离原则)

（Interface Segregation Principle，ISP）、合成/聚合复用原则（Composite/Aggregate Reuse Principle，CARP）、最小知识原则（Principle of Least Knowledge，PLK，也叫

[迪米特法则](https://baike.baidu.com/item/迪米特法则)

#### 1.单一职责原则

单一职责原则是说一个类\(接口、结构体、方法\)而言，应该仅有一个引起它变化的原因.，该负责一个功能，而不是多个功能，简化类的复杂程度.

因为 软件设计要做的内容就是发现职责，并且把这些职责分离开来。  
单一职责原则可以使类的复杂度降低，实现什么职责都有清晰明确的定义；  
类的可读性提高，复杂度降低（复杂度降低肯定可读性提高）；  
可读性提高了，代码就更容易维护；  
变更（需求是肯定会变的，程序员都知道）引起的风险（包括测试的难度，以及需要测试的范围）降低。

2.开闭原则

开闭原则是设计模式的基石,是最重要的原则，那么为什么那么重要呢？

开闭 是说软件中包含的各种功能应该在不修改代码的情况下扩展，开指的是可以扩展功能，闭指的是不能修改原有的代码.

这个听起来也是非常难的，如何在不修改代码的情况下，扩展功能呢？





