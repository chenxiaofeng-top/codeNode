## **Docker** 包括三个基本概念

Docker 不是虚拟机，容器就是进程。既然是进程，那么在启动容器的时候，需要指定所运行的程序及参数。

- **镜像**（`Image`），与java的类类似，相当于代码模板
- **容器**（`Container`），与java的对象一样，通过代码模板创建
- **仓库**（`Repository`），与git类似
- **数据卷**，与本地数据库或配置文件类似

## 安装 Docker

- 查开阿里云：https://developer.aliyun.com/mirror/docker-ce?spm=a2c6h.13651102.0.0.68001b11jwHVOD

## 数据卷

- 可以在容器之间共享和重用
- 对数据卷的修改会立马生效
- 对数据卷的更新，不会影响镜像
- 数据卷默认会一直存在，即使容器被删除

## 网络

## Docker Compose

封装docker命令，命令变成配置文件，一键运行

## 基本命令

容器的运行，镜像的操作

## Dockerfile

自定义镜像