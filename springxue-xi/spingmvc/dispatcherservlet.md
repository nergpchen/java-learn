DispatcherServlet是前端控制器设计模式的实现，提供Spring Web MVC的集中访问点，而且负责职责的分派，而且与Spring IoC容器无缝集成，从而可以获得Spring的所有好处。 具体请参考第二章的图2-1。



DispatcherServlet主要用作职责调度工作，本身主要用于控制流程，主要职责如下：

1、文件上传解析，如果请求类型是multipart将通过MultipartResolver进行文件上传解析；

2、通过HandlerMapping，将请求映射到处理器（返回一个HandlerExecutionChain，它包括一个处理器、多个HandlerInterceptor拦截器）；

3、通过HandlerAdapter支持多种类型的处理器\(HandlerExecutionChain中的处理器\)；

4、通过ViewResolver解析逻辑视图名到具体视图实现；

5、本地化解析；

6、渲染具体的视图等；

7、如果执行过程中遇到异常将交给HandlerExceptionResolver来解析。



从以上我们可以看出DispatcherServlet主要负责流程的控制（而且在流程中的每个关键点都是很容易扩展的）。



## 3.2、DispatcherServlet在web.xml中的配置

```
<
servlet
>
<
servlet-name
>
chapter2
<
/servlet-name
>
<
servlet-class
>
org.springframework.web.servlet.DispatcherServlet
<
/servlet-class
>
<
load-on-startup
>
1
<
/load-on-startup
>
<
/servlet
>
<
servlet-mapping
>
<
servlet-name
>
chapter2
<
/servlet-name
>
<
url-pattern
>
/
<
/url-pattern
>
<
/servlet-mapping
>
```



**load-on-startup：**表示启动容器时初始化该Servlet；

**url-pattern：**表示哪些请求交给Spring Web MVC处理， “/” 是用来定义默认servlet映射的。也可以如“\*.html”表示拦截所有以html为扩展名的请求。



该DispatcherServlet默认使用WebApplicationContext作为上下文，Spring默认配置文件为“/WEB-INF/\[servlet名字\]-servlet.xml”。

