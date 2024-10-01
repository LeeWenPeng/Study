# 应用

## 1 pacman

### 1.1 更新系统

```shell
sudo pacman -Syu
```

### 1.2 安装包

```shell
pacman -S 包名
```

### 1.3 查看包

   ```shell
   # 查看包的详细信息
   pacman -Qi 包名

   # 查找已经被安装的包
   pacman -Qs 包名

   # 使用 Pacman 查看本地包数据库
   pacman -Qq 包名

   # pacman 在数据库中搜索包名称及其描述
   pacman -Ss 包名

   # 在远程软件包中查找文件所属的包
   pacman -F 包名

   # 查找一个包的依赖树
   pactree 包名

   # 通过pacman安装日志查看是否安装某一个包
   sudo cat /var/log/pacman.log |grep apache
   ```

### 1.4 删除包

```shell
# 最常用命令 删除指定的软件包
sudo pacman -Rsu 包名

# 删除孤儿包
sudo pacman -R $(sudo pacman -Qdtq)

# 完全删除软件依赖
sudo pacman -Rscun 包名

# 删除当前未安装的所有缓存包和未使用的同步数据库
sudo pacman -Sc

# 删除所有不需要的依赖项
su
pacman -Qdtq | pacman -Rs -
```

## 2 zip

网址

<https://www.runoob.com/linux/linux-comm-zip.html>

### 2.1 压缩

语法

```shell
zip [options] output.zip file1 file2 ...
```

* output.zip 生成压缩包的名称
* file1 file2 ... 要压缩的文件

[options]

* -r：递归压缩目录及其子目录中的所有文件。
* -e：为压缩文件设置密码保护。
* -q：静默模式，不显示压缩过程。
* -v：显示详细的压缩过程。
* -x：排除某些文件或目录，不进行压缩。
* -m：压缩后删除原始文件。
* -0 到 -9：指定压缩级别，-0 表示存储不压缩，-9 表示最高压缩率，默认是 -6。

### 2.2 解压缩

<https://linuxize.com/post/how-to-unzip-files-in-linux/>

语法

```shell
unzip archive.zip
```

## 3 fictx5

1. 在当前输入法和首选输入法之间切换 (中英文切换)

    `ctrl + space`

2. 选择输入法

    `` ctrl + ` ``

## 4 vim

[vim 快捷键](https://zhuanlan.zhihu.com/p/155973403)
