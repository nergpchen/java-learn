#### AOP的核心是如何织入代码.

Spring提供了两种方式来生成代理对象: JDKProxy和Cglib，具体使用哪种方式生成由AopProxyFactory根据AdvisedSupport对象的配置来决定。

如果目标类是接口，则使用JDK动态代理技术，否则使用Cglib来生成代理。

Spring提供了JdkDynamicAopProxy这个来实现动态代理技术，动态代理技术的核心是字节码增强技术，也就是在运行期间可以修改Class文件.

  


接口：

final class JdkDynamicAopProxy implements AopProxy, InvocationHandler, Serializable

是一个final类，不可被继承

实现了

AopProxy和InvocationHandler两个接口。

AopProxy用来指定一个代理类

InvocationHandler:每个代理类都有一个相应的InvocationHandler用来实现增强功能。

  


AOP接口实现：

public Object getProxy\(ClassLoader classLoader\) {

 if \(logger.isDebugEnabled\(\)\) {

logger.debug\("Creating JDK dynamic proxy: target source is " + this.advised.getTargetSource\(\)\);

 }

 Class

&lt;

?

&gt;

\[\] proxiedInterfaces = AopProxyUtils.completeProxiedInterfaces\(this.advised\);

 findDefinedEqualsAndHashCodeMethods\(proxiedInterfaces\);

 return Proxy.newProxyInstance\(classLoader, proxiedInterfaces, this\);

}

上面代码用来返回一个代理类

1:调用

AopProxyUtils.completeProxiedInterfaces\(\)来返回需要代理的接口

2:发现是否定义了equal和hashcode\(\)方法

3:调用 Proxy.newProxyInstance\(\)生成代理类

