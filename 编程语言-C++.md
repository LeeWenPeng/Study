## 1  下载安装

1. gcc
2. glibc
3. gdb
4. clang
5. make
6. cmake
7. vscode
	1. C/C++
	2. CMake
	3. CMake Tools

## 2  gcc

```shell
### arch Linux
sudo pacman -S gcc 

# 确保安装
gcc -v
# or
pacman -Qi gcc


```

### 2.1  编译

```shell
# 编译
g++ -o filename filename.cpp
```

+ `-o`：指定输出文件为`filename`
