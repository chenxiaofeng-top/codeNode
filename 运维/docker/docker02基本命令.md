## 容器

```shell
#运行一个容器
docker run -it -d -p 3306:3306 ubuntu:18.04 /bin/bash
#常用
-d: 后台运行容器，并返回容器ID
-i: 以交互模式运行容器，通常与 -t 同时使用
-t: 为容器重新分配一个伪输入终端，通常与 -i 同时使用
-p: 指定端口映射，格式为：主机(宿主)端口:容器端口
--name="nginx-lb": 为容器指定一个名称
-e username="ritchie": 设置环境变量
--volume , -v: 绑定一个卷
-m :设置容器使用内存最大值
-w, --workdir="": 指定容器的工作目录,之后执行的命令都在指定的目录（相当进入到指定目录），默认在/home/docker/目录
--restart always: 重启方式
          no：容器退出时不重启;
          on-failure：容器故障退出（返回值非零）时重启;
          always：容器退出时总是重启    
#不常用
-a stdin: 指定标准输入输出内容类型，可选 STDIN/STDOUT/STDERR 三项
-P: 随机端口映射，容器内部端口随机映射到主机的端口
--dns 8.8.8.8: 指定容器使用的DNS服务器，默认和宿主一致
--dns-search example.com: 指定容器DNS搜索域名，默认和宿主一致
-h "mars": 指定容器的hostname
--env-file=[]: 从指定文件读入环境变量
--cpuset="0-2" or --cpuset="0,1,2": 绑定容器到指定CPU运行
--net="bridge": 指定容器的网络连接类型，支持 bridge/host/none/container: 四种类型
       bridge 使用docker daemon指定的网桥       
       host    //容器使用主机的网络    
       container:NAME_or_ID  >//使用其他容器的网路，共享IP和PORT等网络资源    
       none 容器使用自己的网络（类似--net=bridge），但是不进行配置   
--link=[]: 添加链接到另一个容器
--expose=[]: 开放一个端口或一组端口


#容器列表，-a包含stop的
docker container ls -a
docker ps -a

#指定容器日志
docker container logs [container ID or NAMES]

#指定容器启动/重启/停止/删除
docker start/restart/stop/rm [container ID or NAMES]

#进入容器
docker exec -i 69d1 bash

#清理所有处于终止状态的容器
docker container prune
```

## 镜像

```shell
docker images
docker pull ubuntu:13.10
docker search httpd
docker rmi hello-world
```

## 仓库

- 阿里云 https://cr.console.aliyun.com/cn-hangzhou/instance/dashboard

## 信息查看
