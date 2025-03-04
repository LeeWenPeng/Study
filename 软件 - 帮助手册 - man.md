语法

```bash
man [选项] <命令/函数/文件名>
```

手册章节划分

+ `1`：用户命令（如 `ls`, `cp`）
+ `2`：系统调用（如 `open`, `fork`）
+ `3`：C库函数（如 `printf`, `malloc`）
+ `4`：设备文件与特殊文件（如 `/dev/null`）
+ `5`：配置文件格式（如 `/etc/passwd` 的格式）
+ `6`：游戏和屏保
+ `7`：杂项（如协议、文件系统描述）
+ `8`：系统管理命令（如 `ifconfig`, `mount`，通常需要 root 权限）
+ `9`：内核相关（如内核参数或驱动）

常用选项

+ `-k <关键词>`：搜索手册页描述中的关键词（等价于 `apropos` 命令）
+ `-K <关键词>`：**全局搜索**手册页内容（耗时较长，需谨慎使用）
+ `-f <命令>`：显示命令的简短描述（等价于 `whatis` 命令）
+ `-a <命令>`：显示所有章节中匹配的手册页（例如 `man -a printf`）
+ `-w <命令>`：显示手册页的物理路径（如 `man -w ls`）

>[!question] No manual entry for open in section 2No manual entry for open in section 2
>+ 未安装系统调用手册页，安装 `manpages-dev` 或 `man-pages`
>+ 手册页数据库未更新，运行 `sudo mandb`
>+ 非英语环境导致手册页缺失，临时切换为英文手册页`export LANG=en_US.UTF-8`

中文手册下载

```bash
sudo pacman -Syu
sudo pacman -S man-pages-zh_cn
```

临时切换中文语言

```bash
# 1
LANG=zh_CN.UTF-8 man <命令>

# 2q
# 设置优先使用中文手册（若存在）
export LANG=zh_CN.UTF-8
# 若中文手册不存在，则回退到英文
export MANLANG="zh_CN:en"
```

临时切换英语

```bash
LANG=en_US.UTF-8 man <命令>

export LANG=en_US.UTF-8
```
