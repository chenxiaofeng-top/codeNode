## 位置

- 默认:${user.home}/conf/settings.xml
- idea：在idea的settings中搜索
- ${maven.conf}/settings.xml

## 本地仓库位置

```xml
<localRepository>/path/to/local/repo</localRepository>
```

## 是否离线

```xml
<offline>false</offline>
```

## 配置代理服务器

```xml
<proxies>
    <proxy>
      <id>proxy-server-1</id>
      <active>true</active>
      <protocol>http</protocol>
      <username>proxyuser</username>
      <password>proxypass</password>
      <host>proxy.host.net</host>
      <port>80</port>
      <nonProxyHosts>local.net|some.host.com</nonProxyHosts>
    </proxy>
 </proxies>
```

## 配置Nexus私服账号密码

```xml
<distributionManagement>
    <repository>
        <id>cat-release</id>
        <name>RELEASES</name>
        <url>http://172.10.0.100:8081/repository/cat-releases/</url>
    </repository>

    <snapshotRepository>
        <id>cat-snapshot</id>
        <name>SNAPSHOT</name>
        <url>http://172.10.0.100:8081/repository/cat-snapshot/</url>
    </snapshotRepository>
</distributionManagement>
```

```xml
<servers>
    <server>
        <id>cat-release</id>
        <username>laomao</username>
        <password>123456</password>
    </server>
    <server>
        <id>cat-snapshot</id>
        <username>laomao</username>
        <password>123456</password>
    </server>
</servers>
```

## 镜像

```xml
<mirrors>
    <mirror>
        <id>ali</id>
        <name>aliyun maven</name>
        <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
        <mirrorOf>central</mirrorOf>
    </mirror>
</mirrors>
```