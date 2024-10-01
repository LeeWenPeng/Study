# pacman

pacman 使用手册 <https://wiki.archlinuxcn.org/wiki/Pacman>

## 语法

```shell
pacman <operation> [...]
```

operation:

## pacman信息

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

## 查询包

```shell
# 查询文件数据库
pacman {-F --files}    [options] [file(s)]
```

```shell
# 查询本地包数据库
pacman {-Q --query}    [options] [package(s)]
```

## 删除包

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

## 安装包

### (1) 作用

`-S --sync`: synchronization 同步, 意`pacman`在安装软件之前先与软件库同步

`pacman`数据库根据安装原因将安装的包分为两组：

1. 显式安装的包: 由`pacman -S`或`-U`直接安装的包
2. 依赖安装: 安装某个包时，其所依赖的包将被自动安装

### (2) 语法

```shell
# 安装包
pacman {-S --sync}　[options] [package(s)]
```

### (3) 参数

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

## 报错

### 安装时报的错

问题：packate.tar.zst is corrupted (invalid or corrupted package (PGP signature)).
网址<https://n.ethz.ch/~dbernhard/archlinux-package-is-corrupted-invalid-or-corrupted-package.html#:~:text=It%27s%20probably%20because%20your%20keyring%20is%20corrupted.%20A,is%20corrupted%20%28invalid%20or%20corrupted%20package%20%28PGP%20signature%29%29.>
结果：真TMD好使

问题："Failed to commit transaction (invalid or corrupted package)" 错误
网址：<https://wiki.archlinuxcn.org/wiki/Pacman#%22Failed_to_commit_transaction_(invalid_or_corrupted_package)%22_%E9%94%99%E8%AF%AF>
结果：没有帮助，于是去搜了更细的问题，详情见上一个问题