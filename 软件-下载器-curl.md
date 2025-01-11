## 1. 介绍

cURL 是一个命令行工具和库，用于使用 URL 传输数据。该命令支持多种不同的协议，包括 HTTP、HTTPS、FTP、SCP 和 SFTP。

## 2. 下载

```shell
sudo pacman -S curl
```

## 3. 3使用

```shell
# 下载
curl [-O --output] 文件名 URL
# 当URL中含有文件名时，可以直接保存
curl --remote-name URL
# 不指定参数时，将获得的资源打印在stdout
curl URL
```

特殊使用：获取ip地址

```shell
curl cip.cc
```

> `cip.cc`为在线ip查询工具

