# 1.el表达式

## 1.1.简介

EL表达式：expression language 表达式语言
作用 ：简化jsp中java代码开发。
它不是一种开发语言，是jsp中获取数据的一种规范

## 1.2.el表达式使用以及取值原理

- EL表达式只能获取存在4个作用域中的数据
- 键值对
  - ${u} 原理： pageContext.findAttribute("u");
- 取对象
  - ${u.name} == u.getName()方法
  - 点（.）运算符相当于调了getter方法，点后页面跟的是属性名。
- EL获取对于null这样的数据，在页面中表现为空字符串
- []运算符：点能做的，它也能做; 它能做的，点不一定能做

```jsp
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
  </head>
  <body>

    <h3>el表达式</h3>

    <h3><%=request.getAttribute("date")%></h3>
    <h3>${date}</h3>
    <!-- EL获取对于null这样的数据，在页面中表现为空字符串  -->
    <h3>a${data}</h3>

    <!--取对象

- ${u.name} == u.getName()方法
- 点（.）运算符相当于调了getter方法，点后页面跟的是属性名。
-->
    <h1>${user.parent.id}</h1>
    <h1>${user["name"]}</h1>
    <h1>${user["parent"].name}</h1>
    <h1>${user["parent"]["name"]}</h1>

    <!-- []运算符：点能做的，它也能做; 它能做的，点不一定能做 
		arr 和 list下标从0开始	-->
    <h3>${list[1]}</h3>
    <h3>${arr[0]}</h3>
    <h3>${map["a"]}==${map.a}</h3>  <!-- 此处的a不代表属性，代表map中的键 -->
  </body>
</html>
```

创建user对象

```java
public class User {
  private String username;
  private int id;
  private User parent;


  public User getParent() {
    return parent;
  }
  public void setParent(User parent) {
    this.parent = parent;
  }
  public String getUsername() {
    return username;
  }
  public void setUsername(String username) {
    this.username = username;
  }
  public int getId() {
    return id;
  }
  public void setId(int id) {
    this.id = id;
  }
  public User(String username, int id) {
    super();
    this.username = username;
    this.id = id;
  }
  public User() {
    super();
    // TODO Auto-generated constructor stub
  }


}
```

测试Servlet

```java
@WebServlet("/el")
public class el extends HttpServlet {

  private static final long serialVersionUID = 1L;

  protected void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {

    // 键值对
    request.setAttribute("date", new Date());
    // 对象取值
    User user=new User();
    user.setId(1);
    user.setName("lisi");
    user.setParent(new User(2,"wangwu"));

    request.setAttribute("user",user );

    //测试[]符￥号
    ArrayList<String> list = new ArrayList<>();
    list.add("aaaaaa");
    list.add("bbbbbb");
    list.add("cccccc");
    request.setAttribute("list", list);

    HashMap<String, String> hashMap = new HashMap<>();
    hashMap.put("a", "aaaaaaa");
    hashMap.put("b", "bbbbbbb");
    hashMap.put("c", "ccccccc");
    request.setAttribute("map", hashMap);

    String[] arrs=new String[]{"aaaa","bbb","cccc"};

    request.setAttribute("arr", arrs);

    request.getRequestDispatcher("/el/el1.jsp").forward(request, response);
  }

  protected void doPost(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
    doGet(request, response);
  }

}
```

### 1.2.1.取值顺序演示

pageContext-->request-->session-->application

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
    session.setAttribute("name", "session");
    request.setAttribute("name", "request");
    pageContext.setAttribute("name", "page");
    application.setAttribute("name", "application");
    %>


    <h1>${pageScope.name}</h1>
    <h1>${requestScope.name}</h1>
    <h1>${sessionScope.name}</h1>
    <h1>${applicationScope.name}</h1>
    <h1>${pageContext.request.contextPath}</h1>
```

## 1.3.EL的11大隐含对象（会默写）

- 重点
  -   pageContext     pageScope   requestScope  sessionScope  applicationScope  
  -   ${pageContext.request.contextPath}取项目上下文

| EL隐式对象引用名称       | 类型                              | JSP内置对象名称   | 说明                       |
| ---------------- | ------------------------------- | ----------- | ------------------------ |
| pageContext      | javax.servlet.jsp.PageContext   | pageContext | 一样的                      |
| pageScope        | java.util.Map\<String,Object>   | 没有对应的       | pageContext范围中存放的数据,页面范围 |
| requestScope     | java.util.Map\<String,Object>   | 没有对应的       | 请求范围数据                   |
| sessionScope     | java.util.Map\<String,Object>   | 没有对应的       | 会话范围数据                   |
| applicationScope | java.util.Map\<String,Object>   | 没有对应的       | 应用范围数据                   |
| param            | java.util.Map\<String,String>   | 没有对应的       | 一个请求参数                   |
| paramValues      | java.util.Map\<String,String[]> | 没有对应的       | 重名请求参数                   |
| header           | java.util.Map\<String,String>   | 没有对应的       | 一个请求消息头                  |
| headerValues     | java.util.Map\<String,String[]> | 没有对应的       | 重名请求消息头                  |
| initParam        | java.util.Map\<String,String>   | 没有对应的       | web.xml中全局参数             |
| cookie           | java.util.Map\<String,Cookie>   | 没有对应的       | key:cookie对象的name值       |

## 1.5.EL逻辑运算

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
    request.setAttribute("n1", 10);
    request.setAttribute("n2", 20);
    request.setAttribute("n3", 30);
    request.setAttribute("n4", 40);
    %>



    ${n1+n2} <br>

    ${n1 eq n2}
    ${n1 gt n2 }
    ${n1 lt n2 }


    ${ n1 eq n2  and  n1 gt n2 }
    ${ n1 eq n2  or  n1 lt n2 }

  </body>
</html>
```

- empty
  - 判断null，空字符串和没有元素的集合(即使集合对象本身不为null)都返回true

```jsp
<%@page import="net.wanho.pojo.User"%>
<%@page import="java.util.ArrayList"%>
<%@page import="java.util.List"%>
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

    String str1=null;
    request.setAttribute("str1", str1);


    String str2="";
    request.setAttribute("str2", str2);

    String str3="abc";
    request.setAttribute("str3", str3);

    List list1=new ArrayList();
    request.setAttribute("list1", list1);


    List list2=new ArrayList();
    list2.add("ssss");
    request.setAttribute("list2", list2);

    User user=null;
    request.setAttribute("user", user);
    %>

    ${empty str1} <br>
    ${empty str2} <br>
    ${empty str3} <br>
    ${empty list1} <br>
    ${empty list2} <br>
    ${empty user} <br>
  </body>
</html>
```

# 2.jstl

## 2.1.简介

- JSTL（JavaServerPages Standard Tag Library）JSP标准标签库


- 作用
  - 使用JSTL实现JSP页面中逻辑处理。如判断、循环等。

## 2.2.使用

1.添加依赖的jar包

​	jstl.jar

​	standard.jar

2.在JSP页面添加taglib指令

​	<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>

3.使用JSTL标签

## 2.3.jstl的核心标签

### 2.3.1.通用标签

- \<c:set>   设置变量
- \<c:out>  输出数据
- \<c:remove>   移除数据

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
  pageEncoding="UTF-8"%>

<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
  </head>
  <body>

    <!-- pageContext.setAttribute("userName","zhangsan")  -->
    <c:set var="userName" value="zhangsan" scope="page"></c:set>

    <c:remove var="userName" scope="page" />

    <c:out value="${userName}"></c:out>
  </body>
</html>
```

### 2.3.2.条件标签

- \<c: if>   

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
  pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
  </head>
  <body>
    <c:set   var="num" value="10" scope="page"></c:set>

    <c:if  test="${num eq 10 }" var="i" scope="page">
      31231
    </c:if>
   		判断的结果 ${i } 

  </body>
</html>
```

- \<c: choose>   

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
  pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
  </head>
  <body>
    <c:set var="num" value="10" scope="page"></c:set>
    <c:choose>
      <c:when test="${num gt 10 }">
        num >10
      </c:when>
      <c:when test="${num lt 10 }">
        。。。
      </c:when>
      <c:otherwise>
        qita
      </c:otherwise>
    </c:choose>
  </body>
</html>
```

### 2.3.3.循环标签

- \<c: foreach> 
  - var  声明变量
  - begin  初始化
  - end  结束条件
  - step  步长

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
  pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<%@page import="java.util.*"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
  </head>
  <body>
    <%
    List<String> list = new ArrayList<String>();
    list.add("房哥");
    list.add("震哥");
    list.add("张默");

    Map<Long, String> map = new HashMap<Long, String>();
    map.put(1L, "gtx1070");
    map.put(2L, "gtx1080");
    map.put(3L, "gtx1080ti");
    pageContext.setAttribute("map", map);
    pageContext.setAttribute("list", list);
    %>
    <c:forEach var="str" items="${list }">
      ${ str}
    </c:forEach>

    <c:forEach var="entry" items="${map }">
      ${entry.key }---	${entry.value }

    </c:forEach>

    <c:forEach var="i" begin="1" end="10" step="1">
      ${i }

    </c:forEach>

    <!-- 	从1到10的和

变脸10到100 没到第三个数 显示红色 -->

    <c:set var="sum" value="0" scope="page"></c:set>

    <c:forEach var="i" begin="1" end="10" step="1">
      <c:set var="sum" value="${sum + i }" scope="page"></c:set>
    </c:forEach>
    ${sum }

    <c:forEach var="i" begin="10" end="100" step="1">
      <%-- 	<c:choose>

				<c:when test="${i%3 eq 0 }">

					<span style="color:red">${i }</span>
				</c:when>
				<c:otherwise>
				${i }
      </c:otherwise>


			</c:choose> --%>


      <%-- <c:if test="${empty user}"></c:if> --%>
      <c:if test="${i%3 eq 0 }">
        <span style="color: red">${i }</span>

      </c:if>

      <c:if test="${i%3 != 0 }">
        ${i }

      </c:if>

    </c:forEach>
  </body>
</html>
```

### 2.3.4.其他标签

- \<c: catch>  
  - \<c:catch>标签允许在jsp也面中捕获异常。它包含一个var属性，是一个描述异常的变量。

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
  pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
  </head>
  <body>
    <c:catch var="e">
      <%
      int a = 10 / 0;
      %>

    </c:catch>

    ${e.message }


  </body>
</html>
```

- \<c:import>
  - 检索一个绝对或相对 URL，然后将其内容暴露给页面
  - \<c:import>标签提供了所有\<jsp:include>行为标签所具有的功能，同时也允许包含绝对URL。

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
  pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
  </head>
  <body>
    12312
    <c:import url="/jstl/sc.jsp" context="/ServletTest" var="i">

    </c:import>
    ${i } <!-- 用于存储所引入的文本变量  -->

  </body>
</html>
```

- \<c:forTokens>
  - 可以根据某个分隔符指定字符串

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
  pageEncoding="UTF-8"%>

<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
  </head>
  <body>
    <!-- items  字符串
delims 分隔符 	  -->
    <c:forTokens var="i" items="aa,bb,cc" delims=",">
      ${i }
    </c:forTokens>
  </body>
</html>
```

- \<c:redirect>
  - 该标签用来实现请求的重定向。同时可以配合使用\<c:param>标签在url中加入指定的参数。

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
  pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>

<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
  </head>
  <body>
    <c:redirect url="/jstl/sc.jsp"  context="/servlet07">
      <c:param name="username" value="meimei"></c:param>
    </c:redirect>
  </body>
</html>
```

## 2.4.jstl函数标签库

| **fn:contains(string, substring)**       |     如果参数string中包含参数substring，返回true      |
| :--------------------------------------- | :--------------------------------------: |
| fn:containsIgnoreCase(string, substring) |  如果参数string中包含参数substring（忽略大小写），返回true  |
| fn:endsWith(string, suffix)              |      如果参数 string 以参数suffix结尾，返回tru       |
| fn:indexOf(string, substring)            |     返回参数substring在参数string中第一次出现的位置      |
| fn:join(array, separator)                | 将一个给定的数组array用给定的间隔符separator串在一起，组成一个新的字符串并返回。 |
| fn:length(item)                          | 返回参数item中包含元素的数量。参数Item类型是数组、collection或者String。如果是String类型,返回值是String中的字符数。 |
| fn:replace(string, before, after)        | 返回一个String对象。用参数after字符串替换参数string中所有出现参数before字符串的地方，并返回替换后的结果 |
| fn:split(string, separator)              | 返回一个数组，以参数separator 为分割符分割参数string，分割后的每一部分就是数组的一个元素 |
| fn:startsWith(string, prefix)            |       如果参数string以参数prefix开头，返回true       |
| fn:substring(string, begin, end)         | 返回参数string部分字符串, 从参数begin开始到参数end位置，不包括end位置的字符 |
| fn:substringAfter(string, substring)     |    返回参数substring在参数string中后面的那一部分字符串     |
| fn:substringBefore(string, substring)    |    返回参数substring在参数string中前面的那一部分字符串     |
| fn:toLowerCase(string)                   |         将参数string所有的字符变为小写，并将其返回         |
| fn:toUpperCase(string)                   |         将参数string所有的字符变为大写，并将其返回         |
| fn:trim(string)                          |          去除参数string 首尾的空格，并将其返回          |

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
  pageEncoding="UTF-8"%>

<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<%@ taglib prefix="fn" uri="http://java.sun.com/jsp/jstl/functions"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
  </head>
  <body>
    <%
    String a[] = { "aa", "bb", "cc", "dd" };
    request.setAttribute("array", a);
    request.setAttribute("store", "guomei8899");
    request.setAttribute("user", "u1,u2,u3,u4,u5");
    request.setAttribute("test", "aBcDeF   ");
    %>

    <c:out value="${fn:replace(store,'8','9')}" />
    <br>
    <c:out value="${fn:join(array,',')}" />
    <br>
    <c:out value="${fn:startsWith(store,'g')}" />
    <br>
    <c:out value="${fn:substring(store,2,5)}" />
    <br>
    <c:out value="${fn:substringAfter(store,'mei')}" />
    <br>
    <c:out value="${fn:substringBefore(store,'mei')}" />
    <br>
    <c:out value="${fn:toLowerCase(test)}" />
    <br>
    <c:out value="${fn:toUpperCase(test)}" />
    <br>
    <c:out value="${test}hoho" />
    <br>
    <c:out value="${fn:trim(test)}hoho" />
    <br>

  </body>
</html>
```

## 2.5.自定义标签

- 空标签
- 体标签
- 属性标签

空标签

```java
public class JstlDemo1 extends SimpleTagSupport{
  private PageContext pc;
  private JspFragment body;

  @Override
  public void doTag() throws JspException, IOException {
    pc.getOut().write("hello");
  }

  @Override
  public void setJspBody(JspFragment jspBody) {
    this.body=jspBody;
  }

  @Override
  public void setJspContext(JspContext pc) {
    this.pc=(PageContext) pc;
  }
}
```

体标签

```java
public class JstlDemo2 extends SimpleTagSupport{
  private PageContext pc;
  private JspFragment body;

  @Override
  public void doTag() throws JspException, IOException {
    body.invoke(pc.getOut());
  }

  @Override
  public void setJspBody(JspFragment jspBody) {
    this.body=jspBody;
  }

  @Override
  public void setJspContext(JspContext pc) {
    this.pc=(PageContext) pc;
  }



}
```

属性标签

```java
public class JstlDemo3 extends SimpleTagSupport{
  private PageContext pc;
  private JspFragment body;
  private boolean test;

  public void setTest(boolean test) {
    this.test = test;
  }

  @Override
  public void doTag() throws JspException, IOException {
    if(test){
      body.invoke(pc.getOut());

    }
  }

  @Override
  public void setJspBody(JspFragment jspBody) {
    this.body=jspBody;
  }

  @Override
  public void setJspContext(JspContext pc) {
    this.pc=(PageContext) pc;
  }
```

在WEB-INF下配置tld文件  

```xml
<?xml version="1.0" encoding="UTF-8" ?>

<taglib xmlns="http://java.sun.com/xml/ns/j2ee"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://java.sun.com/xml/ns/j2ee http://java.sun.com/xml/ns/j2ee/web-jsptaglibrary_2_0.xsd"
        version="2.0">
  <tlib-version>1.0</tlib-version>
  <short-name>myc</short-name>
  <uri>http://www.wanho.com/myc</uri>

  <tag>
    <name>print</name>
    <tag-class>net.wanho.jstl.JstlDemo1</tag-class>
    <!-- 	配置标签主体 -->
    <body-content>empty</body-content>
  </tag>


  <tag>
    <name>out</name>
    <tag-class>net.wanho.jstl.JstlDemo2</tag-class>
    <!-- 配置标签主体  
		scriptless：接受文本、EL和JSP动作。-->
    <body-content>scriptless</body-content>
  </tag>

  <tag>
    <name>if</name>
    <tag-class>net.wanho.jstl.JstlDemo3</tag-class>
    <!-- 	配置标签主体 -->
    <body-content>scriptless</body-content>
    <attribute>
      <!-- 	属性名 -->
      <name>test</name>
      <!-- 	是否是必须出现的属性 -->
      <required>true</required>
      <!-- 	是否支持el-->
      <rtexprvalue>true</rtexprvalue>
      <!-- 属性的类型 -->
      <type>boolean</type>
    </attribute>
  </tag>

</taglib>

```

jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
  pageEncoding="UTF-8"%>

<%@ taglib prefix="myc" uri="http://www.wanho.com/myc" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
    <title>Insert title here</title>
  </head>
  <body>
    <!-- 这种标签 没有标签主体 -->
    <myc:print/>

    <myc:out>
      聪聪
    </myc:out>
    <% request.setAttribute("num", 10); %>

    <myc:if test="${num eq 11 }">
      聪聪2
    </myc:if>
  </body>
</html>
```

## 2.6.自定义函数

### 2.6.1.自定义类和方法

必须是public +static

```java
public class TestFunction {

  /**
	 * 
	 * 自定义类和方法 ，方法必须是public + static 
	 * @param name
	 * @return
	 */
  public static String Hello(String name){
    return " you are a newcomer here, "+name;
  }
}
```

### 2.6.2.编写tld文件

编写自定义 tld 文件，将此自定义tld文件放在WEB-INF或者WEB-INF的任意子目录下   

```xml
<?xml version="1.0" encoding="UTF-8" ?>
 
<taglib xmlns="http://java.sun.com/xml/ns/j2ee"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://java.sun.com/xml/ns/j2ee http://java.sun.com/xml/ns/j2ee/web-jsptaglibrary_2_0.xsd"
  version="2.0">
	
	
  <description>test own defined functions library</description>
  <display-name>test  functions</display-name>
  <tlib-version>1.0</tlib-version>
  <short-name>test</short-name>
  <uri>http://net.wanho/functions</uri>  
 
	<function>
		<name>testFunction</name>
		<function-class>net.wanho.jstl.TestFunction</function-class>
		<function-signature>java.lang.String Hello(java.lang.String)</function-signature>
	</function>
 </taglib>
```

说明：

 A：标签\<description>、\<description-name>、\<tlib-version>、\<short-name>、\<uri>内容随意，注意这里设置的uri后面jsp中要引入。

B：\<function> 标签中的\<name>标签在JSP中要作为函数名调用，这里的名字可以和实际的函数名一致，也可以不一致，可认为是实际函数名的别名。

C：\<function-class>标签是 包名+类名 (自定义类)。

D：\<function-signature>是自定义函数的说明，如果是包装类型，需写完整路径；如果是基本数据类型，则不需要。

### 2.6.3.引入到jsp页面中

```jsp
<%@ taglib prefix="test" uri="http://net.wanho/functions"%>
```

### 2.6.4.测试

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>

<%@ taglib prefix="test" uri="http://net.wanho/functions"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
	<h1>测试JSTL--自定义函数库</h1>
	<span style="color: #006600;"> </span> ${test:testFunction("胡同学") }
</body>
</html>
```

# 3.jsp中的分页实现

原理

mysql中的 limit关键字

## 3.1.jsp页面

引入bootstrap的样式和js

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
  <%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
<link  rel="stylesheet" href="${pageContext.request.contextPath }/css/bootstrap.min.css"/>
<script type="text/javascript" src="${pageContext.request.contextPath }/js/jquery-3.0.0.js"></script>
<script type="text/javascript" src="${pageContext.request.contextPath }/js/bootstrap.min.js"></script>
<script type="text/javascript" src="${pageContext.request.contextPath }/js/jqPaginator.js"></script>

</head>
<body>

	<form action="/testpage/UserServlet" id="frm" method="post">
		<input name="id"  value="${id }" type="text" />
		<button>搜索</button>
	</form>
		<table>
			
			<tr>
				<th>
					id
				</th>
				<th>
					学生姓名
				</th>	
			</tr>
			
			
			
			<c:forEach var="em" items="${pageInfo.pageDatas }">
				<tr>
					<td>${em.userName }</td>
					<td>${em.pwd}</td>
				
				</tr>
			
			
			</c:forEach>
			
			
			
		</table>


	<div class="pagination-layout">
			
			<div class="pagination">
				<ul class="pagination" >
				
				</ul>
				
				
			</div>
		</div>
	
	<script type="text/javascript">
	
		window.onload=function(){
			var if_fistime=true;
			$(".pagination").jqPaginator({
				totalPages:${pageInfo.totalPages},
				visiblePages:3,
				currentPage:${pageInfo.pageNo},
				 first: '<li class="first"><a href="javascript:void(0);">第一页</a></li>',
			        prev: '<li class="prev"><a href="javascript:void(0);">上一页</a></li>',
			        next: '<li class="next"><a href="javascript:void(0);">下一页</a></li>',
			        last: '<li class="last"><a href="javascript:void(0);">最后一页</a></li>',
			        page: '<li class="page"><a href="javascript:void(0);">{{page}}</a></li>',
				
			        onPageChange:function(num){
			        	
			        	if(if_fistime){
			        		if_fistime=false;
			        	}else if(!if_fistime){
			        		changePage(num);
			        	} 	
			        }
	
			})

		}
	
		function changePage(num){
			
			window.location.href="/testpage/UserServlet?"+"&pageNum="+num;
		}
	
	</script>
</body>
</html>
```

## 3.2.封装pageBean

```java
public class PageBean<T> {
  private int pageNo ;    // 需要显示的页码
  private int totalPages ;   // 总页数
  private int pageSize ;    // 每页记录数
  private int totalRecords ; // 总记录数
  private boolean isHavePrePage ;  // 是否有上一页
  private boolean isHaveNextPage ; // 是否有下一页
  private List<T> pageDatas = new ArrayList<T>();

  public int getpageNo() {
    return pageNo;
  }

  public void setpageNo(int pageNo) {
    this.pageNo = pageNo;
  }

  public int getPageSize() {
    return pageSize;
  }

  public void setPageSize(int pageSize) {
    this.pageSize = pageSize;
  }

  public int getTotalRecords() {
    return totalRecords;
  }


  public List<T> getPageDatas() {
    return pageDatas;
  }

  public void setPageDatas(List<T> pageDatas) {
    this.pageDatas = pageDatas;
  }

  public int getTotalPages() {
    return totalPages;
  }

  public boolean getIsHavePrePage() {
    return isHavePrePage;
  }

  public boolean getIsHaveNextPage() {
    return isHaveNextPage;
  }

  public PageBean(int pageNo, int pageSize, int totalRecords) {
    super();
    this.pageNo = pageNo;
    this.pageSize = pageSize;
    if(totalRecords < 0){
      throw new RuntimeException("总记录数不能小于0!");
    }
    //设置总记录数
    this.totalRecords = totalRecords;
    //计算总页数
    this.totalPages = this.totalRecords/this.pageSize;
    if(this.totalRecords%this.pageSize!=0){
      this.totalPages++;
    }
    //计算是否有上一页
    if(this.pageNo>1){
      this.isHavePrePage = true;
    }else{
      this.isHavePrePage = false;
    }
    //计算是否有下一页
    if(this.pageNo<this.totalPages){
      this.isHaveNextPage = true;
    }else{
      this.isHaveNextPage = false;
    }
  }

  public PageBean() {
    super();
  }


}
```

## 3.3.servlet

```java
package net.wanho.controller;

import java.io.IOException;
import java.sql.Connection;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.util.ArrayList;
import java.util.List;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import net.wanho.pojo.User;
import net.wanho.util.JDBCUtil2;
import net.wanho.util.PageBean;

/**
 * Servlet implementation class UserServlet
 */
@WebServlet("/UserServlet")
public class UserServlet extends HttpServlet {
  private static final long serialVersionUID = 1L;

  /**
     * @see HttpServlet#HttpServlet()
     */
  public UserServlet() {
    super();
    // TODO Auto-generated constructor stub
  }

  /**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
	 */
  protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {

    String pageNum = request.getParameter("pageNum");

    int pageNo;
    if(pageNum==null){
      pageNo=1;
    }else{
      pageNo=Integer.parseInt(pageNum);
    }
    Integer recordCount = getRecordCount();

    String sql="select * from user limit ?,?";
    Connection connection=JDBCUtil2.getConnection();
    PreparedStatement pstmt=null;
    ResultSet rs=null;
    User user=null;
    List<User> list=new ArrayList<>();
    try {
      pstmt=connection.prepareStatement(sql);
      pstmt.setInt(1, (pageNo-1)*2);
      pstmt.setInt(2, 2);
      rs=pstmt.executeQuery();

      while(rs.next()){
        user=new User();
        user.setId(rs.getInt("id"));
        user.setUserName(rs.getString("username"));
        user.setPwd(rs.getString("pwd"));
        list.add(user);
      }

    } catch (SQLException e) {
      // TODO Auto-generated catch block
      e.printStackTrace();
    }finally {
      JDBCUtil2.closeConnection(rs, pstmt, connection);
    }

    PageBean pageInfo= new PageBean<>(pageNo, 2,  recordCount);
    pageInfo.setPageDatas(list);
    request.setAttribute("pageInfo", pageInfo);
    request.getRequestDispatcher("/show.jsp").forward(request, response);



  }

  private Integer getRecordCount() {
    String sql="select count(*) from user";
    Connection connection=JDBCUtil2.getConnection();
    PreparedStatement pstmt=null;
    ResultSet rs=null;
    Integer recordCount=null;
    try {
      pstmt=connection.prepareStatement(sql);
      rs=pstmt.executeQuery();

      while(rs.next()){
        recordCount=rs.getInt("count(*)");
      }

    } catch (SQLException e) {
      // TODO Auto-generated catch block
      e.printStackTrace();
    }finally {
      JDBCUtil2.closeConnection(rs, pstmt, connection);
    }

    return recordCount;
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





