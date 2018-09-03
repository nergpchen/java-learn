Spring AOP的核心是通过代理模式实现，目前支持两种代理：JDK动态代理、CGLIB代理来创建AOP代理

Spring建议优先使用JDK动态代理。默认情况下通过JDK动态代理实现。

JDK动态代理：使用java.lang.reflect.Proxy代理代理实现。 是基于接口实现的,就是对接口实现代理对象

CGLIB:是个开源的代码生成库，通过生成子类对象来创建代理。

所以学习SpringAOP的代理实现，首先要掌握JDK动态代理技术。

1.JDK动态代理技术

动态代理是指在运行的时候创建一个实现了多个接口的类，每个代理类的对象都会关联一个表示内部处理逻辑的InvocationHandler接口的实现。那么访问代理类的时候，不但可以访问被代理类的行为，并且可以在被代理类上增加一些功能，比如缓存，日志，记录性能，访问记录等动作,也就是说在访问代理类的时.

#### 2：怎么实现的？

#### java提供了Proxy类和InvocationHandler接口来支持动态代理。

Proxy类：提供用于创建动态代理类和实例对象的方法

比如：public static Object newProxyInstance\(ClassLoader loader, Class&lt;?&gt;\[\] interfaces, InvocationHandler h\)

上面代码通过传入类加载器，接口数字和 InvocationHandler接口来创建一个代理类，

而InvocationHandler其实具体调用处理者.

#### invocationHandler接口：

```
InvocationHandler is the interface implemented by the invocation handler of a proxy instance. 

Each proxy instance has an associated invocation handler. When a method is invoked on a proxy instance, the method invocation is encoded and dispatched to the invoke method of its invocation handler.
```

每一个动态代理类都必须要实现InvocationHandler这个接口，并且每个代理类的实例都关联到了一个handler，当我们通过代理对象调用一个方法的时候，这个方法的调用就会被转发为由InvocationHandler这个接口的 invoke 方法来进行调用。我们来看看InvocationHandler这个接口的唯一一个方法invoke方法：

```
Object invoke(Object proxy, Method method, Object[] args) 
throws
 Throwable
```

我们看到这个方法一共接受三个参数，那么这三个参数分别代表什么呢？

```
Object invoke(Object proxy, Method method, Object[] args)  throws Throwable

proxy :　　指代我们所代理的那个真实对象
method:　　指代的是我们所要调用真实对象的某个方法的Method对象
args:　　指代的是调用真实对象某个方法时接受的参数
```

代理 类的代码如下：

```
 Subejct sub = (Subject)Proxy.newProxyInstance(handler.getClass().getClassLoader(), realSubject
                .getClass().getInterfaces(), handler);
```

**通过 Proxy.newProxyInstance 创建的代理对象是在jvm运行时动态生成的一个对象，而是在运行是动态生成的一个对象，并且命名方式都是这样的形式，以$开头，proxy为中，最后一个数字表示对象的标号.**



