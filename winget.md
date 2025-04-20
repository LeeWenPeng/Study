## install 命令

### 常用

```bash

```

### 详情

[winget](https://learn.microsoft.com/zh-cn/windows/package-manager/winget/) 工具的 install 命令可安装指定的应用程序。 使用 [search](https://learn.microsoft.com/zh-cn/windows/package-manager/winget/search) 命令找到要安装的应用程序。

install 命令要求你指定要安装内容的具体字符串。 如果存在任何不明确性，系统会提示你进一步将 install 命令筛选到具体应用程序。

```bash
winget install [[-q] <query> ...] [<options>]
```

别名

+   `add`

参数

+   `-q --query`：用于搜索位置查询

选项

+   `--id`：将安装限制为应用程序的 ID。
+   `--name`：将搜索限制为应用程序的名称。
+   `-i` ：交互形式运行安装程序
+   `-l --location`：设置要安装的位置（如果支持）
+   `--rainbow`：彩虹色进度条

## list 命令

### 常用

```bash

```

### 详情

[winget](https://learn.microsoft.com/zh-cn/windows/package-manager/winget/) 工具的 list 命令可显示计算机上当前安装的应用程序的列表。

```bash
winget list [[-q] <query>] [<options>]
```

别名

+   `list`的别名 `ls`

参数

+   `-q --query`：用于搜索位置查询

选项

+   `--id <id>`： 将列出限制为应用程序的 ID。

+   `--name <name>`：将列出限制为应用程序的名称。

+   `--cmd、--command`：按应用程序指定的命令筛选结果。

## settings 命令

### 详情

通过使用 [winget](https://learn.microsoft.com/zh-cn/windows/package-manager/winget/) 工具的 settings 命令，可以自定义 Windows 程序包管理器客户端体验。 settings 命令将启动默认文本编辑器。 

```bash
winget settings
```

别名

+   `config`

## show 命令

### 常用

```bash

```

### 详情



```bash'
winget show [[-q] <query>] [<options>]
```

别名

+   `view`

参数

+   `-q --query`：用于搜索位置查询

选项

+   `-m、--manifest`：要显示的应用程序的清单路径