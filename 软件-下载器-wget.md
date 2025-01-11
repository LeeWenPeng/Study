[wget wiki](https://wiki.archlinuxcn.org/wiki/Wget)

## 1. 介绍

[GNU Wget](https://www.gnu.org/software/wget/) 是一款自由软件，用于使用HTTP、HTTPS、[FTP](https://wiki.archlinuxcn.org/wiki/FTP "FTP")和 FTPS（FTPS 的支持自 1.18 版起）来检索文件。它是一个非交互式命令行工具，可以从脚本中调用它。

## 2. 下载

包(二选其一)：

+ [wget2](https://aur.archlinux.org/packages/wget2)(依赖于pandoc)
+ [wget2-no-docs](https://aur.archlinux.org/packages/wget2-no-docs)(避免依赖)

## 3. 配置

配置文件`/etc/wgetrc`

### 3.1. FTP

Wget 使用标准代理环境变量

```shell
# 代理验证功能
wget ftp://root:somepassword@10.13.X.Y//ifs/home/test/big/"*.tar"
```

### 3.2. 代理

```shell
wget --proxy-user "DOMAIN\USER" --proxy-password "PASSWORD" URL
```

### 3.3. pacman 集成

```cpp

XferCommand = /usr/bin/wget --proxy-user "domain\user" --proxy-password="password" --passive-ftp --quiet --show-progress --continue --output-document=%o %u

```

## 4. 使用

下载文件

```shell
wget [-b] URL
```

`[options]`：

+ `[-b]`：后台下载
