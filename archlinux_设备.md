# 设备

## 1 蓝牙

[蓝牙网址](https://wiki.archlinuxcn.org/wiki/%E8%93%9D%E7%89%99)

### 1　安装

1. 安装 `bluez`包，这个软件包提供蓝牙协议栈。
2. 安装 `bluez-utils`包，这个软件包提供 `bluetoothctl` 实用程序。
3. `btusb` 内核模块是通用蓝牙驱动。检查模块是否已加载。如果还没有，先加载模块。
4. 启动/启用 `systemctl enabled bluetooth.service`

### 2 操作

#### 1 bluetoothctl

```shell
bluetoothctl # 进入到前端界面中

help # 帮助
list # 列出
power on # 打开控制器电源
agent on # 打开代理
default-agent # 使用默认代理
devices # 获取要配对的设备MAC码
remove MAC码 # 从设备中删除
scan on # 打开扫描
scan off # 关闭扫描
pair MAC码 # 配对
connect MAC码 # 建立连接
trust MAC码 # 将设备添加到信任列表，自动连接
```

> 蓝牙是默认开启的，也就是`power on`这一步其实一般都不太需要
> 蓝牙代理主要用于管理蓝牙"配对码"，一般在把搜索打开前，先打开代理
> 蓝牙耳机的配对和普通蓝牙设备的配对步骤几乎差不多，但依赖的包更多
>

## 3 内核模块

[内核模块WiKi](https://wiki.archlinuxcn.org/wiki/%E5%86%85%E6%A0%B8%E6%A8%A1%E5%9D%97#%E8%8E%B7%E5%8F%96%E4%BF%A1%E6%81%AF)

显示当前装入的内核模块 `lsmod`

显示模块信息 `modinfo module_name`
