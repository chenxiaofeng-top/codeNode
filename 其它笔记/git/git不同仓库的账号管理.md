# git不同仓库的账号管理20211027

## 一，问题：

1，公司用https://gitee.com/，而个人用https://github.com/，需要分开管理，不然至少会有一个认证失败。



## 二，说明

1. 只能用ssh，无法用https。

## 三，步骤

1. 生成两对私钥公钥，每个仓库分配一个公钥
2. 在.ssh目录下创建config文件，配置每个仓库与私钥的关系
3. 在Git Bash客户端执行测试命令,会自动生成known_hosts

## 四，详细

### 	1，生成两对私钥公钥，每个仓库分配一个公钥

```sh
ssh-keygen -t rsa -C "邮件地址"
```

![image-20211027175416578](img/image-20211027175416578.png)

完成后把公钥分配到对应的git服务商，window位置C:\Users\\{用户名}\\.ssh

### 2，在.ssh目录下创建config文件，配置每个仓库与私钥的关系

```properties
Host github.com                 
    HostName github.com 域名地址 “git@e.coding.net:platformcs”中的e.coding.net
    IdentityFile id_rsa的地址,可以写多个通过","分开会依次尝试
    PreferredAuthentications publickey 配置登录时的权限认证 (取值publickey,password publickey,keyboard-interactive等，PreferredAuthentications 强制使用Public Key验证)
    User 用户名 域名地址 “git@e.coding.net:platformcs”中的git

修复： 
对于这种仓库:
git@github.com:chenxiaofeng-top/codeNode.git 为以下配置

Host private               
HostName github.com
IdentityFile C:\oneDrive\Nssh\private\id_rsa_private
PreferredAuthentications publickey
User git(一般来说，就是git,)
```

!![image-20220303151018064](img/image-20220303151018064-16462914202942.png)

### 3，在Git Bash客户端执行测试命令,会自动生成known_hosts

```sh
 ssh -T git@gitee.com (Host的值)
 ssh -T private
```

![image-20211027180603894](img/image-20211027180603894.png)