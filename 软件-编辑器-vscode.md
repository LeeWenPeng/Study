## 1. 介绍

[vscode archlinux 帮助手册](https://wiki.archlinuxcn.org/wiki/Visual_Studio_Code)

## 2. 下载安装

[vscode AUR 仓库位置](https://aur.archlinux.org/packages/visual-studio-code-bin)

```shell
# archlinux
# 1 下载
git clone https://aur.archlinux.org/visual-studio-code-bin.git
# 2 进入文件夹
cd visual-studio-code-bin/
# 3 安装
makepkg -si
```

## 3. 配置C++

### 3.1. 预安装

1. vscode软件
2. C/C++ 扩展
3. GCC 编译器[[编程语言-C++#下载安装]]
4. GDB debug
5. clang 代码补全

### 3.2. 配置文件

`.vscode`文件夹：

+ tasks.json (compiler build settings) ，负责编译
+ launch.json (debugger settings)，负责调试
+ c_cpp_properties.json (compiler path and IntelliSense settings)，负责更改路径等设置

#### 3.2.1. tasks.json

负责告诉vscode如何**编译**程序，将调用 g++编译器从源代码创建一个可执行文件。

1. 在上方的主菜单中，**终端(Terminal)** -> **配置默认生成任务(Configure Default Build Task)**
2. 在下拉菜单中选择选择 **C/C++: g++ 生成活动文件(C/C++: g++ build active file)**

```json
{
	"version": "2.0.0",
	"tasks": [
		{
			"type": "cppbuild",
			"label": "C/C++: g++ 生成活动文件",
			"command": "/usr/bin/g++",
			"args": [
				"-fdiagnostics-color=always",
				"-g",
				"${file}",
				"-o",
				"${fileDirname}/${fileBasenameNoExtension}"
			],
			"options": {
				"cwd": "${fileDirname}"
			},
			"problemMatcher": [
				"$gcc"
			],
			"group": {
				"kind": "build",
				"isDefault": true
			},
			"detail": "编译器: /usr/bin/g++"
		}
	]
}
```

+ `command`：程序路径
+ `args`：传给g++的命令行参数
+ `label`：标签值是将在任务列表中看到的内容；可以随意命名它。
+ `group`：
	+ `isDefault`：
		+ `true`：表示支持通过快捷键 `ctrl+shift+B` 来执行该编译任务。
		+ `false`：从菜单中选择运行：终端(Terminal)->运行生成任务(Run Build Task)。

#### 3.2.2. launch.json

 1. **运行(Run)**-> **添加配置(Add Configuration…)**
 2. 在生成的页面中点选右下角按键**添加配置…**

```json
{
    // 使用 IntelliSense 了解相关属性。 
    // 悬停以查看现有属性的描述。
    // 欲了解更多信息，请访问: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        
        {
            "name": "(gdb) 启动",
            "type": "cppdbg",
            "request": "launch",
            "program": "${fileDirname}/${fileBasenameNoExtension}",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${fileDirname}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "setupCommands": [
                {
                    "description": "为 gdb 启用整齐打印",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                },
                {
                    "description": "将反汇编风格设置为 Intel",
                    "text": "-gdb-set disassembly-flavor intel",
                    "ignoreFailures": true
                }
            ],
            "preLaunchTask":"C/C++: g++ 生成活动文件",
            "miDebuggerPath": "/usr/bin/gdb"
        }

    ]
}
```

+ `program`：指调试程序的位置，对应`tasks.json`中`args`对应value的最后一项
+ `stopAtEntry`：
	+ `false`：默认值，C++拓展不会向源代码添加任何断点。
	+ `true`，将使调试器在开始调试时停止在 main 方法上。

#### 3.2.3. c_cpp_properties.json

1. `Ctrl+Shift+P`，启动命令模版
2. 在下拉菜单中选择，C/C++: 编辑配置(JSON)，生成`c_cpp_properties.json`文件
