1.**SpringMVC的流程？**

（1）用户发送请求至前端控制器DispatcherServlet；  
（2） DispatcherServlet收到请求后，调用HandlerMapping处理器映射器，请求获取Handle；  
（3）处理器映射器根据请求url找到具体的处理器，生成处理器对象及处理器拦截器\(如果有则生成\)一并返回给DispatcherServlet；  
（4）DispatcherServlet通过HandlerAdapter处理器适配器调用处理器；  
（5）执行处理器\(Handler，也叫后端控制器\)；  
（6）Handler执行完成返回ModelAndView；  
（7）HandlerAdapter将Handler执行结果ModelAndView返回给DispatcherServlet；  
（8）DispatcherServlet将ModelAndView传给ViewReslover视图解析器进行解析；  
（9）ViewReslover解析后返回具体View；  
（10）DispatcherServlet对View进行渲染视图（即将模型数据填充至视图中）  
（11）DispatcherServlet响应用户。



 --------------------- 本文来自 a745233700 的CSDN 博客 ，全文地址请点击：https://blog.csdn.net/a745233700/article/details/80963758?utm\_source=copy

**10、Spring MVC的异常处理 ？**

答：可以将异常抛给Spring框架，由Spring框架来处理；我们只需要配置简单的异常处理器，在异常处理器中添视图页面即可。



**11、SpringMvc的核心入口类是什么,Struts1,Struts2的分别是什么：**

答：SpringMvc的是DispatchServlet,Struts1的是ActionServlet,Struts2的是StrutsPrepareAndExecuteFilter。



**12、SpringMvc的控制器是不是单例模式,如果是,有什么问题,怎么解决？**

答：是单例模式,所以在多线程访问的时候有线程安全问题,不要用同步,会影响性能的,解决方案是在控制器里面不能写字段。



**13、SpingMvc中的控制器的注解一般用那个,有没有别的注解可以替代？**

答：一般用@Conntroller注解,表示是表现层,不能用用别的注解代替。



**14、 @RequestMapping注解用在类上面有什么作用？**

答：是一个用来处理请求地址映射的注解，可用于类或方法上。用于类上，表示类中的所有响应请求的方法都是以该地址作为父路径。



**15、怎么样把某个请求映射到特定的方法上面？**

答：直接在方法上面加上注解@RequestMapping,并且在这个注解里面写上要拦截的路径。



**16、如果在拦截请求中,我想拦截get方式提交的方法,怎么配置？**

答：可以在@RequestMapping注解里面加上method=RequestMethod.GET。



**17、怎么样在方法里面得到Request,或者Session？**

答：直接在方法的形参中声明request,SpringMvc就自动把request对象传入。



**18、如果想在拦截的方法里面得到从前台传入的参数,怎么得到？**

答：直接在形参里面声明这个参数就可以,但必须名字和传过来的参数一样。



**19、如果前台有很多个参数传入,并且这些参数都是一个对象的,那么怎么样快速得到这个对象？**

答：直接在方法中声明这个对象,SpringMvc就自动会把属性赋值到这个对象里面。



**20、SpringMvc中函数的返回值是什么？**

答：返回值可以有很多类型,有String, ModelAndView，但一般用String比较好。



**21、SpringMvc用什么对象从后台向前台传递数据的？**

答：通过ModelMap对象,可以在这个对象里面用put方法,把对象加到里面,前台就可以通过el表达式拿到。



**22、SpringMvc中有个类把视图和数据都合并的一起的,叫什么？**

答：叫ModelAndView。



**23、怎么样把ModelMap里面的数据放入Session里面？**

答：可以在类上面加上@SessionAttributes注解,里面包含的字符串就是要放入session里面的key。



**24、当一个方法向AJAX返回特殊对象,譬如Object,List等,需要做什么处理？**

答：要加上@ResponseBody注解。

 --------------------- 本文来自 a745233700 的CSDN 博客 ，全文地址请点击：https://blog.csdn.net/a745233700/article/details/80963758?utm\_source=copy

