# Nginx篇--解读nginx配置

**一.前述**

**Nginx安装步骤：**

1.依赖 gcc openssl-devel pcre-devel zlib-devel
​    安装：yum install gcc openssl-devel pcre-devel zlib-devel -y

\2. 安装Nginx
./configure 

\3. make && make install

默认安装目录：
/usr/local/nginx

4.配置Nginx为系统服务，以方便管理
  1、在/etc/rc.d/init.d/目录中建立文本文件nginx
  2、在文件中粘贴下面的内容：

```
#!/bin/sh
#
# nginx - this script starts and stops the nginx daemon
#
# chkconfig:   - 85 15 
# description:  Nginx is an HTTP(S) server, HTTP(S) reverse \
#               proxy and IMAP/POP3 proxy server
# processname: nginx
# config:      /etc/nginx/nginx.conf
# config:      /etc/sysconfig/nginx
# pidfile:     /var/run/nginx.pid
 
# Source function library.
. /etc/rc.d/init.d/functions
 
# Source networking configuration.
. /etc/sysconfig/network
 
# Check that networking is up.
[ "$NETWORKING" = "no" ] && exit 0
 
nginx="/usr/local/nginx/sbin/nginx"
prog=$(basename $nginx)
 
NGINX_CONF_FILE="/usr/local/nginx/conf/nginx.conf"
 
[ -f /etc/sysconfig/nginx ] && . /etc/sysconfig/nginx
 
lockfile=/var/lock/subsys/nginx
 
make_dirs() {
   # make required directories
   user=`nginx -V 2>&1 | grep "configure arguments:" | sed 's/[^*]*--user=\([^ ]*\).*/\1/g' -`
   options=`$nginx -V 2>&1 | grep 'configure arguments:'`
   for opt in $options; do
       if [ `echo $opt | grep '.*-temp-path'` ]; then
           value=`echo $opt | cut -d "=" -f 2`
           if [ ! -d "$value" ]; then
               # echo "creating" $value
               mkdir -p $value && chown -R $user $value
           fi
       fi
   done
}
 
start() {
    [ -x $nginx ] || exit 5
    [ -f $NGINX_CONF_FILE ] || exit 6
    make_dirs
    echo -n $"Starting $prog: "
    daemon $nginx -c $NGINX_CONF_FILE
    retval=$?
    echo
    [ $retval -eq 0 ] && touch $lockfile
    return $retval
}
 
stop() {
    echo -n $"Stopping $prog: "
    killproc $prog -QUIT
    retval=$?
    echo
    [ $retval -eq 0 ] && rm -f $lockfile
    return $retval
}
 
restart() {
    configtest || return $?
    stop
    sleep 1
    start
}
 
reload() {
    configtest || return $?
    echo -n $"Reloading $prog: "
    killproc $nginx -HUP
    RETVAL=$?
    echo
}
 
force_reload() {
    restart
}
 
configtest() {
  $nginx -t -c $NGINX_CONF_FILE
}
 
rh_status() {
    status $prog
}
 
rh_status_q() {
    rh_status >/dev/null 2>&1
}
 
case "$1" in
    start)
        rh_status_q && exit 0
        $1
        ;;
    stop)
        rh_status_q || exit 0
        $1
        ;;
    restart|configtest)
        $1
        ;;
    reload)
        rh_status_q || exit 7
        $1
        ;;
    force-reload)
        force_reload
        ;;
    status)
        rh_status
        ;;
    condrestart|try-restart)
        rh_status_q || exit 0
            ;;
    *)
        echo $"Usage: $0 {start|stop|status|restart|condrestart|try-restart|reload|force-reload|configtest}"
        exit 2
esac
```

**注意修改成自己的安装目录！！！**
3、修改nginx文件的执行权限
​    chmod +x nginx
4、添加该文件到系统服务中去
​    chkconfig --add nginx
​    查看是否添加成功
​    chkconfig --list nginx

启动，停止，重新装载
service nginx start|stop









**二.具体配置**

#工作模式与连接数上限
events
{
#参考事件模型，use [ kqueue | rtsig | epoll | /dev/poll | select | poll ]; epoll模型是Linux 2.6以上版本内核中的高性能网络I/O模型，如果跑在FreeBSD上面，就用kqueue模型。
use epoll;
#单个进程最大连接数（最大连接数=连接数*进程数）
worker_connections 65535;
}
event下的一些配置及其意义
 #单个后台worker process进程的最大并发链接数    
    worker_connections  1024;

并发总数是 worker_processes 和 worker_connections 的乘积

即 max_clients = worker_processes * worker_connections

在设置了反向代理的情况下，max_clients = worker_processes * worker_connections / 4  为什么

为什么上面反向代理要除以4，应该说是一个经验值

根据以上条件，正常情况下的Nginx Server可以应付的最大连接数为：4 * 8000 = 32000

worker_connections 值的设置跟物理内存大小有关

因为并发受IO约束，max_clients的值须小于系统可以打开的最大文件数（小与句柄数）

而系统可以打开的最大文件数和内存大小成正比，一般1GB内存的机器上可以打开的文件数大约是10万左右

我们来看看360M内存的VPS可以打开的文件句柄数是多少：

$ cat /proc/sys/fs/file-max

输出 34336

32000 < 34336，即并发连接总数小于系统可以打开的文件句柄总数，这样就在操作系统可以承受的范围之内

所以，worker_connections 的值需根据 worker_processes 进程数目和系统可以打开的最大文件总数进行适当地进行设置

使得并发总数小于操作系统可以打开的最大文件数目

其实质也就是根据主机的物理CPU和内存进行配置

当然，理论上的并发总数可能会和实际有所偏差，因为主机还有其他的工作进程需要消耗系统资源。

ulimit -SHn 65535

nginx.conf配置文件
#定义Nginx运行的用户和用户组
user www www;

#nginx进程数，建议设置为等于CPU总核心数。
worker_processes 8;

#全局错误日志定义类型，[ debug | info | notice | warn | error | crit ]
error_log /var/log/nginx/error.log info;

#进程文件
pid /var/run/nginx.pid;

#一个nginx进程打开的最多文件描述符数目，理论值应该是最多打开文件数（系统的值ulimit -n）与nginx进程数相除，但是nginx分配请求并不均匀，所以建议与ulimit -n的值保持一致。
worker_rlimit_nofile 65535;

#设定http服务器
http
{
include mime.types; #文件扩展名与文件类型映射表
default_type application/octet-stream; #默认文件类型
#charset utf-8; #默认编码
server_names_hash_bucket_size 128; #服务器名字的hash表大小
client_header_buffer_size 32k; #上传文件大小限制
large_client_header_buffers 4 64k; #设定请求缓
client_max_body_size 8m; #设定请求缓
sendfile on; #开启高效文件传输模式，sendfile指令指定nginx是否调用sendfile函数来输出文件，对于普通应用设为 on，如果用来进行下载等应用磁盘IO重负载应用，可设置为off，以平衡磁盘与网络I/O处理速度，降低系统的负载。注意：如果图片显示不正常把这个改成off。send file  高清图片 大图片 要关闭
autoindex on; #开启目录列表访问，合适下载服务器，默认关闭。
tcp_nopush on; #防止网络阻塞
tcp_nodelay on; #防止网络阻塞
keepalive_timeout 120; #长连接超时时间，单位是秒

**#gzip模块设置gzip on;（节省带宽）**

 \#开启gzip压缩输出gzip_min_length 1k; #最小压缩文件大小gzip_buffers 4 16k; #压缩缓冲区gzip_http_version 1.0; #压缩版本（默认1.1，前端如果是squid2.5请使用1.0）gzip_comp_level 2; #压缩等级gzip_types text/plain application/x-javascript text/css application/xml;#压缩类型，默认就已经包含text/html，所以下面就不用再写了，写上去也不会有问题，但是会有一个warn。gzip_vary on;#limit_zone crawler $binary_remote_addr 10m; #开启限制IP连接数的时候需要使用   **# 虚拟主机一些配置及其意义**  通过nginx可以实现虚拟主机的配置，nginx支持三种类型的虚拟主机配置， **1、基于ip的虚拟主机， （一块主机绑定多个ip地址）** **2、基于域名的虚拟主机（servername）** **3、基于端口的虚拟主机（listen如果不写ip端口模式）** 示例基于虚拟机ip的配置，这里需要配置多个ip server {     listen 192.168.20.20:80;     server_name www.linuxidc.com;     root /data/www; } server {     listen 192.168.20.21:80;     server_name www.linuxidc.com;     root /data/www; }

**nginx.conf下的配置** **http{** **server{**     **#表示一个虚拟主机** **}** **}** **#location 映射（ngx_http_core_module）**

 location [ = | ~ | ~* | ^~ ] uri { ... }     location URI {}:         对当前路径及子路径下的所有对象都生效；     location = URI {}: 注意URL最好为具体路径。         精确匹配指定的路径，不包括子路径，因此，只对当前资源生效；     location ~ URI {}:     location ~* URI {}:   **模式匹配URI**，此处的URI可使用正则表达式，~区分字符大小写，~*不区分字符大小写；     location ^~ URI {}:         不使用正则表达式     优先级：= > ^~ > ~|~* >  /|/dir/  /loghaha.html /logheihei.html ^/log.*html$

**#location匹配规则**

**=前缀的指令严格匹配这个查询。如果找到，停止搜索。** 所有剩下的常规字符串，最长的匹配。如果这个匹配使用^〜前缀，搜索停止。 正则表达式，在配置文件中定义的顺序。 如果第3条规则产生匹配的话，结果被使用。否则，如同从第2条规则被使用 

location 的执行逻辑跟 location 的编辑顺序无关。矫正：这句话不全对，“普通 location ”的匹配规则是“最大前缀”，因此“普通 location ”的确与 location 编辑顺序无关；  但是“**正则 location ”的匹配规则是“顺序匹配，且只要匹配到第一个就停止后面的匹配”；** “普通location ”与“正则 location ”之间的匹配顺序是？**先匹配普通 location ，再“考虑”匹配正则 location 。** 注意这里的“考虑”是“可能”的意思，也就是说匹配完“普通 location ”后，有的时候需要继续匹配“正则 location ”，有的时候则不需要继续匹配“正则 location ”。两种情况下，不需要继续匹配正则 location ： （ 1 ）当普通 location 前面指定了“ ^~ ”，特别告诉 Nginx 本条普通 location 一旦匹配上，则不需要继续正则匹配； （ 2 ）当普通location 恰好严格匹配上，不是最大前缀匹配，则不再继续匹配正则  loghaha.html l:  logha l:  ^~ loghah l:  loghaha.html l:  =loghaha.html l:   ^logh.*html$ l:   ^logha.*html$

 **#执行逻辑（！！！）** 

**nginx  收到请求头：判定ip，port，hosts决定server** **nginx location匹配：用客户端的uri匹配location的uri** 先普通 顺序无关 最大前缀 匹配规则简单 打断： ^~ 完全匹配 再正则 不完全匹配 正则特殊性：一条URI可以和多条location匹配上 有顺序的 **先匹配，先应用，即时退出匹配** 

**ps: location中的    / 跟**

**html: 相对于nginx目录(默认是找寻Nginx中的当前HTML目录)**

**ps1 :(反向代理理解)**

通常的代理服务器，只用于代理内部网络对Internet的连接请求，**客户机必须指定代理服务器,**并将本来要直接发送到Web服务器上的http请求发送到代理服务器中由代理服务器向Internet上的web服务器发起请求，最终达到客户机上网的目的。  反向代理（Reverse Proxy）方式是指以**代理服务器来接受internet上的连接请求，然后将请求转发给内部网络上的服务器**，并将从服务器上得到的结果返回给internet上请求连接的客户端，此时代理服务器对外就表现为一个反向代理服务器

**PS2：总结**

**=绝对匹配**

**~\* 正则匹配**

**\.把点转义**

**/最大前缀匹配**  

**·~最大前缀匹配**  

**先找不是正则的 然后找正则的 先匹配先应用**

**host：决策server负责处理** **uri：决策location** **反向代理：proxy_pass  ip:port[uri];**

proxy_pass 反向代理

![img](https://ask.qcloudimg.com/http-save/yehe-2056975/hescv1k4p9.png?imageView2/2/w/1620)

**不带斜线：将uri透传过去**

**带斜线：访问反向代理的主页 将URI屏蔽掉**  

**配置负载均衡（反向代理）!!!!!**

**upstream  httpd-servers {**

**}**

![img](https://ask.qcloudimg.com/http-save/yehe-2056975/ngbatudyv0.png?imageView2/2/w/1620)

**httpd-servers upstreams 名字**

![img](https://ask.qcloudimg.com/http-save/yehe-2056975/3xkm17flmw.png?imageView2/2/w/1620)

 PS3.修改默认HTML目录

```javascript
server {
    listen       80;
    server_name  localhost;
 
    #charset koi8-r;
    #access_log  /var/log/nginx/log/host.access.log  main;
 
    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
    }
 
    #error_page  404              /404.html;
```

 默认路径为/usr/share/nginx/html 修改完后的目录为 /usr/share/alsa/pcm/default.conf。

**修改nginx目录报错403解决办法**  刚好我就遇到了，一查发现是权限不足引起；  **chmod -R 755 /usr/share/nginx/html**  将web目录设置为755权限，-R表示向下递归  chown -R nginx_user:nginx_user   /usr/share/nginx/html 