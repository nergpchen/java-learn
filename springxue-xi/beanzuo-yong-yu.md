**Spring中的bean默认都是单例的，这些单例Bean在多线程程序下如何保证线程安全呢？**

Bean作用域: 分为单例、prototype、request、session、globalSession

![](/assets/bean.png)

一:singleton

在Spring容器中，只有1个Bean实例，称之为singleton.在Spring中，默认都是singleton.

二:prototype:

**prototype 作用域的 bean 会导致在每次对该 bean 请求**

（将其注入到另一个 bean 中，或者以程序的方式调用容器的 getBean\(\) 方法\*\*）时都会创建一个新的 bean 实例。prototype 是原型类型，它在我们创建容器的时候并没有实例化，而是当我们获取bean的时候才会去创建一个对象，而且我们每次获取到的对象都不是同一个对象

根据经验，对有状态的 bean 应该使用 prototype 作用域，而对无状态的 bean 则应该使用 singleton 作用域。\*\* 在 XML 中将 bean 定义成 prototype ，可以这样配置：

通过 注解@Scope\("prototype"\)来声明作用域



### 二：bean的生命周期

Spring Bean是Spring应用中最最重要的部分了。所以来看看Spring容器在初始化一个bean的时候会做那些事情，顺序是怎样的，在容器关闭的时候，又会做哪些事情。

1.初始化和销毁

**2.在bean的配置文件中指定init-method和destroy-method方法**

Spring允许我们创建自己的 init 方法和 destroy 方法，只要在 Bean 的配置文件中指定 init-method 和 destroy-method 的值就可以在 Bean 初始化时和销毁之前执行一些操作。

例子如下：

```
public
class
GiraffeService
 {
    
//
通过
<
bean
>
的destroy-method属性指定的销毁方法
public
void
destroyMethod
() 
throws
Exception
 {
        
System
.
out
.
println(
"
执行配置的destroy-method
"
);
    }
    
//
通过
<
bean
>
的init-method属性指定的初始化方法
public
void
initMethod
() 
throws
Exception
 {
        
System
.
out
.
println(
"
执行配置的init-method
"
);
    }
}
```

配置文件中的配置：

```
<
bean name="giraffeService" class="com.giraffe.spring.service.GiraffeService" init-method="initMethod" destroy-method="destroyMethod"
>
<
/bean
>
```



**3.使用@PostConstruct和@PreDestroy注解**

除了xml配置的方式，Spring 也支持用`@PostConstruct`和`@PreDestroy`注解来指定`init`和`destroy`方法。这两个注解均在`javax.annotation`包中.了注解可以生效，需要在配置文件中定义org.springframework.context.annotation.CommonAnnotationBeanPostProcessor或context:annotation-config

```
<bean class ="org.springframework.context.annotation.CommonAnnotationBeanPostProcessor" />
```

所以。。。结合第一节控制台输出的内容，Spring Bean的生命周期是这样纸的：

* Bean容器找到配置文件中 Spring Bean 的定义。
* Bean容器利用Java Reflection API创建一个Bean的实例。
* 如果涉及到一些属性值 利用set方法设置一些属性值。
* 如果Bean实现了BeanNameAware接口，调用setBeanName\(\)方法，传入Bean的名字。
* 如果Bean实现了BeanClassLoaderAware接口，调用setBeanClassLoader\(\)方法，传入ClassLoader对象的实例。
* 如果Bean实现了BeanFactoryAware接口，调用setBeanClassLoader\(\)方法，传入ClassLoader对象的实例。
* 与上面的类似，如果实现了其他\*Aware接口，就调用相应的方法。
* 如果有和加载这个Bean的Spring容器相关的BeanPostProcessor对象，执行postProcessBeforeInitialization\(\)方法
* 如果Bean实现了InitializingBean接口，执行afterPropertiesSet\(\)方法。
* 如果Bean在配置文件中的定义包含init-method属性，执行指定的方法。
* 如果有和加载这个Bean的Spring容器相关的BeanPostProcessor对象，执行postProcessAfterInitialization\(\)方法
* 当要销毁Bean的时候，如果Bean实现了DisposableBean接口，执行destroy\(\)方法。
* 当要销毁Bean的时候，如果Bean在配置文件中的定义包含destroy-method属性，执行指定的方法。

  


  




