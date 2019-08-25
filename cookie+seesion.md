# 1.会话

​	会话：用户开一个浏览器，访问一个网站，只要不关闭该浏览器，不管该用户点击多少个超链接，访问多少资源，直到用户关闭浏览器，整个这个过程我们称为一次会话。

- 举例
  - 打开浏览器--->输入www.baidu.com（发送请求）--->搜索新闻（返回结果给浏览器）--->重复发送、返回--->直至阅读结束关闭浏览器（会话结束）
- 实际场景
  - 当你是第一次登入这个网站，网站会发出：”欢迎来到本网站”。 然而，当你第二次登入该网站，它就会发出：”欢迎再次回来”。 为什么服务器会知道我们已经登入过该页面呢？没错，就是在与服务器会话的过程中产生了一些数据，而这些数据被保存下来，服务器根据这些数据来判断你是否登陆过该页面，而输出不同欢迎标语。

下面就来学习两门会话信息管理技术

- Cookie技术: 会话数据保存在浏览器客户端。
- Session技术：会话数据保存在服务器端。

# 2.cookie

一种会话数据管理技术，该技术把会话数据保存在浏览器客户端。

## 2.1.cookie的工作原理（机制）

1）首先浏览器向服务器发出请求。

2）服务器就会根据需要生成一个Cookie对象，并且把数据保存在该对象内。

3）然后把该Cookie对象放在响应头，一并发送回浏览器。

4）浏览器接收服务器响应后，提出该Cookie保存在浏览器端。

5）当下一次浏览器再次访问那个服务器，就会把这个Cookie放在请求头内一并发给服务器。

6)  服务器从请求头提取出该Cookie，判别里面的数据，然后作出相应的动作。

## 2.2.常用方法

- 创建Cookie对象：Cookie(java.lang.String name, java.lang.String value)
- 设置Cookie对象
  - setPath(java.lang.String uri)
    - 设置cookie的有效路径，就是指定该Cookie访问哪个资源时会传过去，访问其他资源则就不会传。
  - setMaxAge(int expiry) 
    - 设置cookie的有效时长，以秒为单位
    - 正整数： 表示cookie数据保存在浏览器的缓存区中（硬盘中），以秒为单位。例如,10: cookie在10秒之后失效！
    - 负整数： 表示cookie数据保存在浏览器的内存区中。关闭浏览器cookie就会失效！
    - 零： 表示删除同名的cookie数据
  - setValue(java.lang.String newValue)
    - 设置cookie的值
  - response. addCookie(Cookie cookie)  
    - 发送cookie信息到浏览器
- 注意事项
  - cookie保存的会话数据类型必须是字符串的。浏览器一般只允许存放300个Cookie，每个站点最多存放20个Cookie，每个Cookie的大小限制为4KB。
  - cookie不适合保存敏感数据（例如密码）可见的

## 2.3.案例

```java
@WebServlet("/demo")
public class ServletDemo extends HttpServlet {

  @Override
  protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {

    //创建一个新的cookie
    Cookie cookie=new Cookie("name", "zhangsan");
    //设置最长的存活时间 可在浏览器端查看 以秒为单位
    cookie.setMaxAge(30);
    //将cookie响应到客户端
    resp.addCookie(cookie);

    //遍历所有的cookie
    Cookie[] cookies = req.getCookies();
    for(Cookie c: cookies){
      System.out.println(c.getName()+"=="+c.getValue());
    }
  }

  @Override
  protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    doGet(req, resp);
  }
}
```

- 编写工具类

```java

public class MyCookieUtil {

  public static Cookie getCookieByName(Cookie[] cookies,String cookieName){
    if(cookies==null){
      return null;
    }else{
      for(Cookie c :cookies){
        if(c.getName().equals(cookieName)){
          return c;
        }
      }
      return null;

    }

  }
}
```

- 第二次访问
  - 如果是第一次访问，先输出欢迎大爷光临
  - 如果不是第一次访问，返回上一次访问的时间

```java
@WebServlet("/CookieServletDemo3")
public class CookieServletDemo3 extends HttpServlet {
  private static final long serialVersionUID = 1L;

  /**
	 * @see HttpServlet#HttpServlet()
	 */
  public CookieServletDemo3() {
    super();
    // TODO Auto-generated constructor stub
  }

  /**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse
	 *      response)
	 */
  protected void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {

    /**
		 * 1.先判断是否是第一次访问，根据结果选择如何处理 2.如果是第一次访问，输出欢迎大爷光临，创建cookie，返回浏览器
		 * 3.如果不是第一次，从cookie中取值，把时间输出到页面上，把最新的时间保存到cookie中
		 */
    // 从cookie中取，然后判断
    Cookie[] cookies = request.getCookies();
    Cookie cookie = CookieUitl.getCookieByName(cookies, "last_time");

    // 时间转换
    SimpleDateFormat simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
    Date date = new Date();
    String dateString = simpleDateFormat.format(date);
    response.setContentType("text/html;charset=utf-8");

    if (cookie == null) {
      Cookie lastCookie = new Cookie("last_time", dateString);
      lastCookie.setMaxAge(60 * 60);
      response.addCookie(lastCookie);
      response.getWriter().write("欢迎大爷光临");
    } else {
      // 上一次访问的时间
      String lastTime = cookie.getValue();
      cookie.setValue(dateString);
      cookie.setMaxAge(60 * 60);
      response.addCookie(cookie);
      response.getWriter().write("上一次访问时间："+lastTime);
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

- 历史信息记录

product.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
  pageEncoding="UTF-8"%>

<%@ page import="net.wanho.test3.MyCookieUtil" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
  </head>
  <body>


    <!-- <img alt="" src="/servlet04/img/1.jpg"><a href="/servlet04/CartSession?id=1">手电筒</a> -->
    <img alt="" src="/ServletTest/img/2.jpg"><a href="/ServletTest/product?id=2">电话</a>
    <img alt="" src="/ServletTest/img/3.jpg"><a href="/ServletTest/product?id=3">电视</a>
    <img alt="" src="/ServletTest/img/4.jpg"><a href="/ServletTest/product?id=4">冰箱</a>
    <img alt="" src="/ServletTest/img/5.jpg"><a href="/ServletTest/product?id=5">手表</a>
    <img alt="" src="/ServletTest/img/6.jpg"><a href="/ServletTest/product?id=6">电脑</a>
    <h3>当前会话浏览记录</h3>
    <h4> 清除浏览记录</h4>

    <%
    Cookie[] cookies =request.getCookies();
    Cookie c = MyCookieUtil.getCookieByName(cookies, "product");
    if(c!=null){

      String value = c.getValue();
      String [] ids= value.split(",");


      for(String id:ids){
        %>
    <img alt="" src="/ServletTest/img/<%= id%>.jpg">
    <%	}
    }

    %>
  </body>
</html>
```

productServlet

```java
@WebServlet("/product")
public class ProductServlet extends HttpServlet {



  protected void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {


    //		获取传过来的id

    /*		判断是否是第一次访问
如果是第一次访问创建指定的cookie  把这个id 放到cookie 最后返回给浏览器

如果不是第一次  从cookie里面取 
如果cookie已经包含了这个商品 不用处理
如果不包含  product 1 produc 1,2
重定向到商品product.jsp 
在页面 遍历cookie 从cookie中取到product所对应的值 然后拼到img标签里面*/
    Cookie[] cookies = request.getCookies();
    //遍历cookies 数组判断是否存在

    Cookie c=MyCookieUtil.getCookieByName(cookies,"product");
    String id = request.getParameter("id");
    System.out.println(c==null);
    System.out.println(id);
    if(c==null){
      Cookie producCookie = new Cookie("product",id);

      producCookie.setMaxAge(60*60);
      /*	c.setPath("/servlet04");*/
      response.addCookie(producCookie);
    }else{
      /*如果cookie已经包含了这个商品 不用处理
如果不包含  product 1 produc 1,2*/
      String productCookie= c.getValue();
      System.out.println(productCookie);
      String [] ids= productCookie.split(",");
      if(!checkId(ids,id)){
        c.setValue(id+","+productCookie);
        c.setMaxAge(60*60);
        response.addCookie(c);
      }

    }

    response.sendRedirect("/ServletTest/product.jsp");
  }


  private boolean checkId(String[] ids,String id){

    for (String s:ids) {

      if(s.equals(id)){

        return true;
      }
    }



    return false;



  }
  protected void doPost(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
    doGet(request, response);
  }

}
```

# 3.session

一种会话数据管理技术，该技术把会话数据保存在服务器端。

同样都是会话数据管理技术，为什么我们要发明Session技术呢？

- cookie的局限性
  - Cookie数据类型都是String，且容量有限制的。
  - Cookie不适合保存敏感数据

Session技术可以解决这两种情况。

## 3.1.session的原理

1）浏览器发出请求到服务器。

2）服务器会根据需求生成Session对象，并且给这个Session对象一个编号，一个编号对应一个Session对象

3）服务器把需要记录的数据封装到这个Session对象里，然后把这个Session对象保存下来。

4）服务器把这个Session对象的编号放到一个Cookie里，随着响应发送给浏览器

5）浏览器接收到这个cookie就会保存下来

6）当下一次浏览器再次请求该服务器服务，就会发送该Cookie

7）服务器得到这个Cookie，取出它的内容，它的内容就是一个Session的编号！！！

8）凭借这个Session编号找到对应的Session对象，然后利用该Session对象把保存的数据取出来！

## 3.2.session的常用方法

- 创建/得到HttpSession对象
  - HttpSession request.getSession()  
  - HttpSession request.getSession(boolean create)  
- HttpSession作为域对象保存会话数据
  - void setAttribute(java.lang. String name, java.lang.Object value)  保存数据
  - java.lang.Object getAttribute(java.lang.String name)     得到数据
  - void removeAttribute(java.lang.String name)  清除数据
- session细节：
  - java.lang.String getId()  得到session对象的编号
  - void setMaxInactiveInterval(int interval)   设置session对象的有效时长
  - void invalidate()      销毁session对象

```java
@WebServlet("/SessionServletDemo1")
public class SessionServletDemo1 extends HttpServlet {
  private static final long serialVersionUID = 1L;

  /**
	 * @see HttpServlet#HttpServlet()
	 */
  public SessionServletDemo1() {
    super();
    // TODO Auto-generated constructor stub
  }

  /**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse
	 *      response)
	 */
  protected void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {

    HttpSession session = request.getSession();
    session.setAttribute("userName", "zhangsan");

    User user = new User(1, "lisi");
    session.setAttribute("user", user);
    // 单位是秒
    //		session.setMaxInactiveInterval(10);

    System.out.println(session.getId());

    //session失效
    //		session.invalidate();

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

## 3.3.session的注意事项

- 得到session编号： getId() 


- session对象生命周期：
  - session对象什么创建？ 
    - 执行request.getSession()方法时 
  - session对象什么销毁？
    - 默认情况下，session对象在30分钟之后服务器自动销毁。
    - 手动设置session有效时长
      - void setMaxInactiveInterval(int interval) -以秒为单位。
    - 配置session的有效时长（统一配置）
- 手动销毁
  - void invalidate()
- session编号的cookie过期时间：
  - 默认情况下，cookie是在浏览器关闭时失效！！！
  - 修改cookie的有效时长：
    - setMaxAge(正整数);


## 3.4.浏览器禁用cookie仍然可以使用session

	url拼接session的编号
	http://localhost:8080/day06/session.jsp;jsessionid=AE62ECBAAD2CA16DA6AEBF1D1527CD45
## 3.5.案例

session的简易购物车

```java
@WebServlet("/CartSession")
public class CartSession extends HttpServlet {

  private static final long serialVersionUID = 1L;

  protected void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {

    /*		0.Map<Strirng,Integer> cart 车 里面放的是商品名和数量
		1.接收参数  把id转成对应的商品
		String [] names= {"手电筒"，"电视机"，"冰箱"，"电话"}；
							1       2         3           4

		2.判断是否是第一次购买 （从session里面找cart 如果是null 肯定就是第一次了呗）
				如果是第一次我就创建一个购物车，把这个商品放进去数量1
				如果不是第一次
						先判断是否包含该商品 如果包含+1
						如果不包含 放入 1
		3.*/

    String id =request.getParameter("id");
    String [] names = new String []{"手电筒","电视","冰箱","洗衣机","电话","电脑"};
    int index = Integer.parseInt(id);

    String productName=names[index-1];
    //拿车之前 需要什么 需要session
    HttpSession session =request.getSession();
    Map<String,Integer> cart = (Map<String, Integer>) session.getAttribute("cart");
    if(cart==null){
      cart = new HashMap<String,Integer>();
      cart.put(productName, 1);
      session.setAttribute("cart", cart);

    }else{
      if(cart.containsKey(productName)){
        Integer count = cart.get(productName);
        count++;
        cart.put(productName, count);
        session.setAttribute("cart", cart);	
      }else{
        cart.put(productName, 1);
        session.setAttribute("cart", cart);		
      }

    }			
    response.sendRedirect("/servlet04/buy.jsp");
  }

  protected void doPost(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
    doGet(request, response);
  }

}
```

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
  pageEncoding="UTF-8"%>

<%@ page import="java.util.*"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
  </head>
  <body>
    <img alt="" src="/ServletTest/img/1.jpg">
    <a href="/ServletTest/CartSession?id=1">手电筒</a>
    <img alt="" src="/ServletTest/img/2.jpg">
    <a href="/ServletTest/CartSession?id=2">电话</a>
    <img alt="" src="/ServletTest/img/3.jpg">
    <a href="/ServletTest/CartSession?id=3">电视</a>
    <img alt="" src="/ServletTest/img/4.jpg">
    <a href="/ServletTest/CartSession?id=4">冰箱</a>
    <img alt="" src="/ServletTest/img/5.jpg">
    <a href="/ServletTest/CartSession?id=5">手表</a>
    <img alt="" src="/ServletTest/img/6.jpg">
    <a href="/ServletTest/CartSession?id=6">电脑</a>


    <%
    Map<String, Integer> cart = (Map<String, Integer>) session.getAttribute("cart");

    if (cart != null) {
      Set<String> names = cart.keySet();
      for (String name : names) {
        Integer count = cart.get(name);
        %>

    <h3>
      亲，您购买了<%=name%>,数量<%=count%></h3>

    <%
    }
    }
    %>
  </body>
</html>
```

## 3.5.Session的活化和钝化

### 3.5.1.应用场景

1.一般来说，服务器启动后，就不会再关闭了，但是如果逼不得已需要重启，而用户会话还在进行相应的操作，这时就需要使用序列化将session信息保存起来放在硬盘，服务器重启后，又重新加载。这样就保证了用户信息不会丢失，实现永久化保存
2.淘宝每年都会有定时抢购的活动，很多用户会提前登录等待，长时间不进行操作，一致保存在内存中，而到达指定时刻，几十万用户并发访问，就可能会有几十万个session，内存可能吃不消，这时就需要进行对象的活化、钝化，让其在闲置的时候离开内存，将信息保存至硬盘，等要用的时候，就重新加载进内存.

### 3.5.2.应用

活化：从硬盘上读取到内存中

纯化：从内存中写到硬盘上

# 4.Token令牌的应用

作用：避免表单的重复提交

案例

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
    <form action="${pageContext.request.contextPath}/DoFormServlet" method="post">


      <input type="hidden" name="token" value="<%=request.getSession().getAttribute("token")%>"/>

      用户名：<input type="text" name="username">
      <input type="submit" value="提交">
    </form>

  </body>
</html>
```

```java
@WebServlet("/TokenServlet")
public class TokenServlet extends HttpServlet {

  private static final long serialVersionUID = 1L;

  protected void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {

    /*token可以有多种产生的方式 标准的是BH64加密*/
    String token = UUID.randomUUID().toString();

    request.getSession().setAttribute("token", token);


    request.getRequestDispatcher("token.jsp").forward(request, response);
  }

  protected void doPost(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
    doGet(request, response);
  }

}
```

```java
@WebServlet("/DoFormServlet")
public class DoFormServlet extends HttpServlet {

  private static final long serialVersionUID = 1L;

  protected void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
    boolean b = isRepeatSubmit(request);
    if (b) {
      System.out.println("请不要重复提交");
      return;
    }
    request.getSession().removeAttribute("token");
    System.out.println("处理用户请求");
  }

  private boolean isRepeatSubmit(HttpServletRequest request) {
    String formToken = request.getParameter("token");
    if (formToken == null) {
      return true;
    }
    String sessionToken = (String) request.getSession().getAttribute("token");
    if (sessionToken == null) {
      return true;
    }

    System.out.println(formToken);
    System.out.println(sessionToken);
    if (!sessionToken.equals(formToken)) {
      return true;
    }
    return false;
  }

  protected void doPost(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
    doGet(request, response);
  }
}
```

​	