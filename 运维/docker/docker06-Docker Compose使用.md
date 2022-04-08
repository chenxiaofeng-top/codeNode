## compose文件组成

默认文件名：docker-compose.yml

- version
- services
  - web:#服务名称，不可重复
    - image:镜像
    - build:
- networks 
  - 加入指定网络

```yaml
version:'3'
services:
	web: #服务名称，不可重复
		image: #镜像
		build: #Dockerfile镜像，如果同时在存image，image的值作为名称
			 context: ../ #Dockerfile的目录，可以url
			 dockerfile: path/of/Dockerfile #在context下的Dockerfile
		args: #Dockerfile 中的 ARG 指令
		command: #覆盖容器启动后默认执行的命令
		container_name: #容器名称
		depends_on: #依赖容器，
			- db #与web同级的容器
			- redis
		dns: 
		tmpfs: #挂载临时目录到容器内部的tmpfs,与mount 类似
		env_file: #存放变量的文件
		environment: #变量，
			RACK_ENV: development
			- RACK_ENV=development
		expose: #指定暴露的端口
		entrypoint: /code/entrypoint.sh #用于指定接入点
		external_links: #连接到项目配置外部的容器
			- project_db_1:mysql #冒号后面是别名
		extra_hosts: #往容器/etc/hosts增加记录
			- "somehost:162.242.195.82"
		labels: #增加标签
		links: #往容器/etc/hosts增加记录
			- db
			- redis
		logging: #配置日志服务
			driver: syslog
			options:
				syslog-address: "tcp://192.168.0.42:123"
		pid: "host" #访问和操纵其他容器和宿主机的名称空间,不建议使用
		ports:
			- "3000"
			- "8000:8000"
		- "127.0.0.1:8001:8001"
		security_opt: #为每个容器覆盖默认的标签
			- label:user:USER
		stop_signal: SIGUSR1 #置另一个信号来停止容器
		volumes: #数据卷
			- /var/lib/mysql #匿名数据卷
			- /opt/data:/var/lib/mysql #绝对路径挂载数据卷
			- ./cache:/tmp/cache  #相对路径挂载数据卷
			- datavolume:/var/lib/mysql #命名的数据卷
		volumes_from: #与其它容器使用同一数据卷
			- service_name
			- service_name:ro
		cap_add: #指定容器的内核能力（capacity）分配。
			- ALL
		cap_drop: #去掉 NET_ADMIN 能力可以指定为：
			- NET_ADMIN
		deploy: #仅用于 Swarm mode，详细内容请查看 Swarm mode 一节
		working_dir: /code #指定容器中工作目录。
		restart: always #指定容器退出后的重启策略为始终重启
		networks: #加入指定网络。如果不指定，默认myapp_default
            - a-network
            - b-network
	
networks: #自定义网络，如果非发
  a-network:
    driver: bridge
  b-network:
driver: bridge
```

## docker-compose 命令

参考：https://www.cjavapy.com/article/2355/

### 20、docker-compose up 命令

尝试自动完成包括构建镜像，（重新）创建服务，启动服务，并关联服务相关容器的一系列操作

**格式：**

```
docker-compose up [选项] [SERVICE...]
```

**选项：**

1）-d 在后台运行服务容器。

2）--no-color 不使用颜色来区分不同的服务的控制台输出。

3）--no-deps 不启动服务所链接的容器。

4）--force-recreate 强制重新创建容器，不能与 --no-recreate 同时使用。

5）--no-recreate 如果容器已经存在了，则不重新创建，不能与 --force-recreate 同时使用。

6）--no-build 不自动构建缺失的服务镜像。

7）-t, --timeout TIMEOUT 停止容器时候的超时（默认为 10 秒）。

