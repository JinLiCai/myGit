# SpringMVC框架理解

JavaEE体系结构包括四层，从上到下分别是应用层、Web层、业务层、持久层。Struts和SpringMVC是Web层的框架，Spring是业务层的框架，Hibernate和MyBatis是持久层的框架。

### **为什么要使用SpringMVC？**

很多应用程序的问题在于处理业务数据的对象和显示业务数据的视图之间存在紧密耦合，通常，更新业务对象的命令都是从视图本身发起的，使视图对任何业务对象更改都有高度敏感性。而且，当多个视图依赖于同一个业务对象时是没有灵活性的。

SpringMVC是一种基于Java，实现了Web MVC设计模式，请求驱动类型的轻量级Web框架，即使用了MVC架构模式的思想，将Web层进行职责[解耦](https://www.baidu.com/s?wd=%E8%A7%A3%E8%80%A6&tn=24004469_oem_dg&rsv_dl=gh_pc_csdn)。基于请求驱动指的就是使用请求-响应模型，框架的目的就是帮助我们简化开发，SpringMVC也是要简化我们日常Web开发。

### **MVC设计模式**

MVC设计模式的任务是将包含业务数据的模块与显示模块的视图[解耦](https://www.baidu.com/s?wd=%E8%A7%A3%E8%80%A6&tn=24004469_oem_dg&rsv_dl=gh_pc_csdn)。这是怎样发生的？在模型和视图之间引入重定向层可以解决问题。此重定向层是控制器，控制器将接收请求，执行更新模型的操作，然后通知视图关于模型更改的消息。 
![img](https://i.imgur.com/XApjGKM.png)

![img](https://i.imgur.com/iEQSPKx.png)

### **SpringMVC架构**

SpringMVC是Spring的一部分，如图： 
![img](https://i.imgur.com/Qm3U8Fw.png)

**SpringMVC的核心架构：** 
![img](https://i.imgur.com/DT9IY0g.png)

**具体流程：**

（1）首先用户发送请求——>DispatcherServlet，前端控制器收到请求后自己不进行处理，而是委托给其他的解析器进行处理，作为统一访问点，进行全局的流程控制；

（2）DispatcherServlet——>HandlerMapping，映射处理器将会把请求映射为HandlerExecutionChain对象（包含一个Handler处理器（页面控制器）对象、多个HandlerInterceptor拦截器）对象；

（3）DispatcherServlet——>HandlerAdapter，处理器[适配器](https://www.baidu.com/s?wd=%E9%80%82%E9%85%8D%E5%99%A8&tn=24004469_oem_dg&rsv_dl=gh_pc_csdn)将会把处理器包装为[适配器](https://www.baidu.com/s?wd=%E9%80%82%E9%85%8D%E5%99%A8&tn=24004469_oem_dg&rsv_dl=gh_pc_csdn)，从而支持多种类型的处理器，即[适配器](https://www.baidu.com/s?wd=%E9%80%82%E9%85%8D%E5%99%A8&tn=24004469_oem_dg&rsv_dl=gh_pc_csdn)设计模式的应用，从而很容易支持很多类型的处理器；

（4）HandlerAdapter——>调用处理器相应功能处理方法，并返回一个ModelAndView对象（包含模型数据、[逻辑视图](https://www.baidu.com/s?wd=%E9%80%BB%E8%BE%91%E8%A7%86%E5%9B%BE&tn=24004469_oem_dg&rsv_dl=gh_pc_csdn)名）；

（5）ModelAndView对象（Model部分是业务对象返回的模型数据，View部分为[逻辑视图](https://www.baidu.com/s?wd=%E9%80%BB%E8%BE%91%E8%A7%86%E5%9B%BE&tn=24004469_oem_dg&rsv_dl=gh_pc_csdn)名）——> ViewResolver， 视图解析器将把[逻辑视图](https://www.baidu.com/s?wd=%E9%80%BB%E8%BE%91%E8%A7%86%E5%9B%BE&tn=24004469_oem_dg&rsv_dl=gh_pc_csdn)名解析为具体的View；

（6）View——>渲染，View会根据传进来的Model模型数据进行渲染，此处的Model实际是一个Map数据结构；

（7）返回控制权给DispatcherServlet，由DispatcherServlet返回响应给用户，到此一个流程结束。

### **SpringMVC入门程序**

（1）web.xml

```
<web-app>
  <servlet>
  <!-- 加载前端控制器 -->
  <servlet-name>springmvc</servlet-name>
  <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
  <!-- 
       加载配置文件
       默认加载规范：
       * 文件命名：servlet-name-servlet.xml====springmvc-servlet.xml
       * 路径规范：必须在WEB-INF目录下面
       修改加载路径：
   -->
   <init-param>
   <param-name>contextConfigLocation</param-name>
   <param-value>classpath:springmvc.xml</param-value>   
   </init-param>
  </servlet>

  <servlet-mapping>
  <servlet-name>springmvc</servlet-name>
  <url-pattern>*.do</url-pattern>
  </servlet-mapping>
</web-app>
1234567891011121314151617181920212223
```

（2）springmvc.xml

```
<beans>
    <!-- 配置映射处理器：根据bean(自定义Controler)的name属性的url去寻找hanler；springmvc默认的映射处理器是
    BeanNameUrlHandlerMapping
     -->
    <bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"></bean>


    <!-- 配置处理器适配器来执行Controlelr ,springmvc默认的是
    SimpleControllerHandlerAdapter
    -->
    <bean class="org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter"></bean>

    <!-- 配置自定义Controler -->
    <bean id="myController" name="/hello.do" class="org.controller.MyController"></bean>

    <!-- 配置sprigmvc视图解析器：解析逻辑试图； 
        后台返回逻辑试图：index
        视图解析器解析出真正物理视图：前缀+逻辑试图+后缀====/WEB-INF/jsps/index.jsp
    -->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/jsps/"></property>
        <property name="suffix" value=".jsp"></property>        
    </bean>
</beans>
123456789101112131415161718192021222324
```

（3）自定义Controler

```
public class MyController implements Controller{

    public ModelAndView handleRequest(HttpServletRequest arg0,
            HttpServletResponse arg1) throws Exception {
        ModelAndView mv = new ModelAndView();
        //设置页面回显数据
        mv.addObject("hello", "欢迎学习springmvc！");

        //返回物理视图
        //mv.setViewName("/WEB-INF/jsps/index.jsp");

        //返回逻辑视图
        mv.setViewName("index");
        return mv;
    }
}
12345678910111213141516
```

（4）index页面

```
<html>
<body>
<h1>${hello}</h1>
</body>
</html>
12345
```

（5）测试地址

```
http://localhost:8080/springmvc/hello.do
1
```

### **HandlerMapping**

HandlerMapping 将会把请求映射为 HandlerExecutionChain 对象（包含一个 Handler 处理器（页面控制器）对象、多个 HandlerInterceptor 拦截器）对象，通过这种策略模式，很容易添加新的映射策略。

映射处理器有三种，三种可以共存，相互不影响，分别是BeanNameUrlHandlerMapping、SimpleUrlHandlerMapping和ControllerClassNameHandlerMapping；

**BeanNameUrlHandlerMapping**

```
//默认映射器，即使不配置，默认就使用这个来映射请求。
<bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"></bean>
//映射器把请求映射到controller
<bean id="testController" name="/hello.do" class="org.controller.TestController"></bean>
1234
```

**SimpleUrlHandlerMapping**

```
<bean class="org.springframework.web.servlet.handler.SimpleUrlHandlerMapping">
    <property name="mappings">
        <props>
            <prop key="/ss.do">testController</prop>
            <prop key="/abc.do">testController</prop>
        </props>
    </property>
</bean>
//那么上面的这个映射配置：表示多个*.do文件可以访问多个Controller或者一个Controller。 
//前提是：都必须依赖自定义的控制器bean
<bean id="testController" name="/hello.do" class="org.controller.TestController"></bean>
1234567891011
```

**ControllerClassNameHandlerMapping**

```
//这个Mapping一配置：我们就可以使用Contrller的 [类名.do]来访问这个Controller.
<bean class="org.springframework.web.servlet.mvc.support.ControllerClassNameHandlerMapping"></bean>
12
```

**HandlerMapping架构图** 
![img](https://i.imgur.com/VTvZ1CR.png)

### **HandlerAdapter**

处理器适配器有两种，可以共存，分别是SimpleControllerHandlerAdapter和HttpRequestHandlerAdapter。

**SimpleControllerHandlerAdapter** 
SimpleControllerHandlerAdapter是默认的适配器，表示所有实现了org.springframework.web.servlet.mvc.Controller 接口的Bean 可以作为SpringMVC 中的处理器。

**HttpRequestHandlerAdapter** 
HTTP请求处理器适配器将http请求封装成HttpServletResquest 和HttpServletResponse对象，和servlet接口类似。

（1）配置HttpRequestHandlerAdapter适配器

```
<!-- 配置HttpRequestHandlerAdapter适配器 -->
<bean class="org.springframework.web.servlet.mvc.HttpRequestHandlerAdapter"></bean>
12
```

（2）编写Controller

```
public class HttpController implements HttpRequestHandler{

    public void handleRequest(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        //给Request设置值，在页面进行回显
        request.setAttribute("hello", "这是HttpRequestHandler！");
        //跳转页面
        request.getRequestDispatcher("/WEB-INF/jsps/index.jsp").forward(request, response);
    }
}
12345678910
```

（3）准备jsp页面

```
<html>
<body>
<h1>${hello}</h1>
</body>
</html>
12345
```

**Adapter源码分析** 
[模拟](https://www.baidu.com/s?wd=%E6%A8%A1%E6%8B%9F&tn=24004469_oem_dg&rsv_dl=gh_pc_csdn)场景：前端控制器（DispatcherServlet）接收到Handler对象后，传递给对应的处理器适配器（HandlerAdapter），处理器适配器调用相应的Handler方法。

（1）[模拟](https://www.baidu.com/s?wd=%E6%A8%A1%E6%8B%9F&tn=24004469_oem_dg&rsv_dl=gh_pc_csdn)Controller

```
//以下是Controller接口和它的是三种实现 
public interface Controller {
}

public class SimpleController implements Controller{
    public void doSimpleHandler() {
        System.out.println("Simple...");
    }
}

public class HttpController implements Controller{
    public void doHttpHandler() {
        System.out.println("Http...");
    }
}

public class AnnotationController implements Controller{
    public void doAnnotationHandler() {
        System.out.println("Annotation..");
    }
} 
123456789101112131415161718192021
```

（2）[模拟](https://www.baidu.com/s?wd=%E6%A8%A1%E6%8B%9F&tn=24004469_oem_dg&rsv_dl=gh_pc_csdn)HandlerAdapter

```
//以下是HandlerAdapter接口和它的三种实现
public interface HandlerAdapter {
    public boolean supports(Object handler);
    public void handle(Object handler);
}

public class SimpleHandlerAdapter implements HandlerAdapter{
    public boolean supports(Object handler) {
        return (handler instanceof SimpleController);
    }

    public void handle(Object handler) {
        ((SimpleController)handler).doSimpleHandler();
    }
}

public class HttpHandlerAdapter implements HandlerAdapter{
    public boolean supports(Object handler) {
        return (handler instanceof HttpController);
    }

    public void handle(Object handler) {
        ((HttpController)handler).doHttpHandler();
    }
}

public class AnnotationHandlerAdapter implements HandlerAdapter{
    public boolean supports(Object handler) {
        return (handler instanceof AnnotationController);
    }

    public void handle(Object handler) {
        ((AnnotationController)handler).doAnnotationHandler();
    }
}
1234567891011121314151617181920212223242526272829303132333435
```

（3）模拟DispatcherServlet

```
public class Dispatcher {
    public static List<HandlerAdapter> handlerAdapter = new ArrayList<HandlerAdapter>();

    public Dispatcher(){
        handlerAdapter.add(new SimpleHandlerAdapter());
        handlerAdapter.add(new HttpHandlerAdapter());
        handlerAdapter.add(new AnnotationHandlerAdapter());
    }

    //核心功能
    public void doDispatch() {
        //前端控制器（DispatcherServlet）接收到Handler对象后
        //SimpleController handler = new SimpleController();
        //HttpController handler = new HttpController();
        AnnotationController handler = new AnnotationController();

        //传递给对应的处理器适配器（HandlerAdapter）
        HandlerAdapter handlerAdapter = getHandlerAdapter(handler);

        //处理器适配器调用相应的Handler方法
        handlerAdapter.handle(handler);
    }

    //通过Handler找到对应的处理器适配器（HandlerAdapter）
    public HandlerAdapter getHandlerAdapter(Controller handler) {
        for(HandlerAdapter adapter : handlerAdapter){
            if(adapter.supports(handler)){
                return adapter;
            }
        }
        return null;
    }
}
123456789101112131415161718192021222324252627282930313233
```

（4）测试

```
public class Test {
    public static void main(String[] args) {
        Dispatcher dispather = new Dispatcher();
        dispather.doDispatch();
    }
}
123456
```

### **控制器**

**控制器架构图** 
![img](https://i.imgur.com/L0r1Tns.png)

**Controller 简介**

- 收集、验证请求参数并绑定到命令对象；
- 将命令对象交给业务对象，由业务对象处理并返回模型数据；
- 返回ModelAndView（Model部分是业务对象返回的模型数据，视图部分为逻辑视图名）。

**ServletForwardingController(转发控制器)**

将接收到的请求转发到一个命名的servlet，具体示例如下：当我们请求/forwardToServlet.do时，会被转发到名字为“forwarding”的servlet处理，该sevlet的servlet-mapping标签配置是可选的.

（1）控制器

```
public class ForwardingServlet extends HttpServlet{
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp)
            throws ServletException, IOException {
        resp.getWriter().write("Controller forward to Servlet");
    }
}
1234567
```

（2）web.xml

```
<servlet>  
<servlet-name>forwarding</servlet-name>  
<servlet-class>org.controller.ForwardingServlet</servlet-class>  
</servlet> 
1234
```

（3）spring.xml

```
<bean name="/forwardToServlet.do"   
class="org.springframework.web.servlet.mvc.ServletForwardingController">  
<property name="servletName" value="forwarding"></property>  
123
```

**AbstractCommandController(命令控制器)**

**使用post请求进行表单提交**

模拟提交用户表信息。

（1）spring.xml配置文件：

```
<beans>
    <!-- 配置映射处理器-->
    <bean class="org.springframework.web.servlet.handler.BeanNameUrlHandlerMapping"></bean>

    <!-- 配置处理器适配器-->
    <bean class="org.springframework.web.servlet.mvc.SimpleControllerHandlerAdapter"></bean>

    <!-- 配置自定义Controler -->
    <bean name="/command.do" class="org.controller.CommandController"></bean>

    <bean name="/toAdd.do" class="org.controller.ToAddController"></bean>

    <!-- 配置sprigmvc视图解析器：解析逻辑试图 -->
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/jsps/"></property>
        <property name="suffix" value=".jsp"></property>        
    </bean>
</beans>
123456789101112131415161718
```

（2）表单跳转控制器：跳转到表单页面

```
public class ToAddController implements Controller{
    public ModelAndView handleRequest(HttpServletRequest request,
            HttpServletResponse response) throws Exception {
        ModelAndView mv = new ModelAndView();
        //调转到add添加页面视图
        mv.setViewName("add");
        return mv;
    }
}
123456789
```

（3）编辑页面控制器：转发表单信息

```
public class CommandController extends AbstractCommandController{

    //指定参数绑定到哪个javaBean
    public CommandController(){
        this.setCommandClass(User.class);
    }

    @Override
    protected ModelAndView handle(HttpServletRequest request,
            HttpServletResponse response, Object command, BindException errors)
            throws Exception {
        //把命令对象强转成User对象
        User user = (User) command;
        ModelAndView mv = new ModelAndView();

        mv.addObject("user", user);
        mv.setViewName("MyJsp");

        return mv;
    }

    /*
     * 进行时间类型各种格式的覆盖
     */
    @Override
    protected void initBinder(HttpServletRequest request,
            ServletRequestDataBinder binder) throws Exception {
        String str = request.getParameter("birthday");

        if(str.contains("/")){
            binder.registerCustomEditor(Date.class, 
                    new CustomDateEditor(new SimpleDateFormat("yyyy/MM/dd"), true));
        }else{
            binder.registerCustomEditor(Date.class, 
                    new CustomDateEditor(new SimpleDateFormat("yyyy-MM-dd"), true));    
        }
    }
}
1234567891011121314151617181920212223242526272829303132333435363738
```

（4）表单页面：

```
<html>
<body>
<form action="${pageContext.request.contextPath }/command.do" method="post">
姓名：<input type="text" name="username" id="username"><p>
生日：<input type="text" name="birthday" id="birthday"><p>
性别：<input type="text" name="sex" id="sex"><p>
地址：<input type="text" name="address" id="address"><p>
<input type="submit" value="提交">
</form>
</body>
</html>
1234567891011
```

（5）表单信息呈现页面：

```
<html>
<body>
${user.username } <br>
${user.birthday } <br>
${user.sex } <br>
${user.address } <br>
</body>
</html>
12345678
```

（6）进入表单页面

```
http://localhost:8080/springmvc/toAdd.do 
1
```

**使用get请求进行表单提交**

在上面的代码基础上，直接输入地址：

```
http://localhost:8080/springmvc/command.do?username=ltx&birthday=1996/11/01&sex=男&address=广东
1
```

**ParameterizableViewController（参数控制器）**

使用参数控制器，不用自己定义Controller，可以直接使用toIndex进行访问。

```
<bean name="/toIndex.do" class="org.springframework.web.servlet.mvc.ParameterizableViewController">
<!-- 配置你所要跳转到视图的名称。跳转到index页面-->
<property name="viewName" value="index"></property>
</bean>
1234
```

### **中文乱码解决**

**Get请求乱码**

```
对于get请求中文参数出现乱码解决方法有两个：
修改tomcat配置文件添加编码与工程编码一致，如下：
<Connector URIEncoding="UTF-8" connectionTimeout="20000" port="8080" protocol="HTTP/1.1" redirectPort="8443"/>

另外一种方法对参数进行重新编码：
String userName =new
String(request.getParamter("userName").getBytes("ISO8859-1"),"UTF-8")
ISO8859-1是Tomcat默认编码，需要将Tomcat编码后的内容按UTF-8编码
12345678
```

**Post请求乱码** 
在web.xml中加入：

```
<filter>
    <filter-name>characterEncoding</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    <init-param>
        <param-name>encoding</param-name>
        <param-value>UTF-8</param-value>
    </init-param>
</filter>
<filter-mapping>
    <filter-name>characterEncoding</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```