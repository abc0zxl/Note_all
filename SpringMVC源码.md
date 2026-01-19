# 注意

1.**查找依赖文件**：双击shift

2.**查找当前文件接口方法**：也就是这个方法的原java文件在外面，ctrl+f12

3.**查找当前文件调用方法的方法类**：按住ctrl鼠标左键。

# DispacherServlet

#### **控制器**：

例如：DispatcherServlet，他是springMVC的入口，是一个标准的HttpServlet，这个控制器更准确的说法是**前端控制器**

**作用**：接受所有客户端的HTTP请求，负责请求全局调度（分发，协调各个组件），不处理具体业务逻辑，只是个**总指挥**

**核心方法**：doDispatch(request,response),一次http请求就会调用一次doDispach,整个请求的处理流程等都在这个方法中展开

#### **处理器**：

**解释**：真正处理**具体业务逻辑**的组件，就是@controller标注的方法

**作用**：接受请求参数，处理业务逻辑，返回处理结果

**处理器执行链**：就是将处理器和拦截器绑定在一起，确保拦截器能按顺序围绕处理器执行

#### **拦截器**：

**解释**：是Springmvc提供的增强组件，是一个接口，用户可自定义实现，用于在处理器执行气候做统一的额外处理。

#### **解析器**：

解析器有很多种，例如视图解析器、处理器异常解析器等，

**介绍**：他是一个接口，负责将**逻辑视图名**转换为**物理视图对象**。

**关键词**：

* InternalResourceViewResolver：这个是SpringMVC内置的，用于解析JSP视图，
* ThymeleafViewResolver：是Thymeleaf框架提供的，用于解析Thymeleaf模板，

**代码**：resulveViewNane（）

#### **适配器**：

**解释**：是一个接口，不同类型的Handler对应不同的实现类

**作用**：因为Handler只是一个**业务方法**，DispatcherServlet无法直接执行，而适配器就可以解决这个问题，采用处理器适配器来适配执行。

**作用**：充当**翻译官**，**执行者**的作用。

**代码**：getHandlerAdapter(mappedHandler.getHandler())，会根据get到的Handler类型，查找到适配他的HandlerAdapter适配器

#### **视图**：

他是一个接口，代表物理视图对象，对应具体的试图格式JSP，Thymeleaf，JSON

**主流的视图实现类**：

1.**InternalResourceView**：

2.**ThymeleafView**：

### 组件

**HandlerMapping**：处理器映射器

**Handler**：处理器

**HandlerInterceptor**：拦截器

**HandlerExecutionChain**：处理器执行链

**MultipartResolver**：文件上传解析器

**HandlerAdapter**：处理器适配器

**ModelAndView**：结果封装对象

**ViewResolver**：视图解析器

**HandlerMethod**：处理器方法对象，他在web服务器启动时**初始化Spring**时就创建好了，它还包含两个重要属性，**beanName，Method**

* **beanName**：这个时控制器的类的名字，定位到某个controller，java文件

1.**前端控制器的核心方法**：doDispatch，一次请求调用一次

**通过请求获取一个处理器（）**：

HandlerExecutionChain mappedHandler=getHandler(request);

* 这里的mappedHandler.getHadnler就是通过这个请求获取处理器。这个getHandler方法中有一个HandlerMapping接口，是处理器映射器，他会根据请求路径去映射处理器方法。这个接口有很多方法，其中RequestMappingHandlerMapping是注解@RequestMapping的专用处理器映射器对象
* 内部还有一个for循环来寻找HanlderMapping,只有合适的HandlerMapping才会获取到HandlerExecutionChain对象
* 这个处理器相当于一个执行链，将要执行的所有拦截器和处理器串在一起
* 一次请求串一次，也就是对应一个处理器对象。
* **最后封装为了HandlerExecutionChain**，这个里有两个属性，

  **一个是**：HandlerMethod（）这个是一个处理器的方法对象。

  **一个是**：List<HandlerInterceptor这个是数组用于存储拦截器

2.**获取处理器适配器对象**：

HandlerAdapter ha=getHandlerAdapter(mappedHandler.getHandler())

* 这里面的mappedHandler.getHandler是获取处理器适配器对象

**执行该请求对应的所有拦截器中的preHandle方法**：

if(!mappedHandler.applyPreHandle(processedRequest,response)){return};

**调用映射的处理器**：处理结束后返回逻辑视图名称，

mv=ha.handle(processedRequest,response,mappedHandler.getHandler());

**执行该请求的所有拦截器中的postHandle方法**：

mappedHandler.applyPostHandle(processdRequest,response,mv);

3.**处理试图的代码**：处理分发结果，响应到浏览器用于渲染页面

processDispatchResult(processedRequest,reponse,mappedHandler,mv,hdisptchException);

4.**渲染页面**：render(mv，request,response);这个是上面的方法中的一行代码，实现它处理视图的功能，是正真整合了转换，响应，渲染的方法

* **逻辑视图转换为物理视图**：这个方法也是上面的render中的方法view=resolveViewName(viewName,mv.getModelInternal(),locale,request).
* **调用视图对象的渲染方法**：
  view.render(mv.getModelInternal(),request,response)
* **上面的View接口**：

  View
* **上面的resolveViewName方法**：

  **第一步**：resolveViewName();这个内部又实现的是**视图解析器**，创建了一个对象ViewResolver viewResolver;

  **第二步**：通过这个视图解析器对象，解析视图返回视图对象

  View view=viewResolver.resolveViewName(viewName,locale);
* **上面的ViewResolver**：这个是一个接口，他有ThymeleafViewResolver和InternalResourceViewResolver
* f
* f

**执行拦截器的aftercompletion方法**：这个也是processDispatchResult方法中的。

mappedHandler.triggerAfterCompletion(request,response,null)

6.**视图解析器**：这个代码也是上面的的方法中的一个方法，**他是真正起作用的代码，上面都是嵌套**

这里的viewResolver是一个接口，他会自动创建一个thymeleafViewResolver

这个ViewResolver接口就是最底层的实现，实现转换，和返回我上面说的对不对

j

**拦截器**：

**解析器**：

**适配器**：

1.**前端控制器的核心方法**：doDispatch，一次请求调用一次

**通过请求获取一个处理器（）**：

HandlerExecutionChain mappedHandler=getHandler(request);

* 这里的mappedHandler.getHadnler就是通过这个请求获取处理器。
* 这个处理器相当于一个执行链，将要执行的所有拦截器和处理器串在一起
* 一次请求串一次，也就是对应一个处理器对象。

2.**获取处理器适配器对象**：

HandlerAdapter ha=getHandlerAdapter(mappedHandler.getHandler())

* 这里面的mappedHandler.getHandler是获取处理器适配器对象

**执行该请求对应的所有拦截器中的preHandle方法**：

if(!mappedHandler.applyPreHandle(processedRequest,response)){return};

**调用映射的处理器**：处理结束后返回逻辑视图名称，

mv=ha.handle(processedRequest,response,mappedHandler.getHandler());

**执行该请求的所有拦截器中的postHandle方法**：

mappedHandler.applyPostHandle(processdRequest,response,mv);

3.**处理试图的代码**：处理分发结果，响应到浏览器用于渲染页面

processDispatchResult(processedRequest,reponse,mappedHandler,mv,hdisptchException);

4.**渲染页面**：render(mv，request,response);这个是上面的方法中的一行代码，实现它处理视图的功能，是正真整合了转换，响应，渲染的方法

* **逻辑视图转换为物理视图**：这个方法也是上面的render中的方法view=resolveViewName(viewName,mv.getModelInternal(),locale,request).
* **调用视图对象的渲染方法**：
  view.render(mv.getModelInternal(),request,response)
* **上面的View接口**：

  View
* **上面的resolveViewName方法**：

  **第一步**：resolveViewName();这个内部又实现的是**视图解析器**，创建了一个对象ViewResolver viewResolver;

  **第二步**：通过这个视图解析器对象，解析视图返回视图对象

  View view=viewResolver.resolveViewName(viewName,locale);
* **上面的ViewResolver**：这个是一个接口，他有ThymeleafViewResolver和InternalResourceViewResolver
* f
* f

**执行拦截器的aftercompletion方法**：这个也是processDispatchResult方法中的。

mappedHandler.triggerAfterCompletion(request,response,null)

6.**视图解析器**：这个代码也是上面的的方法中的一个方法，**他是真正起作用的代码，上面都是嵌套**

这里的viewResolver是一个接口，他会自动创建一个thymeleafViewResolver

这个ViewResolver接口就是最底层的实现，实现转换，和返回

## **springmvc流程总结**

1.**第一步**：通过**处理器映射器**找到**请求路径**对应的**处理器方法**

2.****





# springmvc的web服务器

**完成了**

1.初始化Spring上下文，就是创建了所有的bean，让IOC容器把他们管理起来，

2.初始化SpringMVC相关对象，处理器映射器，处理器适配器等。


**注意**：

1.SpringMVC就是一个web项目，主要还是要用Servle t

2.只有在web.xml中配置了servlet的配置，tomcat才会认识
