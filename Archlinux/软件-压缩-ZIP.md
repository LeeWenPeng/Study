## 1. 常用命令

网址

<https://www.runoob.com/linux/linux-comm-zip.html>

### 1.1. 压缩

语法

```shell
zip [options] output.zip file1 file2 ...
```

* output.zip 生成压缩包的名称
* file1 file2 … 要压缩的文件

[options]

* -r：递归压缩目录及其子目录中的所有文件。
	* 也就是说，被压缩内容具有文件夹时需要`-r`
* -e：为压缩文件设置密码保护。
* -q：静默模式，不显示压缩过程。
* -v：显示详细的压缩过程。
* -x：排除某些文件或目录，不进行压缩。
* -m：压缩后删除原始文件。
* -0 到 -9：指定压缩级别，-0 表示存储不压缩，-9 表示最高压缩率，默认是 -6。

### 1.2. 解压缩

[解压缩菜鸟教程](https://www.runoob.com/linux/linux-comm-unzip.html)

语法

```shell
unzip [-d] archive.zip
```

`[-d]`：指定解压目录，同`tar -C`

> [!danger]
> 如果解压时，有同名的文件\文件夹，会直接将同名文件\目录覆盖掉
