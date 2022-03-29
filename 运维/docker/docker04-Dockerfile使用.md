## Dockerfile 定制镜像

参考地址：https://www.leafage.top/posts/detail/21525V8AP

- 创建一个目录，在这个目录下创建名为**Dockerfile**的文件
- 把需要的文件提示放到当前目录
- Dockerfile的内容
  - 需要基础镜像，用FROM
  - RUN shell脚本，安装和运行linux中需要的服务，是在 docker build。
  - COPY 复制目录下的文件到指定目录
  - CMD 在docker run 时运行。
    - 指令就是用于指定默认的容器主进程的启动命令的
    - 如果Dockerfile中存在多条`CMD`指令命令，只有最后一条会被执行；
    - 如果用户启动容器时候指定了运行的命令，则会覆盖掉`CMD`指定的命令
    - entrypoint格式是在CMD指令和`ENTRYPOINT`指令配合时使用的，`CMD`指令中的参数会被添加到`ENTRYPOINT`指令中
    - 如果使用`CMD`为`ENTRYPOINT`指令提供默认参数，`CMD`和`ENTRYPOINT`指令都应以JSON数组格式指定
    - ...
- 运行docker build -t nginx:v3 .



## 指令说明

### FROM指令：引用基础镜像

```dockerfile
FROM <image> [AS <name>]
FROM <image>[:<tag>] [AS <name>]
FROM <image>[@<digest>] [AS <name>]
```

### RUN指令：构建容器时执行的命令

```dockerfile
shell 格式：RUN <command> (/bin/sh -c /S /C)
exec 格式：RUN ["executable", "param1", "param2"]
#实例
RUN /bin/bash -c 'source $HOME/.bashrc; echo $HOME'
RUN ["/bin/bash", "-c", "echo hello"]
```

- 安装和运行linux中所需要的服务
- exec：必须双引号，不能是单引号

### CMD指令：

```dockerfile
exec格式（推荐）：CMD ["executable","param1","param2"]
entrypoint格式：CMD ["param1","param2"] 
shell格式：CMD command param1 param2
```

- 在容器运行时执行
- 多个CMD中，只有最后一条会被执行
- 如果用户启动容器时候指定了运行的命令，则会覆盖掉`CMD`指定的命令

### LABEL指令：打标签

```dockerfile
LABEL <key>=<value> <key>=<value> <key>=<value> ...
```

### EXPOSE指令：声明对外暴露的端口

```dockerfile
EXPOSE <port> [<port>/<protocol>...]
```

- 无论`EXPOSE`设置如何，都可以在运行时使用`-p`参数覆盖它们，例如：docker run -p 8080:80；
- `EXPOSE` 指令是声明运行时容器提供服务端口，这只是一个声明，在运行时并不会因为这个声明应用就会对外暴露这个端口，只有在`docker run` 时显示指定 -p [外部端口]:[容器端口]，才会对外暴露。
- 帮助镜像使用者理解这个镜像服务的守护端口，以方便配置映射；
- 在运行时使用随机端口映射时，也就是 `docker run -P` 时，会自动随机映射 `EXPOSE` 的端口。

### ENV指令：

```dockerfile
设置一个：ENV <key> <value>
设置多个：ENV <key>=<value> <key1>=<value1> ...
```

- 可以通过命令：`docker run -e "key=value"`来覆盖Dockerfile中的设置项的值

### ADD指令：

```dockerfile
ADD [--chown=<user>:<group>] <src>... <dest>
ADD [--chown=<user>:<group>] ["<src>",... "<dest>"]
#实例
ADD https://oss.abeille.top/demo-0.0.1-SNAPSHOT.jar /app
ADD . /app
```

-  `ADD` 指令要比 `COPY` 指令功能更加多，但是根据 Docker 最佳实践的说明，除非需要解压缩功能，否则要尽可能的使用 `COPY` 指令，因为 `COPY` 的语义很明确，就是复制文件而已

### COPY指令：

```dockerfile
COPY [--chown=<user>:<group>] <src>... <dest>
COPY [--chown=<user>:<group>] ["<src>",... "<dest>"]
#实例
COPY /target/demo-0.0.1-SNAPSHOT.jar .
```

### ENTRYPOINT指令：

```dockerfile
exec格式：ENTRYPOINT ["executable", "param1", "param2"]
shell格式：ENTRYPOINT command param1 param2
```

- `ENTRYPOINT`指令和 `CMD` 相似，都可以让容器在每次启动时执行相同的命令，但是又有不同的地方，`CMD`可以是命令，也可以是参数，而`ENTRYPOINT`只能是命令。

### VOLUME指令：

```dockerfile
VOLUME ["/data"]
```

- 如果用户忘记挂载数据卷，则把该目录挂载到主机上，防止容器中写入大量数据
- 挂载到默认目录/var/lib/docker/volumes下，匿名（随机名）
- 作为防范作用

### USER指令：

```dockerfile
USER <user>[:<group>]
USER <UID>[:<GID>]
#实例
RUN groupadd -r dev && useradd -r -g dev dev
USER dev
RUN [ "systemctl start elasticsearch" ]
```

- 指定运行容器时的用户名或 UID，后续的 `RUN` 也会使用指定用户。当服务不需要管理员权限时，可以通过该命令指定运行用户。并且可以在之前创建所需要的用户

### WORKDIR指令：工作目录

```dockerfile
WORKDIR /path/to/workdir
#实例
FROM openjdk:8-jdk-alpine
WORKDIR /everyday
WORKDIR chain
RUN pwd  #/everyday/chain


```

- 认为容器的工作目录
- 可能会与数据卷绑定
- 可能会保存创建镜像的信息
- 容器交互时，进入的目录

### ARG指令：

```dockerfile
ARG <name>[=<default value>]
```

- 构建参数和 `ENV` 的效果一样，都是设置环境变量。所不同的是，`ARG` 所设置的构建环境的环境变量，在将来容器运行时是不会存在这些环境变量的。通过 `docker history` 可以看到所有设置的值。

### ONBUILD :为他人作嫁衣裳

```dockerfile
ONBUILD [其它指令]
```

- `ONBUILD` 是一个特殊的指令，它后面跟的是其它指令，比如 `RUN`, `COPY` 等，而这些指令，在当前镜像构建时并不会被执行。只有当以当前镜像为基础镜像，去构建下一级镜像的时候才会被执行。

