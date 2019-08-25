# 1.Filter过滤器

## 1.1.引入

- Filter，过滤器，顾名思义，即是对数据等的过滤，预处理过程。


- 为什么要引入过滤器
  - 在平常访问网站的时候，有时候发一些敏感的信息，发出后显示时 就会将敏感信息用*等字符替代，这就是用过滤器对信息进行了处理。
  - 它不仅能预处 理数据，只要是发送过来的请求它都是可以预处理的，同时，它还可以对服务器返回的响应进行预处理，这样，大大减轻了服务器的压力。
- 适用场景
  - 实现URL级别的 权限访问控制、过滤敏感词汇、压缩响应信息等一些高级功能

## 1.2.原理

- 当客户端发生请求后，在HttpServletRequest 到达Servlet 之前，过滤器拦截客户的HttpServletRequest 。 
- 根据需要检查HttpServletRequest ，也可以修改HttpServletRequest 头和数据。 
- 在过滤器中调用doFilter方法，对请求放行。请求到达Servlet后，对请求进行处理并产生HttpServletResponse发送给客户端。
- 在HttpServletResponse 到达客户端之前，过滤器拦截HttpServletResponse 。 
- 根据需要检查HttpServletResponse ，可以修改HttpServletResponse 头和数据。
- 最后，HttpServletResponse到达客户端。



![](E:/wanhe/pictures/第四阶段/8.png)

## 1.3.生命周期

- Filter接口中有三个重要的方法
  - init()方法：初始化参数，在创建Filter时自动调用。当我们需要设置初始化参数的时候，可以写到该方法中。
  - doFilter()方法：拦截到要执行的请求时，doFilter就会执行。这里面写我们对请求和响应的预处理。
  - destroy()方法：在销毁Filter时自动调用。
- Filter的生命周期
  -  Filter的创建和销毁由web服务器控制。
  -  服务器启动的时候，web服务器创建Filter的实例对象，并调用其init()方法，完成对象的初始化功能。filter对象只会创建一次，init()方法也只会执行一次。
  -  拦截到请求时，执行doFilter方法。可以执行多次。
  -  服务器关闭时，web服务器销毁Filter的实例对象。

## 1.4.编写一个过滤器

创建一个类实现Filter接口

```java
public class FilterDemo1 implements Filter {

  @Override
  public void destroy() {
    System.out.println("我被销毁了");
  }

  @Override
  public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
    throws IOException, ServletException {

    request.setAttribute("name", "zhangsan");
    ((HttpServletResponse) response).setContentType("text/html;charset=UTF-8");
    response.getWriter().write("我是过滤器写的");
    chain.doFilter(request,response);


  }

  @Override
  public void init(FilterConfig filterConfig) throws ServletException {
    System.out.println("初始化");

  }
}
```

在web.xml中配置过滤器

```xml
<filter>
  <filter-name>filterDemo1</filter-name>
  <filter-class>net.wanho.filter.FilterDemo1</filter-class>
</filter>
<filter-mapping>
  <filter-name>filterDemo1</filter-name>
  <url-pattern>/*</url-pattern>
  <!-- /*是对所有的文件进行拦截 -->
</filter-mapping>
```

编写一个Servlet进行测试

```java
@WebServlet("/ServletDemo3")
public class ServletDemo3 extends HttpServlet {

  private static final long serialVersionUID = 1L;

  protected void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
    String name = (String) request.getAttribute("name");
    response.getWriter().write("我是服务器写的");
    System.out.println(name);

  }

  protected void doPost(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
    doGet(request, response);
  }
}
```

## 1.4.1.记录某个服务被每个ip分别访问多少次

```java
@WebFilter(filterName = "CountFilter", urlPatterns = "/*")
public class CountFilter implements Filter {

  private FilterConfig fConfig;

  public void destroy() {
    // TODO Auto-generated method stub
  }

  public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
    throws IOException, ServletException {
    String ip = request.getRemoteAddr();
    System.out.println(ip);
    ServletContext context = fConfig.getServletContext();
    Map<String, Integer> coutMap = (Map<String, Integer>) context.getAttribute("coutMap");
    Integer count = coutMap.get(ip);
    if (count == null) {

      count = 1;

    } else {

      count++;
    }

    coutMap.put(ip, count);
    context.setAttribute("coutMap", coutMap);
    System.out.println("已被ip"+ip+"访问"+count+"次");
    chain.doFilter(request, response);
  }

  /*
	 * 创建map<stirng,count>
	 */
  public void init(FilterConfig fConfig) throws ServletException {
    Map<String, Integer> coutMap = new HashMap<String, Integer>();
    ServletContext context = fConfig.getServletContext();
    context.setAttribute("coutMap", coutMap);
    this.fConfig = fConfig;

  }

}
```

已被ip0:0:0:0:0:0:0:1访问1次

0:0:0:0:0:0:0:1是ipv6的地址，也代表本机

## 1.5.FilterConfig对象

用 户在配置filter时，可以使用\<init-param>为filter配置一些初始化参数，当web容器实例化Filter对象，调用其 init方法时，会把封装了filter初始化参数的filterConfig对象传递进来。因此开发人员在编写filter时，通过 filterConfig对象的方法，就可获得：

- String getFilterName()：得到filter的名称。
- String getInitParameter(String name)： 返回在部署描述中指定名称的初始化参数的值。如果不存在返回null.
- Enumeration getInitParameterNames()：返回过滤器的所有初始化参数的名字的枚举集合。
- public ServletContext getServletContext()：返回Servlet上下文对象的引用。

```java
public class FilterDemo2 implements Filter {

  @Override
  public void destroy() {
    System.out.println("我被销毁了");
  }

  @Override
  public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
    throws IOException, ServletException {

    chain.doFilter(request, response);
  }

  @Override
  public void init(FilterConfig filterConfig) throws ServletException {
    System.out.println("初始化");
    // 获取过滤器名称
    System.out.println(filterConfig.getFilterName());
    // 获取初始化参数
    String encoding = filterConfig.getInitParameter("encoding");
    System.out.println(encoding);
    // 获取所有的参数名集合
    Enumeration<String> initParameterNames = filterConfig.getInitParameterNames();
    while (initParameterNames.hasMoreElements()) {
      String name = (String) initParameterNames.nextElement();
      String value = filterConfig.getInitParameter(name);
      System.out.println(name + "====" + value);
    }

    // 获取上下文对象
    ServletContext servletContext = filterConfig.getServletContext();

  }
}
```

```xml
<filter>
  <filter-name>filterDemo2</filter-name>
  <filter-class>net.wanho.filter.FilterDemo2</filter-class>
  <init-param>
    <param-name>encoding</param-name>
    <param-value>UTF-8</param-value>
  </init-param>
</filter>
<filter-mapping>
  <filter-name>filterDemo2</filter-name>
  <url-pattern>/*</url-pattern>
  <!-- /*是对所有的文件进行拦截 -->
</filter-mapping>
```

## 1.6.过滤器链——FilterChain

一组过滤器对某些web资源进行拦截，那么这组过滤器就称为过滤器链。过滤器的执行顺序和\<filter-mapping>有关（谁在前先执行谁）。

![](E:/wanhe/pictures/第四阶段/7.png)

- 案例
  - 编写两个过滤器
  - 改变配置文件的顺序，访问被拦截的Servlet，观察结果

```java
public class FilterDemo2 implements Filter {

  @Override
  public void destroy() {
    System.out.println("我被销毁了");
  }

  @Override
  public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
    throws IOException, ServletException {
    System.out.println("我是filter2");
    chain.doFilter(request, response);
  }

  @Override
  public void init(FilterConfig filterConfig) throws ServletException {
    System.out.println("初始化");

  }
}
```

```java
public class FilterDemo1 implements Filter {

  @Override
  public void destroy() {
    System.out.println("我被销毁了");
  }

  @Override
  public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
    throws IOException, ServletException {

    System.out.println("我是filter1");
    chain.doFilter(request,response);


  }

  @Override
  public void init(FilterConfig filterConfig) throws ServletException {
    System.out.println("初始化");

  }
}

```

```xml
<!-- 过滤器执行的顺序和配置的顺序有关 -->
<filter>
  <filter-name>filterDemo1</filter-name>
  <filter-class>net.wanho.filter.FilterDemo1</filter-class>
</filter>
<filter-mapping>
  <filter-name>filterDemo1</filter-name>
  <url-pattern>/*</url-pattern>
  /*是对所有的文件进行拦截
</filter-mapping>

<filter>
  <filter-name>filterDemo2</filter-name>
  <filter-class>net.wanho.filter.FilterDemo2</filter-class>
  <init-param>
    <param-name>encoding</param-name>
    <param-value>UTF-8</param-value>
  </init-param>
</filter>
<filter-mapping>
  <filter-name>filterDemo2</filter-name>
  <url-pattern>/*</url-pattern>
  <!-- /*是对所有的文件进行拦截 -->
</filter-mapping>
```

## 1.7.乱码过滤

- 接收参数时需要过滤，响应时也需要过滤

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
  pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
  </head>
  <body>
    <form action="/ServletTest/ServletDemo2" method="post">
      姓名<input type="text" name="username"/>
      <input type="submit" value="提交"/>
    </form>
  </body>
</html>
```

```java
/*用来处理中文乱码问题 utf-8 作为参数配置到 web.xml
 中  
 自己来写一个  字符集过滤器
 *
 */
public class EncodingFilter implements Filter {

  private FilterConfig filterConfig;

  @Override
  public void init(FilterConfig filterConfig) throws ServletException {
    // TODO Auto-generated method stub
    this.filterConfig = filterConfig;
  }

  @Override
  public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
    throws IOException, ServletException {
    // TODO Auto-generated method stub
    String encoding = filterConfig.getInitParameter("encoding");
    request.setCharacterEncoding(encoding);
    response.setContentType("text/html;charset=" + encoding);
    chain.doFilter(request, response);
  }

  @Override
  public void destroy() {
    // TODO Auto-generated method stub

  }

}
```

## 1.8.登录过滤（免登录）

登录页面

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
  pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
  </head>
  <body>
    <form action="/day09/LoginServlet" method="post">
      账号：<input type="text" name="userName" id="userName"> 
      密码：<input type="text" name="password" id="password"> 
      <input type="checkbox" name="auto_login" value="auto_login">自动登录
      <input type="submit" value="提交">
    </form>
  </body>
</html>
```

LoginServlet做登录业务

```java
@WebServlet("/LoginServlet")
public class LoginServlet extends HttpServlet {
  private static final long serialVersionUID = 1L;

  /**
	 * @see HttpServlet#HttpServlet()
	 */
  public LoginServlet() {
    super();
    // TODO Auto-generated constructor stub
  }

  /**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse
	 *      response)
	 */
  protected void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
    String userName = request.getParameter("userName");
    String password = request.getParameter("password");
    String auto_login = request.getParameter("auto_login");

    // 验证

    if (userName != null && userName.equals("zhangsan") && password != null && password.equals("123")) {

      // 登录成功，信息放到session中
      User newUser = new User();
      newUser.setUserName(userName);
      newUser.setPassword(password);
      request.getSession().setAttribute("user", newUser);

      // 选择自动登录
      if (auto_login != null && auto_login.equals("auto_login")) {
        Cookie cookie = new Cookie("autoLogin", userName + "#" + password);
        cookie.setMaxAge(60 * 60);
        response.addCookie(cookie);
      }
      response.sendRedirect("/day09/success.jsp");

    } else {
      response.sendRedirect("/day09/lg.jsp");
    }

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

}
```

添加免登录过滤器

- MyCookieUtil从前面的工程中取

```java
@WebFilter("/lg.jsp")
public class LoginFilter implements Filter {

  /**
	 * Default constructor.
	 */
  public LoginFilter() {
    // TODO Auto-generated constructor stub
  }

  /**
	 * @see Filter#destroy()
	 */
  public void destroy() {
    // TODO Auto-generated method stub
  }

  /**
	 * @see Filter#doFilter(ServletRequest, ServletResponse, FilterChain)
	 */
  public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
    throws IOException, ServletException {
    /**
		 * 1.在过滤器中，从session中取值，如果用户信息不为空，直接跳转到成功页面
		 * 2.如果session为空，从cookie中取值，如果cookie中信息为空，跳转到登录页面，如果cookie中有值（zhangsan#
		 * 123），拿账号密码去数据库比对 3.如果比对不正确，重新登录 4.如果查询到了，在session中放一遍用户信息，放行
		 */

    HttpServletRequest req = (HttpServletRequest) request;
    HttpServletResponse resp = (HttpServletResponse) response;
    HttpSession session = req.getSession();
    User user = (User) session.getAttribute("user");

    // session中用户信息不为空，跳转到成功页面
    if (user != null) {
      resp.sendRedirect("/day09/success.jsp");
    } else {
      Cookie[] cookies = req.getCookies();

      Cookie cookie = CookieUitl.getCookieByName(cookies, "autoLogin");

      if (cookie == null) {
        // 第一次登录的情况，直接去登录
        chain.doFilter(request, response);
        return;
      } else {
        // 处理cookie中的值
        String userName = cookie.getValue().split("#")[0];
        String password = cookie.getValue().split("#")[1];
        // 去数据库比对
        // 数据正确 跳转到成功页面
        if (userName != null && userName.equals("zhangsan") && password != null && password.equals("123")) {
          User newUser = new User();
          newUser.setUserName(userName);
          newUser.setPassword(password);
          session.setAttribute("user", newUser);
          resp.sendRedirect("/day09/success.jsp");
        } else {
          chain.doFilter(request, response);
          return;
        }

      }

    }

    chain.doFilter(request, response);
  }
```

## 1.9.权限过滤

登录成功页面

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
  pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
  </head>
  <body>
    <c:if test="${ not empty user }">
      <h3>欢迎${user.userName } 角色是${user.userType}</h3>
    </c:if>

    <a href="/day11/power/admin/add.jsp">添加商品</a>
    <a href="/day11/power/user/cha.jsp">查询商品</a>
    <a href="/day11/power/admin/delete.jsp">删除商品</a>
    <a href="/day11/power/admin/update.jsp">修改</a>
    <a href="/day11/power/main.jsp">回到首页</a>
  </body>
</html>
```

```java
public class PowerFilter implements Filter {

  private static Map<String, String> map;

  /**
	 * Default constructor.
	 */
  public PowerFilter() {
    // TODO Auto-generated constructor stub
  }

  /**
	 * @see Filter#destroy()
	 */
  public void destroy() {
    // TODO Auto-generated method stub
  }

  /**
	 * @see Filter#doFilter(ServletRequest, ServletResponse, FilterChain)
	 */
  public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain)
    throws IOException, ServletException {
    // 获取登录的用户的信息
    HttpServletRequest req = (HttpServletRequest) request;
    HttpServletResponse resp = (HttpServletResponse) response;

    User user = (User) req.getSession().getAttribute("user");

    String servletPath = req.getServletPath();
    System.out.println(servletPath);
    Set<String> keySet = map.keySet();

    for (String key : keySet) {
      // 如果是以配置的url开头的需要权限验证
      if (servletPath.startsWith(key)) {
        if (user == null) {
          resp.sendRedirect("/day11/lg.jsp");
          return;
        } else {
          String userType = user.getUserType();
          if (userType == null) {
            throw new RuntimeException("用户信息有误");
          }

          // 如果拥有权限 放行
          if (userType.equals(map.get(key))) {
            chain.doFilter(request, response);
            return;
          } else {
            resp.sendRedirect("/day11/fail.jsp");
            return;
          }

        }

      }

    }
    // 如果不需要验证直接放行
    chain.doFilter(request, response);

  }

  /**
	 * @see Filter#init(FilterConfig)
	 */
  public void init(FilterConfig fConfig) throws ServletException {

    Map<String, String> map = new HashMap<>();
    Enumeration<String> initParameterNames = fConfig.getInitParameterNames();
    while (initParameterNames.hasMoreElements()) {
      String name = (String) initParameterNames.nextElement();
      map.put(name, fConfig.getInitParameter(name));
    }

    this.map = map;

  }

}

```

web.xml中配置

```xml
<filter>
  <filter-name>PowerFilter</filter-name>
  <filter-class>net.wanho.filter.PowerFilter</filter-class>
  <init-param>
    <param-name>/power/user</param-name>
    <param-value>1</param-value>
  </init-param>
  <init-param>
    <param-name>/power/admin</param-name>
    <param-value>0</param-value>
  </init-param>
</filter>
<filter-mapping>
  <filter-name>PowerFilter</filter-name>
  <url-pattern>/power/*</url-pattern>
</filter-mapping>
```

# 2.Listener 监听器

web监听器是一种Servlet中的特殊的类，它们能帮助开发者监听web中的特定事件，比如ServletContext,HttpSession,ServletRequest的创建和销毁；变量的创建、销毁和修改等。可以在某些动作前后增加处理，实现监控。

- 常见用途：
  - 通常使用Web监听器做以下的内容：
  - 统计在线人数，利用HttpSessionLisener
  - 加载初始化信息：利用ServletContextListener
  - 统计网站访问量

## 2.1.八大监听器

| Listener接口                      | Event类                       |
| ------------------------------- | ---------------------------- |
| ServletContextListener          | ServletContextEvent          |
| ServletContextAttributeListener | ServletContextAttributeEvent |
| HttpSessionListener             | HttpSessionEvent             |
| HttpSessionActivationListener   |                              |
| HttpSessionAttributeListener    | HttpSessionBindingEvent      |
| HttpSessionBindingListener      |                              |
| ServletRequestListener          | ServletRequestEvent          |
| ServletRequestAttributeListener | ServletRequestAttributeEvent |

## 2.2.监听器的三大作用域

- 三大作用域
  - Session
  - request
  - ServletContext 

- 8种监听器可以分为三类
  - 监听 Session、request、context 的创建于销毁
    - 分别为 HttpSessionListener、ServletContextListener、ServletRequestListener。

  - 监听对象属性变化
    - HttpSessionAttributeListener、ServletContextAttributeListener、ServletRequestAttributeListener

  - 监听Session 内的对象，分别为HttpSessionBindingListener 和 HttpSessionActivationListener。与上面六类不同，这两类 Listener 监听的是Session 内的对象，而非 Session 本身，不需要在 web.xml中配置。

    - HttpSessionBindingListener

      - 监听session内的对象的绑定和解绑

      - 实体类实现HttpSessionBindingListener

        ```java
        public class User implements HttpSessionBindingListener{

          private Integer id;
          private String  name;

          public User() {
            super();
            // TODO Auto-generated constructor stub
          }
          public User(Integer id, String name) {
            super();
            this.id = id;
            this.name = name;
          }
          public Integer getId() {
            return id;
          }
          public void setId(Integer id) {
            this.id = id;
          }
          public String getName() {
            return name;
          }
          public void setName(String name) {
            this.name = name;
          }
          @Override
          public void valueBound(HttpSessionBindingEvent arg0) {
            System.out.println("我被session绑定了");

          }
          @Override
          public void valueUnbound(HttpSessionBindingEvent arg0) {
            System.out.println("我被session移除了");
          }

        }
        ```

        ```
        session.setAttribute("user", new User(1,"zhangsan")); 触发valueBound
        session.removeAttribute("user");  触发valueUnbound
        ```

    - HttpSessionActivationListener（了解 不举例）

      - 实现实体类的序列化（活化钝化）
        - 钝化 数据存到硬盘中
          - 活化 数据硬盘读到内存中	

## 2.3.案例

ServletContextListener

```java
public class MyServletContextListener  implements ServletContextListener{

  @Override
  public void contextInitialized(ServletContextEvent sce) {
    /*System.out.println("context被创建了");
		ServletContext c =sce.getServletContext();
		c.setAttribute("progect", "/servlet10");*/
    ServletContext c =sce.getServletContext();
    c.setAttribute("count", 0);
  }

  @Override
  public void contextDestroyed(ServletContextEvent sce) {
    // TODO Auto-generated method stub
    System.out.println("context被销毁了");
  }

}
```

web.xml中配置

```xml
<listener>
  <listener-class>net.wanho.listener.MySessionListener</listener-class>
</listener>
```

ServletRequestListener

```java
public class MyServletRequestListener  implements ServletRequestListener{

  @Override
  public void requestDestroyed(ServletRequestEvent sre) {
    System.out.println("request被销毁");

  }

  @Override
  public void requestInitialized(ServletRequestEvent sre) {

    System.out.println("request被创建");
  }
}
```

MySessionAttributeListener

```java
public class MySessionListener implements  HttpSessionAttributeListener{
  @Override
  public void attributeAdded(HttpSessionBindingEvent se) {
    System.out.println("session中域存入了属性值");

  }

  @Override
  public void attributeRemoved(HttpSessionBindingEvent se) {
    System.out.println("session中域移除了属性值");

  }

  @Override
  public void attributeReplaced(HttpSessionBindingEvent se) {
    System.out.println("session中域替换了属性值");

  }
}



@WebServlet("/countServlet")
public class ServletDemo4 extends HttpServlet {

  private static final long serialVersionUID = 1L;

  protected void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {

    request.getSession().setAttribute("name", "张三");
    request.getSession().setAttribute("name", "李四");
    request.getSession().removeAttribute("name");
  }

  protected void doPost(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
    doGet(request, response);
  }

}

```

监控在线人数

```java
public class MySessionListener implements HttpSessionListener {

	@Override
	public void sessionCreated(HttpSessionEvent se) {
		System.out.println("session被创建");
		HttpSession ses= se.getSession();
		ServletContext c = ses.getServletContext();
		int count = (int) c.getAttribute("count");
		count++;
		c.setAttribute("count", count);
	}

	@Override
	public void sessionDestroyed(HttpSessionEvent se) {
		System.out.println("session被销毁");
		HttpSession ses= se.getSession();
		ServletContext c = ses.getServletContext();
		int count = (int) c.getAttribute("count");
		count--;
		c.setAttribute("count", count);
	}

}

```

# 3.文件的上传和下载

## 3.1.添加jar包

commons-io-1.4.jar
commons-fileupload-1.2.1.jar

## 3.2.文件的上传

### 3.2.1.文件上传的原理

![](E:/wanhe/pictures/第四阶段/9.png)

### 3.2.2.代码

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
  pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
  </head>
  <body>
<!-- 不对字符编码，在使用包含文件上传控件的表单时，必须使用该值  enctype="multipart/form-data"
	上传大量数据的时候用post get只能上传少量数据	-->			
    <form action="/ServletTest/UploadServlet" method="post"  enctype="multipart/form-data">

      文件描述 <input  type="text" name="filedesc"/><br/>
      文件上传 <input  type="file" name="myfile"/><br/>
      <input type ="submit" value="上传"/>
    </form>
  </body>
</html>
```

UploadServlet

```java
@WebServlet("/UploadServlet")
public class UploadServlet extends HttpServlet {
  private static final long serialVersionUID = 1L;

  /**
	 * @see HttpServlet#HttpServlet()
	 */
  public UploadServlet() {
    super();
    // TODO Auto-generated constructor stub
  }

  /**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse
	 *      response)
	 */
  protected void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
    // 创建磁盘文件工厂类 文件上传第一步
    DiskFileItemFactory factory = new DiskFileItemFactory();

    // 创建文件上传的核心对象
    ServletFileUpload upload = new ServletFileUpload(factory);

    // 设置上传文件的名称的编码
    upload.setHeaderEncoding("utf-8");

    // 提取文件
    try {
      // 解析请求的内容 提取文件数据
      List<FileItem> list = upload.parseRequest(request);
      for (FileItem f : list) {
        // 判断该表单项是否是普通类型
        if (f.isFormField()) {
          System.out.println(f.getString("utf-8"));
        } else {
          // 文件类型
          String fileName = f.getName();

          // 保证文件的名字不重复
          fileName = UUID.randomUUID().toString() + "_" + fileName;

          // 获取输入流
          InputStream in = new BufferedInputStream(f.getInputStream());

          // 指定文件上传的路径（保证文件路径不重复）
          String realPath = getServletContext().getRealPath("/upload");
          String path = UploadUtil.getPath(fileName);
          File file = new File(realPath + path);

          // 获取文件上传之后的路径
          String canonicalPath = file.getCanonicalPath();
          System.out.println(canonicalPath);

          file.mkdirs();

          // 输出流
          OutputStream os=new BufferedOutputStream(new FileOutputStream(realPath+path+"/"+fileName));

          int len=0;
          byte[] b=new byte[1024];
          while((len=in.read(b))!=-1){
            os.write(b, 0, len);

          }
          os.flush();
          os.close();
          in.close();

        }

      }

    } catch (FileUploadException e) {
      // TODO Auto-generated catch block
      e.printStackTrace();
    }

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

}
```

```java
public class UploadUtil {
  public static String getPath(String filename){
    int code =filename.hashCode();
    int dir1 = code& 0xf;
    int dir2 = (code >>> 4)&0xf;
    return "/"+dir1+"/"+dir2;

  }
}
```

## 3.3.文件的下载

### 3.3.1.文件下载的原理

- response.setHeader("Content-Type","文件格式所对应的内容类型")
  - 具体要根据国际标准的MIME属性来制定,很多种格式的文件类型在MIME都会有对应,如果直接通过URL来指定具体资源文件,则Apache服务器会根据服务器上的资源文件类型生成相应的HTTP相应消息的content-type类型,但是如果不是直接通过URL指定资源文件,而是指向一个Servlet,则在Servlet内部就需要通过代码显式来指定响应消息中的content-type类型,否则不同种类的浏览器会有不同的动作,也很有可能使浏览器崩溃。
- response.setHeader("Content-Disposition","attachment;filename=" + 文件名称)
  -  指定文件保存的默认命名,上例指定为utils.jar,是通过"content-disposition"属性指定的,如果不指定则浏览器会默认指定为当前Servlet的URL名称,例如CodeServlet.do,也就是说扩展名变成了.do而不是.jar.
- 获取文件，并读取文件
- 以字节流的方式返回页面

### 3.3.2.代码

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
  pageEncoding="UTF-8"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
  </head>
  <body>

    <a href="/ServletTest/DownLoad?filename=nazha.jpg"> 下载nazha.jpg</a>

  </body>
</html>
```

DownLoad

```java
@WebServlet("/DownloadServlet")
public class DownloadServlet extends HttpServlet {
  private static final long serialVersionUID = 1L;

  /**
	 * @see HttpServlet#HttpServlet()
	 */
  public DownloadServlet() {
    super();
    // TODO Auto-generated constructor stub
  }

  /**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse
	 *      response)
	 */
  protected void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {

    // 获取要下载的文件名称
    String fileName = request.getParameter("fileName");

    // 设置下载文件的位置
    String realPath = getServletContext().getRealPath("download");
    InputStream in = new FileInputStream(realPath + "/" + fileName);

    // 获取文件的类型
    // 可以通过文件名自动获取文件类型
    String type = getServletContext().getMimeType(fileName);

    // 设置文件类型
    response.setContentType(type);

    // 告诉浏览器以附件的形式打开文件
    response.setHeader("Content-Disposition", "attachment;filename=" + fileName);

    // 获取响应字节输出流
    OutputStream os = response.getOutputStream();
    int len = 0;
    byte[] b = new byte[1024];
    while ((len = in.read(b)) != -1) {
      os.write(b, 0, len);

    }
    os.flush();
    os.close();
    in.close();

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

}

```

