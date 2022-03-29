## 数据卷

docker提供了三种方式将数据从宿主机挂载到容器中：

- volumes：Docker管理宿主机文件系统的一部分，默认位于 /var/lib/docker/volumes 目录中；（**最常用的方式**）
- bind mounts：意为着可以存储在宿主机系统的任意位置；（**比较常用的方式,但不可移植**）但是，bind mount在不同的宿主机系统时不可移植的，比如Windows和Linux的目录结构是不一样的，bind mount所指向的host目录也不能一样。这也是为什么bind mount不能出现在Dockerfile中的原因，因为这样Dockerfile就不可移植了。
- tmpfs：挂载存储在宿主机系统的内存中，而不会写入宿主机的文件系统；（**一般都不会用的方式**）

```shell
#运行时挂载
#-v后面的映射关系是"宿主目录:容器目录"，宿主目录需要提前存在的，容器目录会自动创建
docker run -d -P \
    --name web \
    # -v /src/webapp:/usr/share/nginx/html:ro      \ #ro权限
    # -v      my-vol:/usr/share/nginx/html nginx   \
    --mount type=bind,source=/src/webapp,target=/usr/share/nginx/html,readonly \
    nginx:alpine
    
   
#创建一个数据卷
docker volume create my-vol
#删除自定义数据卷
docker volume rm  my-vol

#查看指定 数据卷 的信息
docker volume inspect my-vol
# 查看所有容器卷
docker volume ls 
```

