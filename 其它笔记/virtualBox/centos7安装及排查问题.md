文件:

下载centos：http://isoredirect.centos.org/centos/7/isos/x86_64/
下载vb:https://www.virtualbox.org/wiki/Downloads

1. 安装VB增强插件，正常在导航设备那里“安装增强插件”

2. 如果报异常，则手动安装 

   ```bash
   sudo mkdir --p /media/cdrom
   sudo mount -t auto /dev/cdrom /media/cdrom/
   cd /media/cdrom/
   sudo sh VBoxLinuxAdditions.run
   ```

   

3. 按提示安装相关程序

   ![img](https://img-blog.csdnimg.cn/20200409041959903.png)

4. 如果网络不通，参考地址：https://segmentfault.com/a/1190000023086220

