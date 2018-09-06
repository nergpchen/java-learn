ApplicationContext是Spring一个功能齐全的IOC容器。

IOC容器初始化过程：

IoC容器的初始化包括BeanDefinition的Resource定位、载入和注册这三个基本的过程.

以ClassPathXmlApplicationContext为例来说明

```
public
```

```
void
 refresh() 
throws
 BeansException, IllegalStateException {
        
synchronized
 (
this
.startupShutdownMonitor) {
            
//
1.准备刷新的上下文环境，例如对系统属性或者环境变量进行准备及验证。
            prepareRefresh();
            
//2.初始化BeanFactory，并进行XML文件读取，这一步之后，ClassPathXmlApplicationContext实际上就已经包含了BeanFactory所提供的功能，也就是可以进行Bean的提取等基础操作了。

            ConfigurableListableBeanFactory beanFactory =
 obtainFreshBeanFactory();
            
//3.对BeanFactory进行各种功能填充,@Qualifier与@Autowired这两个注解正是在这一步骤中增加的支持。
            //设置@Autowired和 @Qualifier注解解析器QualifierAnnotationAutowireCandidateResolver


　　　　　　　prepareBeanFactory(beanFactory);
            
try
 {
                
//
子类覆盖方法做额外的处理,提供了一个空的函数实现postProcessBeanFactory来方便程序员在业务上做进一步扩展。
                postProcessBeanFactory(beanFactory);
                
//
激活各种BeanFactory处理器
                invokeBeanFactoryPostProcessors(beanFactory);
                
//
注册拦截Bean创建的Bean处理器,这里只是注册，真正的调用是在getBean时候
                registerBeanPostProcessors(beanFactory);
                
//
为上下文初始化Message源，即不同语言的消息体进行国际化处理
                initMessageSource();
                
//
初始化应用消息广播器，并放入“applicationEventMulticaster”bean中
                initApplicationEventMulticaster();
                
//
留给子类来初始化其它的Bean
                onRefresh();
                
//
在所有注册的bean中查找Listener bean，注册到消息广播器中
                registerListeners();
                
//
初始化剩下的单实例（非惰性的）
                finishBeanFactoryInitialization(beanFactory);
                
//
完成刷新过程，通知生命周期处理器lifecycleProcessor刷新过程，同时发出ContextRefreshEvent通知别人
                finishRefresh();
            }
            
finally
 {
                
//
 Reset common introspection caches in Spring's core, since we
                
//
 might not ever need metadata for singleton beans anymore...
                resetCommonCaches();
            }
        }
    }
```

启动 过程：

1创建 Bean 容器前的准备工作  
2.创建Bean容器,加载并且注册Bean  
3:初始化所有的 singleton beans

  




