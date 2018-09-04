1.**使用ProxyFactoryBean创建AOP代理:**

在Spring里创建一个AOP代理的基本方法是使用_org.springframework.aop.framework.ProxyFactoryBean_。  
  这个类对应用的切入点和通知提供了完整的控制能力（包括它们的应用顺序）。像其它的`FactoryBean`实现一样，`ProxyFactoryBean`引入了一个间接层。如果你定义一个名为`foo`的`ProxyFactoryBean`， 引用`foo`的对象看到的将不是`ProxyFactoryBean`实例本身，而是一个`ProxyFactoryBean`实现里`getObject()`方法所创建的对象。 这个方法将创建一个AOP代理，它包装了一个目标对象。

`ProxyFactoryBean`类本身也是一个JavaBean，其属性主要有如下用途：

* 指定你希望代理的目标对象

* 指定是否使用CGLIB。



## 1.声明一个 aspect

Aspects 类和其他任何正常的 bean 一样，除了它们将会用 @AspectJ 注释之外，它和其他类一样可能有方法和字段，如下所示：

```

@Aspect

public class AspectModule {
}
```

它们将在 XML 中按照如下进行配置，就和其他任何 bean 一样：

```
<bean id="myAspect" class="org.xyz.AspectModule">
<
!-- configure properties of aspect here as normal --
>
</bean>
```



