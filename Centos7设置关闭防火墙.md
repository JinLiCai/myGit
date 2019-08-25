# [Centos7设置关闭防火墙](https://www.cnblogs.com/hafiz/p/5874117.html)



CentOS 7.0默认使用的是firewall作为防火墙，要想使用iptables必须重新设置一下。

1.关闭防火墙

```
[root@localhost ~]# systemctl stop firewalld.service
```

2.禁止防火墙开机自启

```
[root@localhost ~]# systemctl disable firewalld.service
```

3.安装iptables service

```
yum -y install iptables-services
```

4.修改防火墙配置，如增加防火墙端口3306

```
vi /etc/sysconfig/iptables 
```

增加以下规则

```
-A INPUT -m state --state NEW -m tcp -p tcp --dport 3306 -j ACCEPT
```

保存退出后

重启防火墙使配置生效

```
[root@localhost ~]# systemctl restart iptables.service
```

设置防火墙开机启动

```
[root@localhost ~]# systemctl enable iptables.service
```

重启系统使设置生效

```
[root@localhost ~]# reboot
```