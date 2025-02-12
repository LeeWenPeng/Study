## VMware Workstation Pro

### 下载

新版的VMware Workstation Pro 对于个人与学生用户已经免费，可以直接去官网下载

[下载网址](https://support.broadcom.com/group/ecx/productdownloads?subfamily=VMware%20Workstation%20Pro)

### VMware Tools 

一般 VMware Tools 都会自动安装

#### 手动安装

如果需要手动安装的话，新版的VMware 不再提供 VMware Tools 镜像，需要自行下载安装。

+   [VMware Tools 下载地址](https://packages-prod.broadcom.com/tools/frozen/linux/linux.iso)
+   [安装手册](https://knowledge.broadcom.com/external/article?legacyId=1014294)
+   [视频教程](https://www.bilibili.com/video/BV1F6DzY2Ep9/?spm_id_from=333.337.search-card.all.click&vd_source=d9e178b992882410dc0927d40741958a)

安装步骤：

1.   下载 VMware Tools 镜像文件：[VMware Tools 下载地址](https://packages-prod.broadcom.com/tools/frozen/linux/linux.iso)
2.   打开设置菜单：虚拟机右键菜单 -> 选择设置
3.   加载镜像文件：添加 -> CD/DVD -> 勾选"使用 ISO 映像文件"，并输入第一步下载好的镜像文件
4.   打开终端：`Ctrl + Alt + T`
5.   找到压缩文件：`cd /media/用户名/VMware Tools`
6.   复制压缩文件：`cp ./VMwareTools-*.tar.gz ~`
7.   进入文件夹：`cd 目录`
8.   安装VMware Tools：`sudo ./vmware-install.pl`

### 虚拟机连接主机VPN方法 

[教程网址](https://blog.xzr.moe/archives/124/)

1.   设置虚拟网络：编辑 -> 虚拟网络编辑器

     1.   设置 NAT，并勾选"主机虚拟机适配器连接到此网络"选项
     2.   可省略，往往是默认配置

2.   设置系统网络适配器：镜像右击 -> 设置 -> 网络适配器 -> 自定义 -> VMnet8

3.   主机网址：任务管理器 -> 性能 -> 以太网 -> IPv4 地址

4.   设置系统代理：

     1.   终端

     ```shell
     export http_proxy=IPv4地址:端口号
     export https_proxy=IPv4地址:端口号
     ```

     2.   设置 -> 网络 -> 网络代理 -> 输入IP地址和端口号

5.   代理软件设置允许局域网连接
     1.   clash：开启 Allon LAN
     2.   v2rayN：基础设置 -> 参数设置 -> 勾选"允许来自局域网的连接" 选项
