SpringIOC容器:

 Spring 启动时读取应用程序提供的Bean配置信息，并在Spring容器中生成一份相应的Bean配置注册表，然后根据这张注册表实例化Bean，装配好Bean之间的依赖关系，为上层应用提供准备就绪的运行环境

Spring 通过一个配置文件描述 Bean 及 Bean 之间的依赖关系，利用 Java 语言的反射功能实例化 Bean 并建立 Bean 之间的依赖关系。 Spring 的 IoC 容器在完成这些底层工作的基础上，还提供了 Bean 实例缓存、生命周期管理、 Bean 实例代理、事件发布、资源装载等高级服务。

Bean工厂结构:

![](/assets/beanfactory.png)

其中BeanFactory作为最顶层的一个接口类，它定义了IOC容器的基本功能规范，BeanFactory 有三个子类：ListableBeanFactory、HierarchicalBeanFactory 和AutowireCapableBeanFactory。

那为何要定义这么多层次的接口呢？  
   查阅这些接口的源码和说明发现，每个接口都有他使用的场合，它主要是为了区分在 Spring 内部在操作过程中对象的传递和转化过程中，对对象的数据访问所做的限制。例如 ListableBeanFactory 接口表示这些 Bean 是可列表的，而 HierarchicalBeanFactory 表示的是这些 Bean 是有继承关系的，也就是每个Bean 有可能有父 Bean。AutowireCapableBeanFactory 接口定义 Bean 的自动装配规则。这四个接口共同定义了 Bean 的集合、Bean 之间的关系、以及 Bean 行为

BeanFactory

```
1 
```

```
public interface  BeanFactory {    

对FactoryBean的转义定义，因为如果使用bean的名字检索FactoryBean得到的对象是工厂生成的对象，    
4
//
如果需要得到工厂本身，需要转义           
5
      String FACTORY_BEAN_PREFIX = 6
//
根据bean的名字，获取在IOC容器中得到bean实例    

      Object getBean(String name) throws BeansException;    

//
根据bean的名字和Class类型来得到bean实例，增加了类型安全验证机制。    
11
      Object getBean(String name, Class requiredType) throws BeansException;    


//
提供对bean的检索，看看是否在IOC容器有这个名字的bean    

      boolean containsBean(String name);    

//
根据bean名字得到bean实例，并同时判断这个bean是不是单例    
17
     boolean isSingleton(String name) throws NoSuchBeanDefinitionException;    

18
19
//
得到bean实例的Class类型    
20
     Class getType(String name) throws NoSuchBeanDefinitionException;    

21
22
//
得到bean的别名，如果根据别名检索，那么其原名也会被检索出来    
23
    String[] getAliases(String name); 
```

#### 二：ApplicationContext介绍

ApplicationContext 继承了 HierarchicalBeanFactory 和 ListableBeanFactory 接口，在此基础上，还通过多个其他的接口扩展了 BeanFactory 的功能：

* ClassPathXmlApplicationContext：默认从类路径加载配置文件

* FileSystemXmlApplicationContext：默认从文件系统中装载配置文件

* ApplicationEventPublisher：让容器拥有发布应用上下文事件的功能，包括容器启动事件、关闭事件等。实现了 ApplicationListener 事件监听接口的 Bean 可以接收到容器事件 ， 并对事件进行响应处理。   在 ApplicationContext 抽象实现类AbstractApplicationContext 中，我们可以发现存在一个 ApplicationEventMulticaster，它负责保存所有监听器，以便在容器产生上下文事件时通知这些事件监听者。

* MessageSource：为应用提供 i18n 国际化消息访问的功能；
* ResourcePatternResolver ： 所 有 ApplicationContext 实现类都实现了类似于PathMatchingResourcePatternResolver 的功能，可以通过带前缀的 Ant 风格的资源文件路径装载 Spring 的配置文件。
* LifeCycle：该接口是 Spring 2.0 加入的，该接口提供了 start\(\)和 stop\(\)两个方法，主要用于控制异步处理过程。在具体使用时，该接口同时被 ApplicationContext 实现及具体 Bean 实现， ApplicationContext 会将 start/stop 的信息传递给容器中所有实现了该接口的 Bean，以达到管理和控制 JMX、任务调度等目的。
* ConfigurableApplicationContext 扩展于 ApplicationContext，它新增加了两个主要的方法： refresh\(\)和 close\(\)，让 ApplicationContext 具有启动、刷新和关闭应用上下文的能力。在应用上下文关闭的情况下调用 refresh\(\)即可启动应用上下文，在已经启动的状态下，调用 refresh\(\)则清除缓存并重新装载配置信息，而调用close\(\)则可关闭应用上下文。这些接口方法为容器的控制管理带来了便利，但作为开发者，我们并不需要过多关心这些方法。



