Controller控制器，是MVC中的部分C，为什么是部分呢？因为此处的控制器主要负责功能处理部分：

1、收集、验证请求参数并绑定到命令对象；

2、将命令对象交给业务对象，由业务对象处理并返回模型数据；

3、返回ModelAndView（Model部分是业务对象返回的模型数据，视图部分为逻辑视图名）

二：相关注解：

`@Controller：用于标识是处理器类；`

`@RequestMapping：请求到处理器功能方法的映射规则；`

`@RequestParam：请求参数到处理器功能处理方法的方法参数上的绑定；`

`@ModelAttribute：请求参数到命令对象的绑定；`

`@SessionAttributes：用于声明session级别存储的属性，放置在处理器类上，通常列出`

`模型属性（如@ModelAttribute）对应的名称，`则这些属性会透明的保存到session中；

`@InitBinder：自定义数据绑定注册支持，用于将请求参数转换到命令对象属性的对应类型；`



**`三、Spring3.0引入RESTful架构风格支持(通过@PathVariable注解和一些其他特性支持),且又引入了`**

**`更多的注解支持：`**

`@CookieValue：cookie数据到处理器功能处理方法的方法参数上的绑定；`

`@RequestHeader：请求头（header）数据到处理器功能处理方法的方法参数上的绑定；`

`@RequestBody：请求的body体的绑定（通过HttpMessageConverter进行类型转换）；`

`@ResponseBody：处理器功能处理方法的返回值作为响应体（通过HttpMessageConverter进行类型转换）；`

`@ResponseStatus：定义处理器功能处理方法/异常处理器返回的状态码和原因；`

`@ExceptionHandler：注解式声明异常处理器；`

`@PathVariable：请求URI中的模板变量部分到处理器功能处理方法的方法参数上的绑定，`

`从而支持RESTful架构风格的URI；`

