## 1  XShell

### 1.1  下载

[下载网址](https://www.xshell.com/zh/free-for-home-school/)

### 1.2  新建链接

服务器端

1.   安装 ssh 服务端：`sudo apt install openssh-server`
2.   安装网络包：`sudo apt install net-tools`
3.   查看服务器 ip：`ifconfig`

主机端

1.   新建连接：打开XShell -> 新建连接(Alt + N) 
2.   输入信息："主机"选项中输入获取的服务器 ip，其余默认

### 1.3  设置

#### 1.3.1  透明度

工具 -> 选项 -> 查看 -> "使窗口透明"

#### 1.3.2  字体大小调节

`ctrl + 鼠标滚轮`

### 1.4  公钥认证——使远程连接不需要输密码

1.   主机生成公钥密钥：`ssh-keygen -t rsa`
2.   复制主机公钥 ：`C:\Users\用户名\.ssh\id_rsa.pub`
3.   服务器端生成公钥密钥：`ssh-keygen -t rsa`
4.   进入公钥密钥文件夹：`cd ~/.ssh`
5.   创建 认证 文件，将主机公钥粘贴到该文件中：`vim authorized_keys`

## 2  Xftp

登录步骤

1.   新建连接
2.   配置名称：见名知意
3.   配置主机：远程主机IP
4.   配置用户信息：远程主机的用户名和密码