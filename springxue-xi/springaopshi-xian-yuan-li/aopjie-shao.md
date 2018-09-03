#### 什么是AOP

AOP是面向切面编程,就是将那些与业务无关，却为业务模块所共同调用的逻辑或责任封装起来，便于减少系统的重复代码，降低模块间的耦合度，并有利于未来的可操作性和可维护性。

实现AOP的技术，主要分为两大类：

一是采用动态代理技术，利用截取消息的方式，对该消息进行装饰，以取代原有对象行为的执行；

二是采用静态织入的方式，引入特定的语法创建“方面”，从而使得编译器可以在编译期间织入有关“方面”的代码。

#### AOP使用场景：

Authentication 权限

Caching 缓存

Context passing 内容传递

Error handling 错误处理

Lazy loading　懒加载

Debugging　　调试

logging, tracing, profiling and monitoring　记录跟踪　优化　校准

Performance optimization　性能优化

Persistence　　持久化

Resource pooling　资源池

Synchronization　同步

Transactions 事务

#### AOP相关概念

切面 :切面就是一个功能的模块化，这个功能可以横切多个对象，比如日志管理、事务管理

连接点:Joinpoint ，是程序执行过程中明确的点，如方法的调用或特点的异常抛出,

通知:Advice:在特定的连接点执行的动作，比如许多AOP框架包括Spring都是以拦截器做通知模型，维护一个“围绕”连接点的拦截器链。Spring中定义了四个advice: BeforeAdvice, AfterAdvice, ThrowAdvice和DynamicIntroductionAdvice

切入点：Pointcut 。 定一个通知将被引发的一系列连接点的集合。AOP框架必须允许开发者指定切入点：例如，使用正则表达式。 Spring定义了Pointcut接口，用来组合MethodMatcher和ClassFilter，可以通过名字很清楚的理解， MethodMatcher是用来检查目标类的方法是否可以被应用此通知，而ClassFilter是用来检查Pointcut是否应该应用到目标类上

引入\(Introduction\):添加方法或字段到被通知的类。 Spring允许引入新的接口到任何被通知的对象。例如，你可以使用一个引入使任何对象实现 IsModified接口，来简化缓存。Spring中要使用Introduction, 可有通过DelegatingIntroductionInterceptor来实现通知，通过DefaultIntroductionAdvisor来配置Advice和代理类要实现的接口

目标 对象 \(Target Object\) : 包含连接点的对象。也被称作被通知或被代理对象。POJO

代理 对象\(AOP Prox\) :AOP框架创建的对象，包含通知。 在Spring中，AOP代理可以是JDK动态代理或者CGLIB代理

织入\(Weaving\) :组装方面来创建一个被通知对象。这可以在编译时完成（例如使用AspectJ编译器），也可以在运行时完成。Spring和其他纯Java AOP框架一样，在运行时完成织入。

切面 是一个要执行的公共模块的功能，连接点、切入点、通知和引入来定义在哪里切面，目标对象、代理对和织入来执行切面的功能。

总结起来：

\(1\)Aspect\(切面\):通常是一个类，里面可以定义切入点和通知

\(2\)JointPoint\(连接点\):程序执行过程中明确的点，一般是方法的调用

\(3\)Advice\(通知\):AOP在特定的切入点上执行的增强处理，有before,after,afterReturning,afterThrowing,around

\(4\)Pointcut\(切入点\):就是带有通知的连接点，在程序中主要体现为书写切入点表达式

\(5\)AOP代理：AOP框架创建的对象，代理就是目标对象的加强。Spring中的AOP代理可以使JDK动态代理，也可以是CGLIB代理，前者基于接口，后者基于子类











