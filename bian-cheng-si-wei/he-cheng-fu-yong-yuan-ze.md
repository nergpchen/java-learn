`合成复用原则`又称为组合/聚合复用原则\(Composition/Aggregate Reuse Principle, CARP\)，指尽量使用对象组合，而不是继承来达到复用的目的。

> 为什么要**尽量使用合成和聚合，而不用继承**？

* 继承复用破坏包装，它把父类的实现细节直接暴露给了子类，父类发生改变，则子类也要发生相应的改变，这就直接导致了类之间的紧耦合，不利于类的扩展、复用、维护。
* 合成与聚合的时候，对象交互往往是通过接口或抽象类进行的，可以很好的避免上面的不足，每个新的类专注于实现自己的任务，符合单一职责原则。

合成复用原则





