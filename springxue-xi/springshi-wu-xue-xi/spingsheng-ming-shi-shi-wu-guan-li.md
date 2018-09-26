## Spring事务管理

> ### Spring支持两种方式的事务管理：

* **编程式事务管理：**
   通过Transaction Template手动管理事务，实际应用中很少使用，
* **使用XML配置声明式事务：**
   推荐使用（代码侵入性最小），实际是通过AOP实现

> ### 实现声明式事务的四种方式：

1. **基于 TransactionInterceptor 的声明式事务:** Spring 声明式事务的基础，通常也不建议使用这种方式，但是与前面一样，了解这种方式对理解 Spring 声明式事务有很大作用。

2. **基于 TransactionProxyFactoryBean 的声明式事务:** 第一种方式的改进版本，简化的配置文件的书写，这是 Spring 早期推荐的声明式事务管理方式，但是在 Spring 2.0 中已经不推荐了。

3. **基于&lt; tx&gt; 和&lt; aop&gt;命名空间的声明式事务管理：** 目前推荐的方式，其最大特点是与 Spring AOP 结合紧密，可以充分利用切点表达式的强大支持，使得管理事务更加灵活。

4. **基于 @Transactional 的全注解方式：** 将声明式事务管理简化到了极致。开发人员只需在配置文件中加上一行启用相关后处理 Bean 的配置，然后在需要实施事务管理的方法或者类上使用 @Transactional 指定事务规则即可实现事务管理，而且功能也不必其他方式逊色。

**我们今天要将的是使用编程式以及基于AspectJ的声明式和基于注解的事务方式，实现烂大街的转账业务。**

再来说一下这个案例的思想吧，我们在两次转账之间添加一个错误语句（对应银行断电等意外情况），如果这个时候两次转账不能成功，则说明事务配置正确，否则，事务配置不正确。

> ### **你需要完成的任务：**

* **使用编程式事务管理完成转账业务**
* **使用基于AspectJ的声明式事务管理完成转账业务**
* **使用基于 @Transactional 的全注解方式事务管理完成转账业务**

  


作者：SnailClimb

  


链接：https://juejin.im/post/5b010f27518825426539ba38

  


来源：掘金

  


著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
