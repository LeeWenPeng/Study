## 1. 作用

属于 `sysstat` 软件包

查看CPU、磁盘的相关信息

## 2. 语法

```shell
iostat [-x] [参数1] [参数1]
```

`[options]`

+ `[-x]`：显示更多信息

参数：

+ `[参数1]`：刷新间隔
+ `[参数2]`：刷新次数

>[!note]
> + 不指定两个参数时，默认为没有刷新间隔和刷新次数，只显示调用命令时系统相关信息
> + 指定一个参数时，默认该参数为刷新间隔，而刷新次数为无限次

## 3. 显示信息

+ `rKB/s`：read KB/s
+ `wKB/s`：write KB/s
+ `%util`：磁盘利用率
