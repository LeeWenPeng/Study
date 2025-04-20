## 1 服务-systemd

网址: <https://wiki.archlinuxcn.org/wiki/Systemd>

１.1 分析系统状态

1. 显示系统状态　`systemctl status`
2. 列出正在运行的单元`systemctl` 或 `systemctl list-units`

1.2 启动、重新启动和重新加载单元

1. 启动单元 `systemctl start example.service`
2. 列出正在运行的单元
3. 列出可用服务

	```VHDL
    systemctl list-units --type=service 
    
    systemctl list-units -a --type=service
    ```



## 3 网络服务

## 3-1 网络接口

文件夹`/sys/class/net`

```shell
# 通过文件查看网络接口
ls /sys/class/net
# 使用命令查看网络接口
ip link

# 查看接口状态
ip link show dev 接口名
# 启用和禁用网络接口
ip link set interface up|down
```

> [!note]
> 接口信息中显示的接口lo 是 Loop 设备，不用于建立网络连接。

### 3-2 静态 ip

#### ip地址 `ip address`

```shell
# 查看ip地址
ip address show
# 添加
ip address add address/prefix_len broadcast + dev interface
# 单个删除
ip address del address/prefix_len dev interface
# 批量删除
ip address flush dev interface
```

#### 路由 `ip route`

```shell
# 列出ipv4路由
ip route show
# 列出ipv6路由
ip -6 show
# 添加路由
ip route add PREFIX via address dev interface
 # 删除路由
ip route add PREFIX via address dev interface
```

## 4 主机名

电脑对外名称

在Linux终端中，一般左侧方括号内内容为：

```shell
[用户名@主机名 路径]
```

主机名文件`/etc/hostname`

查看主机名

```shell
hostnamectl
```

修改主机名

```shell
# 手动修改`/etc/hostname`文件中的hostname值
sudo vim /etc/hostname
# 命令
sudo hostnamectl set-hostname 主机名
```

## 5 端口号

[ss命令帮助菜单](https://man.archlinux.org/man/ss.8)

在archlinux 中`net-tool`包已经被弃用，故包中的`netstat`命令被`ss`命令取代了

常用命令：

```shell
# 查看所有TCP
ss -at
# 查看所有tcp连接及其端口号
ss -atn
# 查看所有UCP
ss -au
```

+ `-a` all
+ `-t` TCP
+ `-u` UCP
+ `-n` port number
