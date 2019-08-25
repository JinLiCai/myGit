# 1.WEB开发

## 1.1.WEB开发简介

当前网络上有两种架构

- C/S	Client/Server	客户端/服务器   	需要下载客户端软件	
  - 例子：QQ、快播、暴风影音
  - 优点：服务器压力相对比较小，安全性比较高。
  - 缺点：需要下载客户端软件，总去更新。
- B/SBrowser/Server浏览器/服务器   不需要下载客户端软件（客户端就指浏览器）
  - 例子：购物网站（淘宝  京东） 12306
  - 缺点：服务器压力比较大（硬件比较强）
  - 优点：浏览器，不用更新，服务器端去做更新了。

## 1.2.WEB相关知识

- WEB：网页。
- JavaWeb：使用Java语言来开发网页。

* 静态的WEB资源
  * HTML CSS JavaScript
* 动态的WEB资源
  * Servlet/JSP

* 静态和动态的区别
  * 动态的资源数据是活的，例子：假如说班长登陆淘宝，显示班长的名字。我登陆了淘宝，显示我的名字。

  * 微软ASP.net
  * PHP小巧（开发网站非常强大，处理大数据）
  * RUBY（日本 面向对象的脚本语言）

* Java语言优点：在开发前台网站方面优势不是特别明显，优势是服务器端，处理业务（电信，电商，保险，银行）。

* 静态Web资源：简单一句话，浏览器能看的懂的。
* 动态Web资源：先需要服务器把它转换成HTML，再给浏览器看。

# 2.服务器

## 2.1.服务器的简介

* 服务器整体概念：
  * 硬件：一台电脑。
  * 软件：服务器的软件，Tomcat服务器软件。
* 如果安装了服务器软件了，启动服务器和关闭服务器。假如启动 了服务器，怎么访问？
  * 访问：http://www.baidu.com	一回车访问百度了
    * http://		代表HTTP的协议
      * www.baidu.com域名（DNS域名服务器注册.baidu.com  61.135.169.125）
  * 最终：http://192.168.1.100:端口号（默认值80）
  * 最终：http://192.168.1.100:80/index.html

## 2.2.常见的WEB服务器

* Tomcat（Apache）	开源免费的	开发中应用最广的服务器	支持JSP/Servlet规范	SSH
  * JBoss（有开源的也有闭源的） 免费的	   支持JAVAEE所有的规范	EJB规范 JSP/Servlet
* Weblogic  原来的公司BEA公司收费的 大型的服务器支持JAVAEE所有的规范 被Oracle收购了
  SUM公司（Java语言）+ 数据库（Oracle MySQL（也被收购了））+  服务器（Weblogic）
* Websphere 公司的IBM公司     收费  大型的服务器支持JAVAEE所有的规范

## 2.3.Tomcat服务器

* 下载tomcat服务器，安装版本和解压版本。现在都使用解压版本（7.x）
* 解压文件，放在本地的磁盘上（目录：不要有中文和空格）
* 启动服务器：在tomcat/bin/startup.bat（批处理文件），双击文件。弹出黑色的窗口。服务器成功。（不要把黑窗口关闭）
  * 访问服务器的主页：http://localhost:8080就可以访问tomcat默认主页
* 关闭服务器：（关闭黑窗口，关闭暴力的），温柔的关闭。在bin的目录下，有shutdown.bat。双击该文件，关闭服务器。

## 2.4.注意问题

* 第一个注意：必须安装JDK，必须配置JAVA_HOME环境变量（按照名字映射，必须一样才能找到运行环境）。窗口一闪而过。说明环境变量没配置好。
* 不小心，已经启动了一个服务器，又想启动服务器。端口占用的问题。
  * 端口占用的问题：java.net.BindException: Address already in use: JVM_Bind
  * 解决占用的问题：
    * 先找到占用端口的应用程序，结束掉该应用程序。
      * netstat  –ano	查看所有占用端口的应用程序，找到程序的PID，要任务任务管理器中结束掉。	
    * 有一个应用一直占用，一开机就占用。
      * 修改端口号（修改tomcat服务器的端口号）。（默认是8080，改成其他的端口号）
        * Tomcat服务器的配置文件-- tomcat/conf/server.xml的文件
      * 一般情况下改成80，80端口是HTTP协议的默认端口号，访问可以不写。
      * 如果万一占用的80端口，干掉它。系统中的服务要是占用80端口，禁用该服务。

* 如果系统自带的微软服务器IIS（World wide web publish IIS），去系统服务中把服务禁用。

## 2.5.Tomcat目录结构

bin				可执行文件（启动和关闭）
conf			存放的Tomcat配置文件
lib				给Tomcat服务器运行时所需jar
logs				存放Tomcat运行时产生日志文件。
temp			Tomcat运行时产生临时文件
webapps		Wab Applicatons（WEB应用们），在该目录下存放就是项目。
work			JSP翻译成.java的文件，存放在work的目录下。

## 2.6.在webapps目录创建静态和动态的WEB资源

* webapps目录下存放的是项目，项目区分静态的WEB资源和动态的WEB资源。
* 静态和动态在webapps的目录下存在的方式不一样。
  * 如果静态的WEB资源 -- 在webapps目录创建一个文件（项目名称） -- 直接可以放在静态资源（HTML CSS JS）
  * 如果动态的WEB资源 
    * 在webapps目录下创建一个文件
    * 在该文件下创建WEB-INF的目录（名称固定、大写固定）
    * 在WEB-INF目录下web.xml的文件（必须要有，有文档声明，根节点和约束，复制一份）
      * 在WEB-INF目录下	classes文件夹（.class文件）
        * 在WEB-INF目录下lib文件夹（引入第三方jar包）

## 2.7.Eclipse和服务器集成

* Eclipse是开发工具（编写代码）
* Tomcat服务器：运行的项目
* Eclipse和Tomcat集成的步骤
  * window -- 首选项 -- MyEclipse -- servers -- Tomcat7.x -- 配置JDK -- 配置Tomcat目录 -- Enable，点击ok
  * 启动 -- 在server窗口中 -- 右键选择启动和关闭

* 如何在MyEclipse部署项目。

## 2.8.Context上下文（虚拟路径）

* 虚拟路径：理解访问路径（默认和项目名称是相同的）。
* 发布到服务器中，作为访问路径。
* 总结：在webapps的目录下的项目的名称其实是虚拟路径（访问路径），虚拟的路径默认情况下和项目名称是相同的。

## 2.9.部署项目（两种方式）

* 开放目录部署方式
  * 直接把项目复制到webapps的目录下
* 把应用打成war包。（演示）
  * 原因：需要把你的系统部署到公司的服务器。
  * 用开发工具把应用打成war包
  * 把war包直接复制到webapps下，应用自动解压

## 2.10.WEB通信

如下图

![1](E:\wanhe\pictures\第四阶段\1.png)

# 3.HTTP协议

## 3.1.HTTP协议概述

 HTTP是HyperText Transfer Protocol(超文本传输协议)的简写，传输HTML文件。

用于定义WEB浏览器与WEB服务器之间交换数据的过程及数据本身的格式。

* 什么是HTTP的协议：协议：甲乙双方根据一些规定达成的共识。人与人之间的协议。
* 人与计算机怎么沟通呢？人通过浏览器与计算机的服务器进行沟通。
* 客户端与服务器之间怎么沟通：涉及到数据的传输。
  * 搜索万和，将万和这个信息传到服务器端，服务器端接受到万和，服务器内部查找内容，查询的结果返回给浏览器。
* 万和是怎么传输啊？图片或者html的内部怎么传输啊？
* HTTP的协议
  * 把万和数据封装到协议规定的格式里，发送到服务器。
  * 服务器把HTML，图片的数据封装到协议的规定的格式，返回给浏览器。
* HTTP协议的格式
  * 咱们要学的是这些格式？这是格式有一些内容，需要学的？
* 请求：从客户端发起，向服务器端发送请求。
* 响应：从服务器做出回应，接收到客户端发送过来的请求，对客户端做出了响应。

## 3.2.HTTP协议的版本

* HTTP协议1.0	
  * 从客户端链接服务器端，发送请求，得到响应。立即断开。
* HTTP协议1.1（现在使用）
  * 从客户端链接服务器端，发送请求，得到响应。不会立即断开，链接一会，如果一段时间内，没有请求，自动断开。

## 3.3.HTTP协议的请求

* 请求行
  * GET  /day08_02/1.html  HTTP/1.1
  * 请求方式
    * 提交方式有很多，主要有两种，get和post。之间区别：
      * GET：明文传输 不安全，数据量有限，不超过1kb（GET /day08_02/1.html?uName=tom&pwd=123 HTTP/1.1）
      * POST: 暗文传输，安全。数据量没有限制。
    * 提交的地址（URI）：统一资源标识符。去协议和IP地址  例: /day08_02/1.html
    * 协议版本HTTP/1.1
* 请求头
  - Accept: text/html,image/*     浏览器可接受的MIME类型 告诉服务器客户端能接收什么样类型的文件。
  - Accept-Charset: ISO-8859-1  浏览器通过这个头告诉服务器，它支持哪种字符集
  - Accept-Encoding: gzip   浏览器能够进行解码的数据编码方式，比如gzip
  - Accept-Language:zh-cn   浏览器所希望的语言种类，当服务器能够提供一种以上的语言版本时要用到。 可以在浏览器中进行设置。
  - Host: www.wanho.net:80  初始URL中的主机和端口 
  - If-Modified-Since: Tue, 11 Jul 2000 18:23:51 GMT   利用这个头与服务器的文件进行比对，如果一致，则从缓存中直接读取文件。
  - Referer: http://www.wanho.net/index.jsp   包含一个URL，用户从该URL代表的页面出发访问当前请求的页面
  - User-Agent: Mozilla/4.0 (compatible; MSIE 5.5; Windows NT 5.0)  浏览器类型
  - Connection: close/Keep-Alive     表示是否需要持久连接。如果服务器看到这里的值为“Keep -Alive”，或者看到请求使用的是HTTP 1.1（HTTP 1.1默认进行持久连接
  - Date: Tue, 11 Jul 2000 18:23:51 GMT   请求时间GMT
* 重点的有
  * If-Modified-Since		需要和响应头和304（状态码）和在一起使用，控制本地的缓存。
    * Referer		记住当前网页的来源（作用：统计网站的访问，防止盗链）
      * User-Agent获取浏览器的版本信息
* 请求体
  * 封装的是post提交方式的参数列表。

## 3.4.HTTP协议的响应

* 响应行
  * 协议版本
  * 状态码（重点记住）
    * 200 ：请求成功处理，一切OK		
    * 302 ：请求重定向
    * 304 ：服务器端资源没有改动，通知客户端查找本地缓存 
    * 404 ：客户端访问资源不存在
    * 500 ：服务器内部出错 

  * 状态码描述
* 响应头
  Location: http://www.it315.org/index.jsp  指示新的资源的位置  通常和302/307一起使用，完成请求重定向
  Server:apache tomcat        指示服务器的类型
  Content-Encoding: gzip      服务器发送的数据采用的编码类型
  Content-Length: 80             告诉浏览器正文的长度
  Content-Language: zh-cn   服务发送的文本的语言
  Content-Type: text/html; charset=GB2312    服务器发送的内容的MIME类型
  Last-Modified: Tue, 11 Jul 2000 18:23:51 GMT   文件的最后修改时间
  Refresh: 1;url=http://www.it315.org    指示客户端刷新频率。单位是秒
  Content-Disposition: attachment; filename=aaa.zip   指示客户端下载文件
  Expires: -1
  Cache-Control: no-cache  
  Pragma: no-cache      表示告诉客户端不要使用缓存（一般以上三个一起使用）
  Connection: close/Keep-Alive   
  Date: Tue, 11 Jul 2000 18:23:51 GMT
  * 重点的响应头
    * Location				和302一起完成重定向
    * Last-Modified和 If-Modified-Since 和304一起来完成控制缓存的操作。
      * Refresh	定时页面刷新（页面定时跳转）
    * Content-Disposition文件下载的时候需要使用
  * 下面这三个头需要一起使用
    Expires: -1
    Cache-Control: no-cache  
    Pragma: no-cache
    作用：禁用浏览器缓存。
* 响应体：服务器向客户端返回的数据（和网页右键“查看源码”看到的内容一样）。