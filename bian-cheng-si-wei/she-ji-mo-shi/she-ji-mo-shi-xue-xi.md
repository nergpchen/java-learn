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

[单一职责原则](https://baike.baidu.com/item/%E5%8D%95%E4%B8%80%E8%81%8C%E8%B4%A3%E5%8E%9F%E5%88%99)

（Single Responsiblity Principle SRP）

[开闭原则](https://baike.baidu.com/item/%E5%BC%80%E9%97%AD%E5%8E%9F%E5%88%99)

（Open Closed Principle，OCP）、

[里氏代换原则](https://baike.baidu.com/item/%E9%87%8C%E6%B0%8F%E4%BB%A3%E6%8D%A2%E5%8E%9F%E5%88%99)

（Liskov Substitution Principle，LSP）、

[依赖倒转原则](https://baike.baidu.com/item/%E4%BE%9D%E8%B5%96%E5%80%92%E8%BD%AC%E5%8E%9F%E5%88%99)

（Dependency Inversion Principle，DIP）、

[接口隔离原则](https://baike.baidu.com/item/%E6%8E%A5%E5%8F%A3%E9%9A%94%E7%A6%BB%E5%8E%9F%E5%88%99)

（Interface Segregation Principle，ISP）、合成/聚合复用原则（Composite/Aggregate Reuse Principle，CARP）、最小知识原则（Principle of Least Knowledge，PLK，也叫

[迪米特法则](https://baike.baidu.com/item/%E8%BF%AA%E7%B1%B3%E7%89%B9%E6%B3%95%E5%88%99)

1. 单一职责原则：

    单一职责原则是说一个类\(接口、结构体、方法\)而言，应该仅有一个引起它变化的原因.，该负责一个功能，而不是多个功能，简化类的复杂程度.

因为 软件设计要做的内容就是发现职责，并且把这些职责分离开来。  
单一职责原则可以使类的复杂度降低，实现什么职责都有清晰明确的定义；  
类的可读性提高，复杂度降低（复杂度降低肯定可读性提高）；  
可读性提高了，代码就更容易维护；  
变更（需求是肯定会变的，程序员都知道）引起的风险（包括测试的难度，以及需要测试的范围）降低。





