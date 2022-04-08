## docker网络种类

- Bridge(默认)，网络桥接模式

  - 内部可以通过ip互联，但需要提前知道ip,ip不保证每次都一样
  - docker0,默认的网络，只能通过ip来互联，ip不保证每次都一样
  - 自己定义网络，能通过ip互联，同时也能通过docker name（转成了域名）来互联

- host，宿主机模式，容器直接使用宿主机的网络

- container模式

```shell
#创建一个新的 Docker 网络。
docker network create -d bridge my-net
#运行一个容器并连接到新建的 my-net 网络
docker run -d -it --name busybox1 --network my-net busybox sh
docker run -d -it --name busybox2 --network my-net busybox sh

#在busybox2中ping busybox1,能ping通
```

