## 1  pacman

pacman 使用手册 <https://wiki.archlinuxcn.org/wiki/Pacman>

### 1.1  语法

```shell
pacman <operation> [...]
```

operation:

### 1.2  pacman信息

```shell
# 帮助
pacman {-h --help}
```

```shell
# 版本
pacman {-V --version}
```

```shell
pacman {-D --database} <options> <package(s)>
```

### 1.3  查询包

```shell
# 查询文件数据库
pacman {-F --files}    [options] [file(s)]
```

```shell
# 查询本地包数据库
pacman {-Q --query}    [options] [package(s)]
```

### 1.4  删除包

```shell
# 删除包，对应 Windows 中的卸载操作
pacman {-R --remove}   [options] <package(s)>
```

`[options]`:

1. `-s`: 删除指定软件包，以及没有被其他包依赖的依赖项。

   > + 删除软件组时，会忽略软件组内软件的安装原因。
   >
   > + 也就是说，删除软件组时，会将软件组内的软件全部删除，即使那个软件的安装早于该软件组的安装。
   >
   > + 但不会忽略依赖的软件的安装原因。

2. `-u`: 删除其他包不需要的依赖。
3. `-c`: 级联操作，删除软件包以及所有依赖该软件包的。
4. `-n`: 避免在删除时备份配置文件。

> pacman 不会删除软件自己创建的文件，包括且不限于主目录中的`.`开头的文件

### 1.5  安装包

#### 1.5.1  (1) 作用

`-S --sync`: synchronization 同步, 意`pacman`在安装软件之前先与软件库同步

`pacman`数据库根据安装原因将安装的包分为两组：

1. 显式安装的包: 由`pacman -S`或`-U`直接安装的包
2. 依赖安装: 安装某个包时，其所依赖的包将被自动安装

#### 1.5.2  (2) 语法

```shell
# 安装包
pacman {-S --sync}　[options] [package(s)]
```

#### 1.5.3  (3) 参数

1. 可以同时安装多个包

	```shell
    sudo pacman -S 包名_1 包名_2 ...
    ```

2. 可以使用正则表达式, 如:

	```shell
    sudo pacman -S $(pacman -Ssq 包正则表达式)
    ```

3. 指定安装路径

	```shell
    sudo pacman -S 父路径/包名
    ```

4. 可使用`{}`扩展安装重复名称软件, 可嵌套使用(如下文的不同部分3)

	```shell
    sudo pacman -S 名称相同部分{不同部分1,不同部分2,不同部分3{不同部分31,不同部分32}}
    ```

```shell
pacman {-T --deptest}  [options] [package(s)]
```

```shell
# 升级包
pacman {-U --upgrade}  [options] <file(s)>
```

### 1.6  安装时报的错

#### 1.6.1  问题一

packate.tar.zst is corrupted (invalid or corrupted package (PGP signature)).

[解决方案](https://n.ethz.ch/~dbernhard/archlinux-package-is-corrupted-invalid-or-corrupted-package.html#:~:text=It%27s%20probably%20because%20your%20keyring%20is%20corrupted.%20A,is%20corrupted%20%28invalid%20or%20corrupted%20package%20%28PGP%20signature%29%29.)

结果：真TMD好使

#### 1.6.2  问题二

"Failed to commit transaction (invalid or corrupted package)" 错误

网址：[解决方案](https://wiki.archlinuxcn.org/wiki/Pacman#%22Failed_to_commit_transaction_(invalid_or_corrupted_package)%22_%E9%94%99%E8%AF%AF)

结果：没有帮助，于是去搜了更细的问题，详情见上一个问题

#### 1.6.3  问题三

error: failed to synchronize all databases (unable to lock database)

网址: [解决方案](https://wiki.archlinux.org/title/Pacman#.22Failed_to_init_transaction_.28unable_to_lock_database.29.22_error)

结果：好用

#### 1.6.4  问题四

curl: (7) Failed to connect to raw.githubusercontent.com port 443 after 1 ms: Could not connect to server

==> ERROR: Failure while downloading https://raw.githubusercontent.com/microsoft/vscode/1.94.2/resources/linux/code.desktop Aborting…

解决方案：修改hosts文件

具体步骤：

```shell
# 1 打开hosts文件
sudo vim /etc/hosts
# 2 hosts文件中添加
185.199.108.133 raw.githubusercontent.com
```

结果：真TMD好使！

问题五

对于某些通过AUR安装的软件无法跟随系统更新而更新

解决方法：重新去AUR仓库找到对应软件，重新下载并安装

结果：好使

### 1.7  设置 Arch Linux CN 软件仓库镜像

相关网址：

+ [arch 相关帮助手册](https://wiki.archlinuxcn.org/wiki/%E9%9D%9E%E5%AE%98%E6%96%B9%E7%94%A8%E6%88%B7%E4%BB%93%E5%BA%93#Arch_Linux_%E4%B8%AD%E6%96%87%E7%A4%BE%E5%8C%BA%E4%BB%93%E5%BA%93)
+ [完整仓库网址](https://github.com/archlinuxcn/repo)
+ [镜像网站列表](https://github.com/archlinuxcn/mirrorlist-repo)

步骤:

1. 配置`pacman`配置文件

```shell
su
vi /etc/pacman.conf
```

将下述文本粘贴到 `pacman.conf` 中

```txt
[archlinuxcn]
#上海交大
Server = https://mirrors.sjtug.sjtu.edu.cn/archlinux-cn/$arch
# 163源
Server = http://mirrors.163.com/archlinux-cn/$arch
# 清华大学
Server = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/$arch
#USTC 中科大
Server = https://mirrors.ustc.edu.cn/archlinuxcn/$arch
#浙江大学
Server = https://mirrors.zju.edu.cn/archlinuxcn/$arch
#西安交通大学
Server = https://mirrors.xjtu.edu.cn/archlinuxcn/$arch
#北京外国语大学
Server = https://mirrors.bfsu.edu.cn/archlinuxcn/$arch
#哈尔滨工业大学
Server = https://mirrors.hit.edu.cn/archlinuxcn/$arch
#南京大学
Server = https://mirrors.nju.edu.cn/archlinuxcn/$arch
#中科院开源软件协会
Server = https://mirrors.opencas.cn/archlinuxcn/$arch
#重庆大学
Server = https://mirrors.cqu.edu.cn/archlinuxcn/$arch
```

2. 安装 Arch Linux CN 的密钥

```shell
sudo pacman -Sy && sudo pacman -S archlinuxcn-keyring
```

3. 更新软件缓存

	```shell

sudo pacman -Syyu

	```

> [!bug] 系统更新报错
> 如果更新系统时报错，需要重新安装一下Arch Linux CN的密钥。

### 1.8  常用命令

#### 1.8.1  更新系统

```shell
sudo pacman -Syu
```

#### 1.8.2  安装包

```shell
# 安装包
pacman -S 包名
# 更新包名
pacman -U 包名
```

#### 1.8.3  查看包

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

	# 查看包的安装命令
	pacman -Ql 包名

	# 查看包的配置文件
	pacman -Ql 包名 | grep /etc

	# 查文件所属的包
	pacman -Qo /path/to/file
   ```

#### 1.8.4  删除包

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
