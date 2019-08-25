# 1.JSP概述

JSP全称是Java Server Pages，它和servle技术一样，都是SUN公司定义的一种用于开发动态web资源的技术。JSP实际上就是Servlet。

jsp = html + java

html:静态内容
servlet：服务器端的小应用程序。适合编写java逻辑代码，如果编写网页内容--苦逼。
jsp:适合编写输出动态内容，但不适合编写java逻辑。

# 2.JSP原理

1. 当用户访问一个JSP页面时，会向一个Servlet容器（Tomcat等）发出请求；
2. 如果页面有所改动，则servlet容器首先要把JSP页面（假设为test.jsp）转化为Servlet代码（test.java），再将其转化为class文件（test.class文件）；这种过程(编译)会耗费时间
3. JSP容器负责调用从JSP转换来的servlet，这些servlet负责提供服务相应用户请求；如果用户有多个请求，则容器会建立多个线程处理多个请求；
4. 容器执行字节码文件，并将其结果返回到客户端；（返回的最终方式是有servlet输出html格式的文件流）

![](E:/wanhe/pictures/第四阶段/6.png)

# 3.JSP的组成元素

## 3.1.静态资源

网页的静态内容。如：html标签和文本。

## 3.2.JSP的脚本片段

- 小脚本：\<%  java代码  %>
- 表达式：<%=    %>
  - 表达式 <%= 2+3 %> 等价于out.print(2+3)
- 声明 ：<%!    %>
  - 表示在类中定义全局成员，和静态块。一般最先加载
- 案例一

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
  pageEncoding="UTF-8"%>

<%@page import="java.util.*" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
  </head>
  <body>

    <h3>编写java 代码</h3>


    <%! int a=10; %>

    <%= a %>
    <%System.out.print(a); %>

    <%= "hello" %>

    <%
    int b =100;
    if(b==100){
      System.out.print(111); 
    }else{

    }
    %>

    <% List list = new ArrayList();
    %>

    <h1 style="color:red"><%= b %></h1>
  </body>
</html>
```

- 案例二

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

    <table border="1" width="70%">
      <%  for(int i=1;i<=10;i++){
  %>


      <tr>
        <td><%=i %></td>

      </tr>


      <%}%>

    </table>
  </body>
</html>
```

## 3.3.JSP注释

JSP注释：<%-- 被注释的内容 --%> 特点：安全，省流量         页面上看不见
网页注释： \<!-- 网页注释 -->  特点：不安全，费流量              页面上可以看见

## 3.4.JSP指令

​	JSP指令（directive）是为JSP引擎而设计的，它们并不直接产生任何可见输出，而只是告诉引擎如何处理JSP页面中的其余部分。

在JSP 2.0规范中共定义了三个指令：

- page指令
- Include指令
- taglib指令

语法

```
<%@ 指令名称 属性1=“属性值1” 属性2=“属性值2”。。。%>
或者：
<%@ 指令名称 属性1=“属性值1”%>
<%@ 指令名称 属性2=“属性值2”%>

如：<%@ page language="java" import="java.util.*" pageEncoding="UTF-8"%>

<%@ page language="java" %>
<%@ page import="java.util.*" %>
```

### 3.4.1.page

用于定义JSP页面的各种属性

-  import 和java代码中的import是一样的

```
<%@ page import="java.util.Date,java.util.List"%>
或者：
<%@ page import="java.util.Date"%>
<%@ page import="java.util.List"%>

JSP会自动导入以下的包：
import java.lang.*;
import javax.servlet.*;
import javax.servlet.http.*;
import javax.servlet.jsp.*;
```

- session:是否会自动创建session对象。默认值是true
- buffer: JSP中有javax.servlet.jsp.JspWriter输出字符流。设置。输出数据的缓存大小，默认是8kb
- errorPage:如果页面中有错误，则跳转到指定的资源.。
  - errorPage="/uri" 如果写“/”则代表当前应用的目录下，绝对路径。
    如果不写“/”则代表相对路径。


- isErrorPage:是否创建throwable对象。默认是false
- context Type:等同于response.setContextType("text/html;charset=utf-8")
- page Encoding:告诉JSP引擎要翻译的文件使用的编码
- isELIgnored: 是否支持EL表达式。 默认是false

#### 3.4.1.1.异常处理案例

发生异常的页面

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8" errorPage="/innerObject/error.jsp"  %>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>

	<%  
		int i=100/0;
	%>

</body>
</html>
```

错误页面

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
  pageEncoding="UTF-8"  isErrorPage="true"  %>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
  </head>
  <body>

    <%= 
  exception.getMessage()
  %>
    </br>
  <%=exception.toString()%>

  </body>
</html>
```

### 3.4.2.include

- 静态包含：把其它资源包含到当前页面中。
  - <%@ include file="/include/header.jsp" %>
- 动态包含
  - \<jsp:include page="/include/header.jsp">\</jsp:include>
- 两者的区别：翻译的时间段不同
  - 静态包含:在翻译时就把两个文件合并
  - 动态包含:不会合并文件，当代码执行到include时，才包含另一个文件的内容

### 3.4.3.taglib

在JSP页面中导入JSTL标签库。替换jsp中的java代码片段

- <%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %> 

## 3.5.JSP的6个动作

使用标签的形式来表示一段java代码

- \<jsp:include > 动态包含
- \<jsp:forward> 请求转发
- \<jsp:param> 设置请求参数
- \<jsp:useBean> 创建一个对象
- \<jsp:setProperty> 给指定的对象属性赋值
- \<jsp:getProperty> 取出指定对象的属性值

```java
public class Student {
  private String name;
  private String password;
  public String getName() {
    return name;
  }
  public void setName(String name) {
    this.name = name;
  }
  public String getPassword() {
    return password;
  }
  public void setPassword(String password) {
    this.password = password;
  }

  public void show(String name){
    this.name = name;
  }
}
```

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
  pageEncoding="UTF-8"%>
<%@ page import="net.wanho.pojo.*"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
  </head>
  <body>
    <%
    Student stu = new Student();
    stu.setName("tom");

    out.print(stu.getName());
    //request.getRequestDispatcher("/7.jsp").forward(request, response);
    %>

    <jsp:useBean id="stu1" class="net.wanho.pojo.Student"></jsp:useBean>
    <jsp:setProperty property="name" name="stu1" value="jerry" />
    <jsp:getProperty property="name" name="stu1" />

    <!-- http://localhost:8080/day11_02_jsp2/6.jsp?name=123 -->
    <jsp:forward page="/7.jsp">
      <jsp:param value="123" name="name" />
      <jsp:param value="333" name="pwd" />
    </jsp:forward>
  </body>
</html>
```

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

    <%
      String name=request.getParameter("name");
      String pwd=request.getParameter("pwd");
      out.println(name+"==="+pwd);
    %>
  </body>
</html>
```

## 3.6.JSP的九大内置对象

- 指在JSP的<%=  %> 和<% %>中可以直接使用的对象

| 对象名         |                   类型                   |           说明           |
| ----------- | :------------------------------------: | :--------------------: |
| request     | javax.servlet.http.HttpServletRequest  |                        |
| response    | javax.servlet.http.HttpServletResponse |                        |
| session     |     javax.servlet.http.HttpSession     |   由session="true"开关    |
| application |      javax.servlet.ServletContext      |                        |
| exception   |          java.lang.Throwable           | 由isErrorPage="false"开关 |
| page        |      java.lang.Object   当前对象this       |      当前servlet实例       |
| config      |      javax.servlet.ServletConfig       |                        |
| out         |      javax.servlet.jsp.JspWriter       |     字符输出流，相当于  +对象     |
| pageContext |     javax.servlet.jsp.PageContext      |                        |

### 3.6.1.pageContext  

1.本身也是一个域对象：它可以操作其它三个域对象（request session application）的数据

- 常见方法
  - void setAttribute(String name,Object o);
  - Object getAttribute(String name);
  - void removeAttribute(String name);

- 操作其它域对象的方法
  - void setAttribute(String name,Object o，int Scope);
  - Object getAttribute(String name,int Scope);
  - void removeAttribute(String name,int Scope);
- scope的值
  - PageContext.PAGE_SCOPE 
  - PageContext.REQUEST_SCOPE 
  - PageContext.SESSION_SCOPE 
  - PageContext.APPLICATION_SCOPE
- findAttribute(String name) 方法
  - 自动从page request session application依次查找，找到了就取值，结束查找。

2.它可以创建其它的8个隐式对象

​	在普通类中可以通过PageContext获取其他JSP隐式对象。自定义标签时就使用。

3.提供了的简易方法

- pageContext.forward("2.jsp");

### 3.6.2.config

   config 对象代表当前JSP 配置信息，但JSP 页面通常无须配置，因此也就不存在配置信息。该对象在JSP 页面中非常少用，但在Servlet 则用处相对较大。因为Servlet 需要配置在web.xml 文件中，可以指定配置参数。

### 3.6.3.exception

异常对象

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
  pageEncoding="UTF-8" isErrorPage="true" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
  </head>
  <body>

    <%= exception.getMessage() %>
    <%=exception.toString() %>   
  </body>
</html>
```

```jsp

<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8" errorPage="/innerObject/error.jsp"  %>    
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>

	<%
		int i=100/0;
	%>

</body>
</html>
```

### 3.6.4.response

1.重定向页面

重定向操作支持将地址重定向到不同的主机上，这一点与转发不同。在客户机浏览器上将会得到跳转的地址，并重新发送请求链接。进行重定向后，request中的属性全部失效，并开始一个新的request对象。

```jsp
<%@ page language="java" import="java.util.*"
	contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
	<%response.sendRedirect("deal.jsp"); %>
```

2.自动刷新

```jsp
<!-- 每隔10秒自动刷新一次 -->
	<% response.setHeader("refresh", "10");%>

```

3.定时跳转到网页

```jsp
<% response.setHeader("refresh", "5;URL=deal.jsp");%>
```

## 3.7.四大域对象

- PageContext : pageConext 存放的数据在当前页面有效。开发时使用较少。
- ServletRequest: request  存放的数据在一次请求（转发）内有效。使用非常多。
- HttpSession: session 存放的数据在一次会话中有效。使用的比较多。如：存放用户的登录信息，购物车功能。
- ServletContext: application 存放的数据在整个应用范围内都有效。因为范围太大，应尽量少用。

# 4.中文乱码解决

JSP页面中文乱码问题是指用户在浏览器看到的服务器所返回的jsp页面中，中文字符不能正常显示；

- 原因：在于没有在JSP中指定 页面显示的编码


- 解决办法：向页面指定编码为utf-8，那么页面就会按照此编码来显示，于是乱码消失
  - <%@ page language="java" import="java.util.*" pageEncoding="utf-8"%>

# 5.JSP的路径问题

- 相对路径
  - 相对于此时文件的路径  
    - ../   父级目录
    - ./   当前目录
- 绝对路径
  - /    根目录（webContent）


