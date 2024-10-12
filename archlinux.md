
# Arch Linux

[TOC]

## 配置

### 1 shell 配置

shell 配置文件为：

```shell
# 系统范围
/etc/profile
/etc/profile.d/*.sh
# 用户
~/.profile
# bash
~/.bash_profile
~/.bashrc
```

> 在登录时，所有兼容 Bourne Shell 的 Shell 都会读取 `/etc/profile`，而 `/etc/profile` 又会读取 `/etc/profile.d/` 中任何可读的 `*.sh` 文件：这些脚本不需要解释器指令，也不需要具有可执行权限。它们用于设置环境并定义特定于应用程序的设置。
>
> `~/.bash_profile` 会读取 `~/.bashrc` 中的配置

参数:

1. `--login`

### 2 网络

可视化

```shell
nmtui
```

### 3 系统

1. 查看系统显卡

   ```shell
   lspci | grep -i nvidia
   ```

2. 音频 alsa

网址: <https://wiki.archlinuxcn.org/wiki/ALSA>

１　安装音频管理工具　`alsa-utils`


### 4 systemd

   systemd 是一个 Linux 系统基础组件的集合，提供了一个系统和服务管理器

#### 4.1 常用命令

1. 显示系统状态

   ```shell
   systemctl status
   ```

2. 列出正在运行的单元

   ```shell
   systemctl 
   <!-- 或 -->
   systemctl list-units
   ```

## 二　环境

### 窗口合成器＝-sway

手册<https://wiki.archlinux.org/title/Sway>

#### 安装

```shell
sudo pacman -S sway swaylock swayidle swaybg
```

#### 配置

配置文件在 `~/.config/sway/config`

### 终端-kitty

官网 <https://sw.kovidgoyal.net/kitty/>

### vim

使用`vim <文件>`

1. `/`

   在normal modal下键入 `/`进入搜索模式

   键入想检索的单词然后回车，光标会跳到第一个匹配的单词

   按下 `n` ，光标会跳到下一个匹配的单词

   按下 `N` ，光标会跳到上一个匹配的单词

默认目录
/srv/http
/srv/http/cgi-bin
### python

#### 构建虚拟环境

##### 1 venv

python3.3+之后带有模块 venv
> 使用venv创建的虚拟环境中，使用的python版本是创建该环境的python版本
>
> 如果想创建使用其他版本的虚拟环境，需要使用python-virtualenv

1 创建

```shell
python -m venv <虚拟环境名>
```

2 激活

```shell
source <虚拟环境名>/bin/activate
```

3 退出

```shell
deactivate
```

##### 2 python-virtualenv

使用这个模块前，需要先安装这个模块

```shell
pacman -S python-virtualenv
```

1 创建虚拟环境

```shell
virtualenv <-p python<2|3>> <虚拟环境名>
# 如果不带`-p python版本号`， 则会默认使用系统自带的python版本
```

2 激活虚拟环境

```shell
source <虚拟环境名>/bin/activate
```

3 退出虚拟环境

```shell
deactivate
```

### apache

arch linux apache 的网址：<https://wiki.archlinux.org/title/Apache_HTTP_Server>

#### 1 安装

```shell
sudo pacman -S apache
```

#### 2 配置

   配置文件放在`/etc/httpd/conf`中

   配置文件为`/etc/httpd/conf/httpd.conf`

   1. 改端口
   修改`Listen 80`为`Listen 127.0.0.1:80`

   2. log地址

   错误日志在

   `/var/log/httpd/error_log`

## 三　应用管理



### makepkg

网址: 
<https://wiki.archlinuxcn.org/wiki/Makepkg>

安装过程如下：

1. 获取软件包的git clone url

需要从AUR库中下载具有文件`PKGBUILD`的文件包，才能使用makepkg软件。所以，首先，进入AUR仓库中找到包的github找到资源，复制资源的`git clone url`。

路径：<https://aur.archlinux.org/>

2. 使用git clone工具下载

   ```shell
   git clone <url>
   ```

3. 打包

    在拥有`PKGBUILD`文件的目录下使用`makepkg`命令

    > 不允许使用root用户运行makepkg本身
    > 如果前两步使用root用户，则`makepkg`会报**没有写入权限**的错误

    ```shell
    mkpkg -si
    # -s / --syncdeps 构建包并安装所需的依赖项
    # -r / --rmdeps makepkg稍后会删除不再需要的依赖项
    # -i / --install 满足所有依赖项并且成功构建包后，在工作目录中创建一个包文件(pkgname-pkgver.pkg.tar.zst)，使用 -i 安装
    # -c / --clean 清理剩余的文件和目录，对于包升级有用处
    ```

#### 安装问题

问题一：当使用`makepkg -si`时，报错如下：

```shell
    gmp-6.3.0.tar.xz ... FAILED (unknown public key F3599FF828C67298)
    mpfr-4.2.1.tar.xz ... FAILED (unknown public key 5831D11A0D4DB02A)
==> ERROR: One or more PGP signatures could not be verified!
```

解决方法：将公钥直接加入进去

```shell
   gpg --recv-key F3599FF828C67298
   gpg --recv-key 5831D11A0D4DB02A
```

### clash

配置文件

```shell
~/.config/clash/clash.yaml
```

更新订阅

```shell
curl -o /home/<用户名>/.config/clash/config.yaml <URL>
```

启动

```shell
clash
```

### scrot

github: <https://github.com/dreamer/scrot>

使用手册: <https://www.howtoforge.com/tutorial/how-to-take-screenshots-in-linux-with-scrot/>

安装：`sudo pacman -S scrot`

> 这个工具只适用于x11，而不适用于wayland和xwayland

### v2ray

网址: <https://wiki.archlinuxcn.org/wiki/V2Ray?rdfrom=https%3A%2F%2Fwiki.archlinux.org%2Findex.php%3Ftitle%3DV2Ray_%28%25E7%25AE%2580%25E4%25BD%2593%25E4%25B8%25AD%25E6%2596%2587%29%26redirect%3Dno>

### 字体

1 note font

2 nerd font

### Clash Verge Rev

[安装网址](https://www.clashverge.dev/install.html)

安装步骤：

1. 安装 paru
   1. 这步操作需要先设置Arch Linux CN软件仓库镜像，因为`paru`在非官方库中
   2. 安装代码：`sudo pacman -S paru`
2. 安装 clash-verge-rev-bin
   1. `paru -S clash-verge-rev-bin`
