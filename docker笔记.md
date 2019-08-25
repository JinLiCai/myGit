关闭docker容器中的tomcat

1. 在win中cmd.exe 输入 docker ps 
2. docker stop  CONTAINER ID(d7598d9e98ef)



**docker images :** 列出本地镜像。

**docker rmi :** 删除本地一个或多少镜像

**docker run ：**创建一个新的容器并运行一个命令

**docker rm ：**删除一个或多少容器

**docker search :** 从Docker Hub查找镜像

1. **--automated :**只列出 automated build类型的镜像；
2. **--no-trunc :**显示完整的镜像描述
3. **-s :**列出收藏数不小于指定值的镜像。

**docker pull :** 从镜像仓库中拉取或者更新指定镜像

docker run -p 8080:8080 tomcat:从docker中运行tomcat



```
docker ps -a能显示所有docker实例的状态，包含已经退出了的
docker ps -aq加上-q参数，只显示container id
docker rm $(docker ps -aq)删除所有容器实例

使用redis镜像执行redis-cli命令连接到刚启动的容器,主机IP为172.17.0.1
docker exec -it CONTAINERID redis-cli

```



```
docker start redis

将容器打成镜像
docker commit CONTAINER ID 容器名称（完成后的）

docker save -o
```



































