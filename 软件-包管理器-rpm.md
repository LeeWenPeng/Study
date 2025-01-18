包：`rpm-tools`

安装命令

```shell
rpm -ivh --nodeps 包名.rpm
```

+ `-i`：安装
+ `-v`：显示安装信息
+ `-h`：显示安装进度
+ `--nodeps` ： 忽略依赖

卸载

```shell
rpm -e --nodeps 包名.rpm
```