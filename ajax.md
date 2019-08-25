# 1.ajax技术简介

AJAX = Asynchronous JavaScript and XML（异步的 JavaScript 和 XML）。

AJAX 不是新的编程语言，而是一种使用现有标准的新方法。

AJAX 最大的优点是在不重新加载整个页面的情况下，可以与服务器交换数据并更新部分网页内容。

AJAX 不需要任何浏览器插件，但需要用户允许JavaScript在浏览器上执行。

# 2.XMLHttpRequest使用

现在使用Jquery版本的ajax较多，但是原生的ajax是我们理解ajax的基础，这里我们也需要讲解一下。

使用XMLHttpRequest的步骤：

- 创建XMLHttpRequest对象
  - XMLHttpRequest 对象用于在后台与服务器交换数据
  - 优势
    - 在不重新加载页面的情况下更新网页（使用的原因）
    - 在页面已加载后从服务器请求数据
    - 在页面已加载后从服务器接收数据
    - 在后台向服务器发送数据
- 设置请求的方法及URL
  - xhr.open("GET/POST","url",true/false), true表示异步请求，false表示同步请求
- 设置状态改变时的回调函数
  - xhr.onreadystatechange=function(){}

　　　　0:未初始化
　　　　1:正在加载
　　　　2:加载完成
　　　　3:请求进行中
　　　　4:请求完成

- responseText:服务器返回的数据(文本格式)

  responseXML:服务器返回的数据（XML格式）


- 发送请求
  - xhr.send(data),如果为post提交，则data为提交的数据，如果为get提交，则参数为null即可。

## 2.1.不传参数

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
    <button onclick="run()">an</button>
    <h3 id="a1"></h3>
    <script type="text/javascript">
      function run() {
        var xhr = createXMLHttpRequest();

        /* 与服务器创建连接 */
        xhr.open("GET", "/ServletTest/ServletAjax1?username=zhangsan",
                 true);
        /* 发送ajax请求 */
        xhr.send(null);
        // 监听 xhr状态的方法
        /*
			readyState状态码：
			0：未初始化
			1：正在加载
			2：加载完成
			3：请求进行中
			4：请求完成
			 */

        xhr.onreadystatechange = function() {
          if (xhr.readyState == 1) {
            alert("正在加载");
          }
          if (xhr.readyState == 2) {
            alert("加载完成");
          }
          if (xhr.readyState == 3) {
            alert("请求进行中");
          }
          if (xhr.readyState == 4 && xhr.status == 200) {
            alert("请求完成");
            var text = xhr.responseText;
            document.getElementById("a1").innerHTML = text;
          }
        }

      }

      /* 原生ajax */
      /* XMLHttpRequest创建方式与浏览器的内核有关 */
      function createXMLHttpRequest() {
        try {
          //非IE内核浏览器
          return new XMLHttpRequest();
        } catch (e) {
          //IE浏览器
          /* 	对老版 ie 6.0做兼容 */
          try {
            return new ActiveXOject("Msxml2.XMLHTTP");
          } catch (e) {

            /* 	说明它是 ie5.5 */

            try {
              return new ActiveXOject("Microsoft.XMLHTTP");
            } catch (e) {
              throw e;
            }

          }

        }

      }
    </script>
  </body>
</html>
```

```java
@WebServlet("/ServletAjax1")
public class ServletAjax extends HttpServlet {

  private static final long serialVersionUID = 1L;

  protected void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
    System.out.println(1111);
    response.getWriter().write("hello ajax");
  }

  protected void doPost(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
    doGet(request, response);
  }

}
```

## 2.2.传参数

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



    <form action="" methd="post">

      用户名:<input id="name" type="text" name="username" onblur="run()"/>
      <span id="uspan"></span><br/>
      密码：<input type="password" name="password"/> <br/>
      <input type="submit" value="注册"/>

    </form>

    <script type="text/javascript">
      function run(){
        var xhr=createXMLHttpRequest();

        /* 与服务器创建连接 */
        xhr.open("POST","/ServletTest/ServletAjax2",true);

        xhr.setRequestHeader("Content-Type","application/x-www-form-urlencoded");
        var username = document.getElementById("name").value;
        xhr.send("username="+username);
        // 监听 xhr状态的方法
        xhr.onreadystatechange =function(){

          if(xhr.readyState==4 &&xhr.status==200){
            var text = xhr.responseText;

            document.getElementById("uspan").innerHTML=text;
          }
        }


      }

      function createXMLHttpRequest(){
        try{
          return new XMLHttpRequest();
        } catch (e){
          /* 	对老版 ie 6.0做兼容 */

          try{
            return new ActiveXOject("Msxml2.XMLHTTP");
          }catch(e){

            /* 	说明它是 ie5.5 */

            try{
              return new ActiveXOject("Microsoft.XMLHTTP");
            }catch(e){
              throw e;
            }

          }

        }

      }

    </script>
  </body>
</html>
```

```java
@WebServlet("/ServletAjax2")
public class ServletAjax2 extends HttpServlet {

  private static final long serialVersionUID = 1L;

  protected void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
    String username = request.getParameter("username");

    System.out.println(username);
    response.setContentType("text/html;charset=utf-8");
    if (username.equals("zhangsan")) {
      response.getWriter().write("<h1>"+"用户名已经被注册"+"<h1>");
    }else {
      response.getWriter().write("<h1>"+"用户名可用"+"<h1>");
    }

  }

  protected void doPost(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
    doGet(request, response);
  }

}
```

## 2.3.返回格式为xml

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

    <button onclick="run()">an</button>
    <script type="text/javascript">
      function run(){
        var xhr=createXMLHttpRequest();

        /* 与服务器创建连接 */
        xhr.open("GET","/ServletTest/SerlvetAjax3",true);


        xhr.send(null);
        // 监听 xhr状态的方法
        xhr.onreadystatechange =function(){

          if(xhr.readyState==4 &&xhr.status==200){
            /* document对象 */
            var doc = xhr.responseXML; 
            //获取stu节点 所有节点 
            var stu = doc.getElementsByTagName("stu")[0];
            var name=stu.getAttribute("name");
            console.info(name);


            var age =stu.getElementsByTagName("age")[0];

            var agetext =age.textContent;

            console.info(agetext);

            var msg = name+"-"+agetext;


          }
        }


      }

      function createXMLHttpRequest(){
        try{
          return new XMLHttpRequest();
        } catch (e){
          /* 	对老版 ie 6.0做兼容 */

          try{
            return new ActiveXOject("Msxml2.XMLHTTP");
          }catch(e){

            /* 	说明它是 ie5.5 */

            try{
              return new ActiveXOject("Microsoft.XMLHTTP");
            }catch(e){
              throw e;
            }

          }

        }

      }

    </script>
  </body>
</html>
```

```java
package net.wanho.ajax;

import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * @author Administrator  E-mail: example@aliyun.com
 * @version 创建时间：2018年6月6日  下午1:33:35
 * tags
 */
@WebServlet("/SerlvetAjax3")
public class SerlvetAjax3 extends HttpServlet {

  private static final long serialVersionUID = 1L;

  protected void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
    String xml ="<stus><stu name='zhangsan'><age>18</age></stu> </stus>";
    response.setContentType("text/xml;charset=UTF-8");
    response.getWriter().write(xml);
  }

  protected void doPost(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
    doGet(request, response);
  }

}
```

# 3.同步请求和异步请求

- 同步
  - 发送方发出数据后，等接收方发回响应以后才发下一个数据包的通讯方式。用户填写所有信息后，提交给服务器，等待服务器的回应（检验数据），是一次性的。信息错误又要重新填写
- 异步
  - 发送方发出数据后，不等接收方发回响应，接着发送下个数据包的通讯方式。
- 区别
  - 当用户填写完一条信息后，该信息会自动向服务器提交，然后服务器响应客户端，在此过程中，用户依然在填写表格的信息，即向服务器请求多次，节省了用户的时间，提高了用户的体验。（表单失去焦点验证）

# 4.Jquery的ajax方法

使用原生的ajax较为复杂，Jquery也提供了ajax的方法，简化了代码，提高了效率

- 格式

```
$.ajax({name:value, name:value, ... })
```

- 所有可能的参数值
  - 常用的参数
    - async，contentType，data，dataType，type
    - 两个重要的函数：success,error

| 名称                           | 值/描述                                     |
| ---------------------------- | ---------------------------------------- |
| async                        | 布尔值，表示请求是否异步处理。默认是 true。                 |
| beforeSend(*xhr*)            | 发送请求前运行的函数。                              |
| cache                        | 布尔值，表示浏览器是否缓存被请求页面。默认是 true。             |
| complete(*xhr,status*)       | 请求完成时运行的函数（在请求成功或失败之后均调用，即在 success 和 error 函数之后）。 |
| contentType                  | 发送数据到服务器时所使用的内容类型。默认是："application/x-www-form-urlencoded"。 |
| context                      | 为所有 AJAX 相关的回调函数规定 "this" 值。             |
| data                         | 规定要发送到服务器的数据。                            |
| dataFilter(*data*,*type*)    | 用于处理 XMLHttpRequest 原始响应数据的函数。           |
| dataType                     | 预期的服务器响应的数据类型。                           |
| error(*xhr,status,error*)    | 如果请求失败要运行的函数。                            |
| global                       | 布尔值，规定是否为请求触发全局 AJAX 事件处理程序。默认是 true。    |
| ifModified                   | 布尔值，规定是否仅在最后一次请求以来响应发生改变时才请求成功。默认是 false。 |
| jsonp                        | 在一个 jsonp 中重写回调函数的字符串。                   |
| jsonpCallback                | 在一个 jsonp 中规定回调函数的名称。                    |
| password                     | 规定在 HTTP 访问认证请求中使用的密码。                   |
| processData                  | 布尔值，规定通过请求发送的数据是否转换为查询字符串。默认是 true。      |
| scriptCharset                | 规定请求的字符集。                                |
| success(*result,status,xhr*) | 当请求成功时运行的函数。                             |
| timeout                      | 设置本地的请求超时时间（以毫秒计）。                       |
| traditional                  | 布尔值，规定是否使用参数序列化的传统样式。                    |
| type                         | 规定请求的类型（GET 或 POST）。                     |
| url                          | 规定发送请求的 URL。默认是当前页面。                     |
| username                     | 规定在 HTTP 访问认证请求中使用的用户名。                  |
| xhr                          | 用于创建 XMLHttpRequest 对象的函数。               |

- 案例(各参数详解)

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

    <span id="span"></span>

  </body>
  <script type="text/javascript" src="/ServletTest/js/jquery-3.0.0.js"></script>
  <script type="text/javascript">
    $.ajax({
      /* 多个参数之间用逗号隔开 */
      /* 请求路径 */
      url : "/ServletTest/login",
      /*请求方式 ("POST" 或 "GET")， 默认为 "GET"。 */
      type : "get",
      /* 
		预期服务器返回的数据类型。如果不指定，jQuery 将自动根据 HTTP 包 MIME 信息来智能判断，比如 XML MIME 类型就被识别为 XML。在 1.4 中，JSON 就会生成一个 JavaScript 对象，而 script 则会执行这个脚本。随后服务器端返回的数据会根据这个值解析后，传递给回调函数。可用值:
		"xml": 返回 XML 文档，可用 jQuery 处理。
		"html": 返回纯文本 HTML 信息；包含的 script 标签会在插入 dom 时执行。
		"script": 返回纯文本 JavaScript 代码。不会自动缓存结果。除非设置了 "cache" 参数。注意：在远程请求时(不在同一个域下)，所有 POST 请求都将转为 GET 请求。（因为将使用 DOM 的 script标签来加载）
		"json": 返回 JSON 数据 。
		"jsonp": JSONP 格式。使用 JSONP 形式调用函数时，如 "myurl?callback=?" jQuery 将自动替换 ? 为正确的函数名，以执行回调函数。
		"text": 返回纯文本字符串
		 */
      datatype : "text",
      /* 发送到服务器的数据
		必须为 Key/Value 格式	
		 */
      data : "",
      /* 回调函数，响应成功之后调用 */
      success : function(data) {
        console.log(data);
        $("#span").html(data);
      },
      /* 回调函数，响应失败之后调用 */
      error : function() {
        alert("失败了");
      }

    })
  </script>

</html>
```

```java
@WebServlet("/login")
public class SerlvetAjax4 extends HttpServlet {

  private static final long serialVersionUID = 1L;

  protected void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {


    response.getWriter().write("hello world");

  }

  protected void doPost(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
    doGet(request, response);
  }

}
```

## 4.1.data的传值方法

- 参数直接传值

```jsp
data : {username:"zhangsan",password:"123456"},
```

- 参数封装成对象传值

```jsp
var user = {
  username : "zhangsan",
  password : "123456"
}
data:user
```

- 表单序列化传值(ajax 提交表单)
  - 服务器代码参照章节4

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

    <form action="" methd="post" id="frm">

      用户名:<input id="name" type="text" name="username" /> <span id="uspan"></span><br />
      密码：<input type="password" name="password" /> <br />
    </form>
    <input type="button" onclick="submit()" value="注册" />

    <span id="span"></span>

  </body>
  <script type="text/javascript" src="/ServletTest/js/jquery-3.0.0.js"></script>
  <script type="text/javascript">
    function submit() {
      $.ajax({
        url : "/ServletTest/login2",
        type : "get",
        datatype : "text",
        data : $("#frm").serialize(),
        success : function(data) {
          console.log(data);
          $("#span").html(data);
        },
        error : function() {
          alert("失败了");
        }
      })
    }
  </script>

</html>
```

# 5.Json

## 5.1.Json简介

- JSON 指的是 JavaScript 对象表示法（**J**ava**S**cript **O**bject **N**otation）
- JSON 是轻量级的文本数据交换格式
- JSON 独立于语言：JSON 使用 Javascript语法来描述数据对象，但是 JSON 仍然独立于语言和平台。JSON 解析器和 JSON 库支持许多不同的编程语言。 目前非常多的动态（PHP，JSP，.NET）编程语言都支持JSON。
- JSON 具有自我描述性，更易理解

## 5.2.Json语法

- 数据在名称/值对中
- 数据由逗号分隔
- 大括号保存对象（json对象）
- 中括号保存数组（json数组）

```json
var sites = [
    { "name":"runoob" , "url":"www.runoob.com" }, 
    { "name":"google" , "url":"www.google.com" }, 
    { "name":"微博" , "url":"www.weibo.com" }
];
```

## 5.3.Java转 Json

### 5.3.1.加入jar包

fastjson-1.2.28.jar

### 5.3.2.Java对象转Json对象

新建一个user对象

```java
public class User {

  private String name;
  private int age;



  public User() {
    super();
    // TODO Auto-generated constructor stub
  }
  public User(String name, int age) {
    super();
    this.name = name;
    this.age = age;
  }
  public String getName() {
    return name;
  }
  public void setName(String name) {
    this.name = name;
  }
  public int getAge() {
    return age;
  }
  public void setAge(int age) {
    this.age = age;
  }
  @Override
  public String toString() {
    return "User [name=" + name + ", age=" + age + "]";
  }
}
```

```java
public void test() {
  User user=new User("zhangsan",12);
  JSONObject jsonObject=new JSONObject();

  jsonObject.put("user", user);
  System.out.println(jsonObject.toString());

  String jsonString = jsonObject.toJSONString(user);
  System.out.println(jsonString);
}
```

### 5.3.3.List转Json对象

```java
@Test
public void test1() {
  User user=new User("zhangsan",12);
  User user1=new User("lisi",12);
  List<User> list=new ArrayList<>();
  list.add(user);
  list.add(user1);
  JSONObject jsonObject=new JSONObject();
  jsonObject.put("userList", list);
  System.out.println(jsonObject.toString());

  String jsonString = jsonObject.toJSONString(list);
  System.out.println(jsonString);
}
```

## 5.4.Json转Java

### 5.4.1.Json对象转Java对象

```java
@Test
public void test2() {
  String json="{'age':12,'name':'zhangsan'}";
  JSONObject jsonObject=new JSONObject();
  User user = jsonObject.parseObject(json,User.class);
  System.out.println(user.getName());
}
```

### 5.4.2.List转Json数组

```java
@Test
public void test3() {
  String json="[{'age':12,'name':'zhangsan'},{'age':12,'name':'lisi'}]";
  JSONObject jsonObject=new JSONObject();
  List<User> list = jsonObject.parseArray(json,User.class);
  System.out.println(list);
}
```

## 5.5. JavaScript转JSON

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

  </body>
  <script type="text/javascript">
    /* JSON.parse(jsonstr); //可以将json字符串转换成json对象 
	JSON.stringify(jsonobj); //可以将json对象转换成json字符串 */

    //可以将json对象转换成json字符串
    var jsonstr = {
      name : "zhangsan",
      age : 20
    }
    var user = JSON.stringify(jsonstr);
    console.log(user);

    //可以将json字符串转换成json对象 
    var jsonstr1 = '{"name":"zhangsan","age":20}';
    var user = JSON.parse(jsonstr1);
    console.log(user.name);


    var jsonstr2 = "{'userList':[{'age':12,'name':'zhangsan'},{'age':12,'name':'lisi'}]}";
    var jsonObject = JSON.parse(jsonstr1);
    console.log(jsonObject.userList);
  </script>

</html>
```



