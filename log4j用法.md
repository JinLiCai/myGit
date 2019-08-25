# 1.log4j

​	Log4j是Apache的一个开源项目，通过使用Log4j，我们可以控制日志信息输送的目的地是控制台、文件、GUI组件，甚至是套接口服务器、NT的事件记录器、UNIX Syslog守护进程等；我们也可以控制每一条日志的输出格式；通过定义每一条日志信息的级别，我们能够更加细致地控制日志的生成过程。最令人感兴趣的就是，这些可以通过一个配置文件来灵活地进行配置，而不需要修改应用的代码。

## 1.1.添加jar包

log4j.jar

## 1.2.创建配置文件 log4j.properties

```properties
### direct log messages to stdout ###
log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.stdout.Target=System.out
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=%d{ABSOLUTE} %5p %c{1}:%L - %m%n

### direct messages to file log ###
log4j.appender.file=org.apache.log4j.FileAppender
log4j.appender.file.File=D:\wanheweb_project2wydt.log
log4j.appender.file.layout=org.apache.log4j.PatternLayout
log4j.appender.file.layout.ConversionPattern=%d{ABSOLUTE} %5p %c{1}:%L - %m%n

### set log levels - for more verbose logging change 'info' to 'debug' ###

log4j.rootLogger=error,stdout,file
```

### 1.2.1.语法

```properties
log4j.rootLogger = [ level ] , appenderName1, appenderName2, …  
```

- level: 是日志记录的优先级，分为OFF、FATAL、ERROR、WARN、INFO、DEBUG、ALL或 者您定义的级别。Log4j建议只使用四个级别，优 先级从高到低分别是ERROR、WARN、INFO、DEBUG。通过在这里定义的级别，您可以控制到应用程序中相应级别的日志信息的开关。比如在这里定 义了INFO级别，则应用程序中所有DEBUG级别的日志信息将不被打印出来。  
- appenderName: 就是指定日志信息输出到哪个地方。您可以同时指定多个输出目的地。  

        例如：log4j.rootLogger＝info,A1,B2,C3 

```properties
org.apache.log4j.ConsoleAppender（控制台），
org.apache.log4j.FileAppender（文件），
org.apache.log4j.DailyRollingFileAppender（每天产生一个日志文件），
org.apache.log4j.RollingFileAppender（文件大小到达指定尺寸的时候产生一个新的文件），
org.apache.log4j.WriterAppender（将日志信息以流格式发送到任意指定的地方）


###  system.out  ###
log4j.appender.A2 =org.apache.log4j.ConsoleAppender
log4j.appender.A2.Threshold=DEBUG
log4j.appender.A2.Target=System.out
log4j.appender.A2.encoding=UTF-8
log4j.appender.A2.layout=org.apache.log4j.PatternLayout
log4j.appender.A2.layout.ConversionPattern=[%x] [%-d{yyyy-MM-dd HH:mm:ss}] [%p] %m%n
 
### file debug ###
log4j.appender.A1 = org.apache.log4j.DailyRollingFileAppender
log4j.appender.A1.File = ../logs/DServerDebug.log
log4j.appender.A1.DatePattern='.'yyyy-MM-dd
###log4j.appender.A1.MaxFileSize=100MB
log4j.appender.A1.encoding=UTF-8
log4j.appender.A1.Append = true
log4j.appender.A1.Threshold = DEBUG
log4j.appender.A1.layout = org.apache.log4j.PatternLayout
log4j.appender.A1.layout.ConversionPattern=[%x] [%-d{yyyy-MM-dd HH:mm:ss}] [%p] %m%n
 
### file INFO ###
log4j.appender.A3 = org.apache.log4j.DailyRollingFileAppender
log4j.appender.A3.File = ../logs/DServerINFO.log
log4j.appender.A3.DatePattern='.'yyyy-MM-dd
###log4j.appender.A3.MaxFileSize=10MB
log4j.appender.A3.encoding=UTF-8
log4j.appender.A3.Append = true
log4j.appender.A3.Threshold = INFO
log4j.appender.A3.layout = org.apache.log4j.PatternLayout
log4j.appender.A3.layout.ConversionPattern=[%x] [%-d{yyyy-MM-dd HH:mm:ss}] [%p] %m%n
 
 
### file WARN ###
log4j.appender.A3 = org.apache.log4j.DailyRollingFileAppender
log4j.appender.A3.File = ../logs/DServerWARN.log
log4j.appender.A3.DatePattern='.'yyyy-MM-dd
###log4j.appender.A3.MaxFileSize=10MB
log4j.appender.A3.encoding=UTF-8
log4j.appender.A3.Append = true
log4j.appender.A3.Threshold = WARN
log4j.appender.A3.layout = org.apache.log4j.PatternLayout
log4j.appender.A3.layout.ConversionPattern=[%x] [%-d{yyyy-MM-dd HH:mm:ss}] [%p] %m%n
  
 
### file ERROR ###
log4j.appender.A4 = org.apache.log4j.DailyRollingFileAppender
log4j.appender.A4.File = ../logs/DServerERROR.log
log4j.appender.A4.DatePattern='.'yyyy-MM-dd
###log4j.appender.A4.MaxFileSize=100MB
log4j.appender.A4.encoding=UTF-8
log4j.appender.A4.Append = true
log4j.appender.A4.Threshold = ERROR
log4j.appender.A4.layout = org.apache.log4j.PatternLayout
log4j.appender.A4.layout.ConversionPattern=[%x] [%-d{yyyy-MM-dd HH:mm:ss}] [%p] %m%n
 
 
# everyday    
log4j.appender.A6=org.apache.log4j.DaliyRollingFileAppender    
log4j.appender.A6.File=../logs/DServerEveryDay.log     
log4j.appender.A6.DatePattern=yyyyMMdd-HH'.log'     
log4j.appender.A6.layout=org.apache.log4j.PatternLayout     
log4j.appender.A6.layout.ConversionPattern=%d{yyyy-MM-dd HH\:mm\:ss} [INFO] %m%n 
```

## 1.3.编写servlet读取配置文件

```java 
public class InitServlet extends HttpServlet {
  private static final long serialVersionUID = 1L;

  /**
	 * @see HttpServlet#HttpServlet()
	 */
  public InitServlet() {
    super();
    // TODO Auto-generated constructor stub
  }

  /**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse
	 *      response)
	 */
  protected void doGet(HttpServletRequest request, HttpServletResponse response)
    throws ServletException, IOException {
    // TODO Auto-generated method stub
    response.getWriter().append("Served at: ").append(request.getContextPath());
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
  public void init(ServletConfig config) throws ServletException {
    // TODO Auto-generated method stub
    super.init(config);
    String path = config.getInitParameter("log4j");

    String realPath = getServletContext().getRealPath(path);
    if (realPath != null) {
      PropertyConfigurator.configure(realPath);
      System.out.println("log4j初始化成功");
    }
  }
}
```

web.xml中的配置

```xml
<servlet>
    <servlet-name>InitServlet</servlet-name>
    <servlet-class>net.wanho.controller.InitServlet</servlet-class>
    <init-param>
      <param-name>log4j</param-name>
      <param-value>/WEB-INF/classes/log4j.properties</param-value>
    </init-param>
    <load-on-startup>1</load-on-startup>
  </servlet>
```

## 1.4.应用

```java
@WebServlet("/TestLog4jServlet")
public class TestLog4jServlet extends HttpServlet {
  private static final long serialVersionUID = 1L;
  private Logger logger=Logger.getLogger(TestLog4jServlet.class);   
  /**
     * @see HttpServlet#HttpServlet()
     */
  public TestLog4jServlet() {
    super();
    // TODO Auto-generated constructor stub
  }

  /**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
	 */
  protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    // TODO Auto-generated method stub
    logger.debug("debug");
    logger.error("error");
    logger.info("info");
    logger.warn("warn");
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

修改配置文件中的输出级别，观察输出的结果。

# 2.权限

权限管理，一般指根据系统设置的安全规则或者安全策略，用户可以访问而且只能访问自己被授权的资源，不多不少。

## 2.1.权限五张表

用户——角色——权限

## 2.2.权限与鉴权

前项校验叫做鉴权

后台校验叫做权限 

# 3.SVN

https://blog.csdn.net/maplejaw_/article/details/52874348