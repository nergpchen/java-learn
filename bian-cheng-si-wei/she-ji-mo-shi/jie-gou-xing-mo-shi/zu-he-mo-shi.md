什么是组合模式

将对象组合成树形结构以表示”部分-整体”的层次结构。组合模式使得用户对单个对象和组合对象的使用具有一致性,

使得客户能够像处理简单元素一样来处理复杂元素，从而使客户程序能够与复杂元素的内部结构解耦。

优点:

* 可以清楚地定义分层次的复杂对象，表示对象的全部或部分层次，使得增加新构件也更容易

* 客户端调用简单，客户端可以一致的使用组合结构或其中单个对象。

* 更容易在组合体内加入对象构件，客户端不必因为加入了新的对象构件而更改原有代码。

缺点:

设计变得更加抽象，业务规则复杂的对象，组合模式实现就越困难，且不是所有的方法都与叶子对象子类都有关联

适用场景:

```
 需要表示一个对象整体或部分层次，在具有整体和部分的层次结构中，希望通过一种方式忽略整体与部分的差异，可以一致地对待它们。
```

* 让客户能够忽略不同对象层次的变化，客户端可以针对抽象构件编程，无须关心对象层次结构的细节。

#### 组合模式结构:

#### ![](/assets/composite.png)

#### 角色:

Component（组合对象）：为组合中的对象声明接口，在适当的情况下，实现所有类共有接口的默认行为，声明用于访问和管理其子组件的接口。

* Leaf（叶子对象）：定义组合中原始对象的行为，叶子节点下再无节点
* Composite（容器对象）：定义所有节点行为，存储子组件，在
  `Component接口`
  中实现与子组件有关操作，如增加\(add\)和删除\(remove\)等。

### JDK中的用法 {#JDK中的用法}

* java.util.Map\#putAll\(Map\)
* java.util.List\#addAll\(Collection\)
* java.util.Set\#addAll\(Collection\)
* java.nio.ByteBuffer\#put\(ByteBuffer\) \(CharBuffer, ShortBuffer, IntBuffer, LongBuffer, FloatBuffer, DoubleBuffer\)



引用:https://blog.battcn.com/2017/11/13/java/design-pattern/composite-pattern/  




