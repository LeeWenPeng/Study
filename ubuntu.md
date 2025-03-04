## Ubuntu

### 镜像下载

[桌面操作系统下载网址](https://ubuntu.com/download/desktop#system-requirements-OracularOriole)

### APT

#### 更换 apt-get 数据源

1.  输入：`sudo -s` 切换为root超级管理员；
2.  执行命令：`vim /etc/apt/sources.list`；
3.  清空：使用命令`:%d` 清空所有内容；
4.  清华数据源地址：[https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/](https://mirrors.tuna.tsinghua.edu.cn/help/ubuntu/?spm=a2c6h.12873639.article-detail.4.4d0a3d660FJGxd) **选择相应的版本**复制内容，粘贴到 sources.list 文件中；
5.  更新源：`sudo apt-get update`
6.  更新软件：`sudo apt-get upgrade`

#### 常用命令

```shell
# 更新源
sudo apt-get update
# 更新软件
sudo apt-get upgrade
# 下载软件
sudo apt install 包名
# 查询软件
apt-get search 包名
```

