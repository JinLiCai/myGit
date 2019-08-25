# 1.什么Servlet

servlet 是运行在 Web 服务器中的小型 Java 程序（即：服务器端的小应用程序）。servlet 通常通过 HTTP（超文本传输协议）接收和响应来自Web 客户端的请求。

## 1.1. 编写一个 servlet程序

### 1.1.1.写一个java类，实现servlet接口

```java
public class ServletDemo implements Servlet{

  @Override
  public ServletConfig getServletConfig() {
    // TODO Auto-generated method stub
    return null;
  }

  @Override
  public String getServletInfo() {
    // TODO Auto-generated method stub
    return null;
  }

  @Override
  public void init(ServletConfig arg0) throws ServletException {
    // TODO Auto-generated method stub

  }

  @Override
  public void service(ServletRequest req, ServletResponse res) throws ServletException, IOException {
    res.getWriter().write("hello world");

  }

  @Override
  public void destroy() {
    // TODO Auto-generated method stub

  }
}
```

### 1.1.2.修改web.xml文件，给servlet提供一个可访问的URI地址

```xml
<!-- 创建一个servlet实例 -->
<servlet>
  <servlet-name>ServletDemo</servlet-name>
  <servlet-class>net.wanho.ServletDemo</servlet-class>
</servlet>

<!-- 给servlet提供(映射)一个可访问的URL地址 -->
<servlet-mapping>
  <servlet-name>ServletDemo</servlet-name>
  <url-pattern>/demo</url-pattern>
</servlet-mapping>
```

### 1.1.3.部署应用到tomcat服务器

### 1.1.4.测试

访问http://localhost:8080/ServletTest/demo

# 2.Servlet生命周期

实例化-->初始化-->服务-->销毁

出生：（实例化-->初始化）第一次访问Servlet就出生（默认情况下）

活着：（服务）应用活着，servlet就活着

死亡：（销毁）应用卸载了servlet就销毁。

```java
public class ServletDemo1 implements Servlet{

  //创建实例   
  public ServletDemo1() {
    super();
    System.out.println("ServletDemo1的实例被创建了");
  }

  //在servlet被服务器移除之前  调用该方法 进行销毁操作
  // 服务器关闭   销毁跟数据之间的 链接 ，向日志写遗言
  //或者实现一些关闭之前的特殊功能
  @Override
  public void destroy() {
    System.out.println("调用摧毁方法");

  }

  @Override
  public ServletConfig getServletConfig() {
    // TODO Auto-generated method stub
    return null;
  }

  @Override
  public String getServletInfo() {
    // TODO Auto-generated method stub
    return null;
  }


  //servlet实例被创建后  立即调用该方法 进行初始化
  // 第一次访问的时候，servlet 实例被服务器创建
  //init方法也只调用一次
  @Override
  public void init(ServletConfig arg0) throws ServletException {
    System.out.println("初始化");

  }

  //serlvet 是接收用户请求 做出响应
  @Override
  public void service(ServletRequest request, ServletResponse reponse) throws ServletException, IOException {
    System.out.println("响应用户请求");
  }

}
```

## 2.1.servlet在服务器启动时就创建

```xml
<servlet>
  <servlet-name>ServletDemo1</servlet-name>
  <servlet-class>net.wanho.ServletDemo1</servlet-class>
  <load-on-startup>1</load-on-startup>
</servlet>
```

当值为0或者大于0时，表示容器在应用启动时就加载这个servlet。正数的值越小，启动该servlet的优先级越高。

当是一个负数时或者没有指定时，则指示容器在该servlet被选择时才加载。

# 3.执行过程

![1](E:\wanhe\pictures\第四阶段\1.png)

# 4.Servlet的三种创建方式

## 4.1、实现javax.servlet.Servlet接口（见1.1.1）

## 4.2、继承javax.servet.GenericServlet类(适配器模式)

```java
GenericSErpublic class ServletDemo2 extends GenericServlet {

  @Override
  public void service(ServletRequest req, ServletResponse res) throws ServletException, IOException {
    res.getWriter().write("hello ServletDemo2");
  }
}
```

## 4.3、继承javax.servlet.http.HttpServlet类（模板方法设计模式）

(开发中常用方式)

```java
public class ServletDemo3 extends HttpServlet {

  @Override
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    resp.getWriter().write("hello ServletDemo3");
  }

  @Override
  protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    doGet(req, resp);
  }
}
```

## 4.4.servlet映射细节

### 4.4.1.配置多个映射路径

```xml
<servlet>
  <servlet-name>ServletDemo4</servlet-name>
  <servlet-class>net.wanho.ServletDemo4</servlet-class>
</servlet>

<!-- 给servlet提供(映射)一个可访问的URL地址 -->
<servlet-mapping>
  <servlet-name>ServletDemo4</servlet-name>
  <url-pattern>/demo4</url-pattern>
</servlet-mapping>

<servlet-mapping>
  <servlet-name>ServletDemo4</servlet-name>
  <url-pattern>/demo44</url-pattern>
</servlet-mapping>

<servlet-mapping>
  <servlet-name>ServletDemo4</servlet-name>
  <url-pattern>/abc/demo4</url-pattern>
</servlet-mapping>
```

### 4.4.2.通配符

- 通配符* 代表任意字符串
  - url-pattern: \*.do(扩展名方式)    以*.扩展名 字符串的请求都可以访问   注：不要加/
  - url-pattern: /* 任意字符串都可以访问
  - url-pattern：/action/* 以/action开头的请求都可以访问
- 匹配规则：
  - 优先级：从高到低
  - 绝对匹配--> /开头匹配--> 扩展名方式匹配
  - 如果url-pattern的值是/，表示执行默认映射。所有资源都是servlet

### 4.4.3.基于注解的映射方式

加上注解@WebServlet() 括号中写上映射路径

注：此方式在web3.0版本之后可以使用

```java
@WebServlet("/demo6")
public class ServletDemo6 extends HttpServlet {

  @Override
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    resp.getWriter().write("hello ServletDemo6");
  }

  @Override
  protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    doGet(req, resp);
  }
}
```

# 5.Servlet获取配置信息

## 5.1.ServletConfig

在web.xml中配置初始化参数

```xml
<servlet>
  <servlet-name>ServletDemo6</servlet-name>
  <servlet-class>net.wanho.ServletDemo6</servlet-class>
  <init-param>
    <param-name>userName</param-name>
    <param-value>zhangsan</param-value>
  </init-param>
  <init-param>
    <param-name>password</param-name>
    <param-value>123456</param-value>
  </init-param>
</servlet>
<!-- 给servlet提供(映射)一个可访问的URL地址 -->
<servlet-mapping>
  <servlet-name>ServletDemo6</servlet-name>
  <url-pattern>/demo6</url-pattern>
</servlet-mapping>
```

使用ServletConfig类获取配置

```java
public class ServletDemo6 extends HttpServlet {

  @Override
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

    ServletConfig config = getServletConfig();
    System.out.println(config.getServletName());
    String userName = config.getInitParameter("userName");
    String password = config.getInitParameter("password");
    System.out.println(userName+"----"+password);

    //获取所有的初始化除参数名
    Enumeration<String> initParameterNames = config.getInitParameterNames();
    //遍历取出值
    while (initParameterNames.hasMoreElements()) {
      String name = (String) initParameterNames.nextElement();
      System.out.println(name);
      String value = config.getInitParameter(name);
      System.out.println(value);
    }

  }

  @Override
  protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    doGet(req, resp);
  }
}
```

## 5.2.ServletContext

ServletContext: 代表的是整个应用。一个应用只有一个ServletContext对象。单例。

服务器开始就存在，服务器关闭才释放。用于存储全局的信息。

### 5.2.1.获取全局配置信息

修改web.xml文件

```xml
<!-- 配置当前应用的全局信息 -->
<context-param>
  <param-name>encoding</param-name>
  <param-value>UTF-8</param-value>
</context-param>
```

获取全局配置信息

```java
public class ServletDemo7 extends HttpServlet {

  @Override
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

    ServletContext servletContext = getServletContext();
    String encoding = servletContext.getInitParameter("encoding");
    System.out.println(encoding);
  }

  @Override
  protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    doGet(req, resp);
  }
}
```

### 5.2.2.在一定范围内（当前应用），使多个Servlet共享数据

- 常用方法

  - void setAttribute(String name,object value)   向ServletContext对象的map中添加数据
  - Object getAttribute(String name)    从ServletContext对象的map中取数据
  - void removeAttribute(String name)   根据name去移除数据

- 画图分析

  ![2](E:\wanhe\pictures\第四阶段\2.png)

- 写一个servlet，记录访问的次数

  ```java
  @WebServlet("/ServletContextA")
  public class ServletContextA extends HttpServlet {
    private static final long serialVersionUID = 1L;
   
    public ServletContextA() {
      super();
      // TODO Auto-generated constructor stub
    }

    protected void doGet(HttpServletRequest request, HttpServletResponse response)
      throws ServletException, IOException {

      ServletContext context = getServletContext();

      /*int i = 1;
  		// 先从ServletContext取出用户访问的次数
  		Object count = context.getAttribute("count");

  		if (null == count) {
  			// 如果不存在，设置一个新的访问次数属性
  			context.setAttribute("count", i);
  		} else {
  			// 如果存在，就把原来的次数加1
  			i = (int) context.getAttribute("count");
  			i++;
  			context.setAttribute("count", i);
  		}*/

      int count=(int)context.getAttribute("count");
      count++;
      context.setAttribute("count", count);
      System.out.println("你已经第" + count + "次访问本应用了");

    }

    /**
  	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse
  	 *      response)
  	 */
    protected void doPost(HttpServletRequest request, HttpServletResponse response)
      throws ServletException, IOException {
      // TODO Auto-generated method stub
      doGet(request, response);
    }

    @Override
    public void init() throws ServletException {
      super.init();
      getServletContext().setAttribute("count", 0);

    }
  }
  ```
  ServletContextB

  ```java
  @WebServlet("/ServletContextB")
  public class ServletContextB extends HttpServlet {
    private static final long serialVersionUID = 1L;

    /**
       * @see HttpServlet#HttpServlet()
       */
    public ServletContextB() {
      super();
      // TODO Auto-generated constructor stub
    }

    /**
  	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
  	 */
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
      ServletContext context = getServletContext();

      /*int i = 1;
  		// 先从ServletContext取出用户访问的次数
  		Object count = context.getAttribute("count");

  		if (null == count) {
  			// 如果不存在，设置一个新的访问次数属性
  			context.setAttribute("count", i);
  		} else {
  			// 如果存在，就把原来的次数加1
  			i = (int) context.getAttribute("count");
  			i++;
  			context.setAttribute("count", i);
  		}

  		context.removeAttribute("count");*/

      int count=(int)context.getAttribute("count");
      count++;
      context.setAttribute("count", count);
      System.out.println("你已经第" + count + "次访问本应用了");

    }

    /**
  	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse response)
  	 */
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
      // TODO Auto-generated method stub
      doGet(request, response);
    }

  }
  ```

### 5.2.3.获取资源路径

- String  getRealPath(String path)    根据资源名称得到资源的绝对路径 

- 可以得到当前应用任何位置的任何资源

  ```java
  @WebServlet("/demo9")
  public class ServletDemo8 extends HttpServlet {

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

      Properties properties = new Properties();
      // 加"/"相对于classes目录
      String path = "/WEB-INF/classes/net/wanho/db.properties";
      // InputStream inputStream = getServletContext().getResourceAsStream(path);
      // properties.load(inputStream);

      // 通过绝对路径获取文件配置
      String realPath = getServletContext().getRealPath(path);
      System.out.println(realPath);
      properties.load(new FileInputStream(realPath));

      String username = properties.getProperty("username");
      String password = properties.getProperty("password");
      System.out.println(username + "=======" + password);
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
      doGet(req, resp);
    }
  }
  ```

# 6.HttpServletRequest

## 6.1.请求行

Get  http://localhost:8080/day09/servlet/req1?username=zs  http/1.1

常用方法

- getMethod(); 获得请求方式
- getRequestURL();返回客户端发出请求时的完整URL。
- getRequestURI(); 返回请求行中的资源名部分。
- getContextPath(); 当前应用的虚拟目录 /day09_01_request
- getQueryString() ; 返回请求行中的参数部分。

```java
@WebServlet("/demo10")
public class ServletDemo10 extends HttpServlet {

  @Override
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    System.out.println("请求方式===" + req.getMethod());
    System.out.println("请求行中的资源===" + req.getRequestURI());
    System.out.println("请求的URL==" + req.getRequestURL());
    System.out.println("虚拟目录==" + req.getContextPath());
    System.out.println("请求行中的参数" + req.getQueryString());
  }

  @Override
  protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    doGet(req, resp);
  }

}
```

## 6.2.请求消息头

常用方法

-  String   get Header(String name)  根据头名称得到头信息值
-  Enumeration   getHeaderNames()  得到所有头信息name

```java
@WebServlet("/demo11")
public class ServletDemo11 extends HttpServlet {

  @Override
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    String agent = req.getHeader("user-agent");
    System.out.println(agent);

    Enumeration<String> headerNames = req.getHeaderNames();
    while (headerNames.hasMoreElements()) {
      String name = (String) headerNames.nextElement();
      String value = req.getHeader(name);
      System.out.println(name+"============"+value);
    }
  }

  @Override
  protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    doGet(req, resp);
  }
}
```

## 6.3.请求正文

### 6.3.1.获取表单数据相关的方法

- get Parameter(name) 根据表单中name属性的名，获取value属性的值方法 
- getParameterNames() 得到表单提交的所有name的方法 
- getParameterMap 到表单提交的所有值的方法   //做框架用，非常实用

新建注册表单

```html
<body>
	<form action="/ServletTest/demo12">
		用户名:<input type="text" id="userName" name="userName"> <br/>
		密码:<input type="text" id="password" name="password"><br/>
		<input type="submit" value="登录">
	</form>
</body>
```

方法测试

```java
@WebServlet("/demo12")
public class ServletDemo12 extends HttpServlet {

  @Override
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    String userName = req.getParameter("userName");
    String password = req.getParameter("password");
    System.out.println(userName + "===" + password);

    Enumeration<String> parameterNames = req.getParameterNames();
    while (parameterNames.hasMoreElements()) {
      String name = (String) parameterNames.nextElement();
      System.out.println(name);

    }

    Map<String, String[]> parameterMap = req.getParameterMap();
    Set<String> keySet = parameterMap.keySet();
    for (String key : keySet) {
      System.out.println(key + "===" + parameterMap.get(key)[0]);
    }

  }

  @Override
  protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    doGet(req, resp);
  }

}
```

### 6.3.2.请求转发

RequestDispatcher getRequestDispatcher(String path)

- forward(ServletRequest request, ServletResponse response) //转发的方法
  - 把请求的内容转发到另外的一个servlet   
  - 转发是在服务器端转发的，客户端是不知道的

```java
@WebServlet("/PoorServlet")
public class PoorServlet extends HttpServlet {
  private static final long serialVersionUID = 1L;

  /**
     * @see HttpServlet#HttpServlet()
     */
  public PoorServlet() {
    super();
    // TODO Auto-generated constructor stub
  }

  /**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
	 */
  protected void doGet(HttpServletRequ“”st request, HttpServletResponse response) throws ServletException, IOException {
    System.out.println("请你买东西");

    System.out.println("我没钱，你去找富人");
    
    //讲解request域的用法
    request.setAttribute("address", "南京本地人");
    request.getRequestDispatcher("/RichServlet").forward(request, response);

   // response.sendRedirect("/day03/RichServlet");



  }

  /**
	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse response)
	 */
  protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    // TODO Auto-generated method stub
    doGet(request, response);
  }

}


```

```java
@WebServlet("/RichServlet")
public class RichServlet extends HttpServlet {
  private static final long serialVersionUID = 1L;

  /**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
	 */
  protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

    System.out.println(request.getAttribute("address"));
    System.out.println("没关系，我有钱，什么都能买");
  }

  /**
	 * @see HttpServlet#doPost(HttpServletRequest request, HttpServletResponse response)
	 */
  protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    // TODO Auto-generated method stub
    doGet(request, response);
  }

}
```

### 6.3.3.request域对象的用法

- void setAttribute(String name, Object value);
- Object getAttribute(String name);
- Void removeAttribute(String name); 

例子见6.3.2

### 6.4.4.请求编码

![](E:\wanhe\pictures\第四阶段\4.png)

- 解决post方式编码
  - request.setCharacterEncoding("UTF-8")
  - 告诉服务器客户端什么编码,只能处理post请求方式
- 解决get方式编码
  - String name = new String(name.getBytes(“iso-8859-1”),”UTF-8”);

# 7.HttpServletResponse

## 7.1.响应行

- setStatus(int sc) 设置响应状态码

## 7.2.响应头

- sendRedirect(String location) 请求重定向
- setHeader(String name, String value)  设置响应头信息

例子

见6.3.2

## 7.3.响应正文

- getWriter(); 字符输出流
- setCharacterEncoding(String charset)    告知服务器使用什么编码
- setContentType(String type)   

```java
@WebServlet("/demo18")
public class ServletDemo18 extends HttpServlet {

  @Override
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

    resp.setContentType("text/html;charset=UTF-8");
    resp.getWriter().write("<h1>5秒之后 跳转页面</h1>");

    // 设置客户端头信息
    resp.setHeader("refresh", "5;url=https://www.baidu.com/");
  }

  @Override
  protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    doGet(req, resp);
  }
}
```

## 7.4.两种解决编码问题的方法分析

![3](E:\wanhe\pictures\第四阶段\3.png)



## 7.5.转发和重定向的区别

![](E:\wanhe\pictures\第四阶段\5.png)

# 8.Servlet的线程安全

　　Servlet体系结构是建立在Java多线程机制之上的，它的生命周期是由Web容器负责的。当客户端第一次请求某个Servlet时，Servlet容器将会根据web.xml配置文件实例化这个Servlet类。当有新的客户端请求该Servlet时，一般不会再实例化该Servlet类，也就是有多个线程在使用这个实例。Servlet容器会自动使用线程池等技术来支持系统的运行。

​	这样，当两个或多个线程同时访问同一个Servlet时，可能会发生多个线程同时访问同一资源的情况，数据可能会变得不一致。所以在用Servlet构建的Web应用时如果不注意线程安全的问题，会使所写的Servlet程序有难以发现的错误。

线程不安全的例子

```java
@WebServlet("/demo19")
public class ServletDemo19 extends HttpServlet {
  PrintWriter pr=null;
  @Override
  protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

    String username = request.getParameter("username");
    /*response.setContentType("text/html,charset=utf-8");*/
    pr=response.getWriter();
    try {
      Thread.sleep(5000);
      pr.write(username);
    } catch (InterruptedException e) {
      // TODO Auto-generated catch block
      e.printStackTrace();
    }
  }	

  @Override
  protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    doGet(req, resp);
  }

}
```

解决线程安全问题的最佳办法，不要写全局变量，而写局部变量。

```java
@WebServlet("/demo19")
public class ServletDemo19 extends HttpServlet {

  @Override
  protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    PrintWriter pr=null;
    String username = request.getParameter("username");
    /*response.setContentType("text/html,charset=utf-8");*/
    pr=response.getWriter();
    try {
      Thread.sleep(5000);
      pr.write(username);
    } catch (InterruptedException e) {
      // TODO Auto-generated catch block
      e.printStackTrace();
    }
  }	

  @Override
  protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    doGet(req, resp);
  }

}
```

# 
