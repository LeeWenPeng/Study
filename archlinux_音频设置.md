# 音频设置

## 1. 驱动 AlSA

[AlSA ArchLinux Wiki 网址](https://wiki.archlinuxcn.org/wiki/ALSA#)

### 1.1. 包

`alsa-utils`

包含`amixer`、`alsamixer`等程序

### 1.2. 服务

`alsa-utils`　软件包默认包含了 `systemd` 单元配置文件:

+ `alsa-restore.service`
+ `alsa-state.service`

二选一，由`systemctl`控制

## 2. 音频服务器 pipewire

### 2.1. 配置

pipewire 相关配置文件主要有三个：

1. 初始配置文件: `/usr/share/pipewire`
2. 系统配置文件: `etc/pipewire`
3. 用户配置文件: `~/.config/pipewire`

其中，`/usr/share/pipewire`中的初始配置文件在`pipewire`安装的时候自动生成，该文件在软件更新时会自动修改，作为初始软件，不应修改；

`etc/pipewire`和`~/.config/pipewire`两个目录为用户自行创建，应该将初始配置文件复制于此，然后对pipewire进行配置

## 3. ３　蓝牙音频

[网址](https://wiki.archlinuxcn.org/wiki/%E8%93%9D%E7%89%99%E8%80%B3%E6%9C%BA#%E9%80%9A%E8%BF%87_Pipewire_%E8%BF%9E%E6%8E%A5%E8%80%B3%E6%9C%BA)

1 通过 Pipewire 连接耳机

`pipewire-pulse`：基础包

<!-- `pavucontrol`:用户服务 -->
