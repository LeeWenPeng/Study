## 3 配置 c++ 语言环境

### 1 安装相关插件

+ c/c++ 官方插件
+ cmake tool 插件
+ CMake Language Support
  + 替换掉下载的 CMake 插件
+ clangd 插件

### 2 下载相关软件

+ LLVM
  + 下载网址：<https://github.com/llvm/llvm-project/releases/tag/llvmorg-16.0.0>
  + windows 系统选择 LLVM-win64.exe
  + 作用：提供 clang kits，非必须

+ mingw64
  + 下载网址：<https://sourceforge.net/projects/mingw-w64/files/mingw-w64/mingw-w64-release/>
  + 可以使用 MSYS2 下载
  + 作用：提供系统包以及 gcc kits

+ virtual studio
  + 官网：<https://visualstudio.microsoft.com/zh-hans/>
  + 作用：提供系统包

> 以上两个软件记得配环境变量，如果是使用应用程序安装而不是解压安装，记得勾选自动配环境变量选项
> mingw64 和 virtual studio 二者可选其一

### 3 配置

配置文件都在 .vscode 文件夹下

1. c_cpp_properties.json

    ```json
    {
    "configurations": [
        {
            "name": "Win32",
            "includePath": [
                "${workspaceFolder}/**"
            ],
            "defines": [
                "_DEBUG",
                "UNICODE",
                "_UNICODE"
            ],
            "compilerPath": "${default}",
            "cStandard": "c11",
            "cppStandard": "c++17",
            "intelliSenseMode": "${default}"
        }
    ],
    "version": 4
    }
    ```

2. launch.json

    ```json
    {
    "version": "0.2.0",
    "configurations": [
        {
            "name": "(gdb) 启动",
            "type": "cppdbg",
            "request": "launch",
            "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${fileDirname}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "miDebuggerPath": "gdb",
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
            "preLaunchTask": "g++ build"
        }
    ]
    }
    ```

3. tasks.json

   ```json
   {
    "tasks": [
        {
            "type": "shell",
            "label": "g++ build",
            "command": "g++",
            "args": [
                "-g",
                "${file}",
                "-o",
                "${fileDirname}\\build\\${fileBasenameNoExtension}.exe"
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
            }
        }
    ],
    "version": "2.0.0"
    }
   
   ```

4. settings.json

    ```json
    {
     // [[C/C++]]
     "C_Cpp.errorSquiggles": "enabled",
     "C_Cpp.default.intelliSenseMode": "windows-gcc-x64",
     "C_Cpp.intelliSenseEngine": "disabled",
     // clangd
     "clangd.path": "clangd", // 直接使用环境变量
     // Clangd 运行参数(在终端/命令行输入 clangd --help-list-hidden 可查看更多)
     "clangd.arguments": [
         "--all-scopes-completion", // 全局补全(补全建议会给出在当前作用域不可见的索引,插入后自动补充作用域标识符),例如在main()中直接写cout,即使没有`#include <iostream>`,也会给出`std::cout`的建议,配合"--header-insertion=iwyu",还可自动插入缺失的头文件
         "--background-index", // 后台分析并保存索引文件
         "--clang-tidy", // 启用 Clang-Tidy 以提供「静态检查」，下面设置 clang tidy 规则
         "--clang-tidy-checks=performance-*, bugprone-*, misc-*, google-*, modernize-*, readability-*, portability-*",
         "--compile-commands-dir=${workspaceFolder}/build/", // 编译数据库(例如 compile_commands.json 文件)的目录位置
         "--completion-parse=auto", // 当 clangd 准备就绪时，用它来分析建议
         "--completion-style=detailed", // 建议风格：打包(重载函数只会给出一个建议);还可以设置为 detailed
         // "--query-driver=/usr/bin/clang++", // MacOS 上需要设定 clang 编译器的路径，homebrew 安装的clang 是 /usr/local/opt/llvm/bin/clang++
         // 启用配置文件(YAML格式)项目配置文件是在项目文件夹里的“.clangd”,用户配置文件是“clangd/config.yaml”,该文件来自:Windows: %USERPROFILE%\AppData\Local || MacOS: ~/Library/Preferences/ || Others: $XDG_CONFIG_HOME, usually ~/.config
         "--enable-config",
         "--fallback-style=Webkit", // 默认格式化风格: 在没找到 .clang-format 文件时采用,可用的有 LLVM, Google, Chromium, Mozilla, Webkit, Microsoft, GNU
         "--function-arg-placeholders=true", // 补全函数时，将会给参数提供占位符，键入后按 Tab 可以切换到下一占位符，乃至函数末
         "--header-insertion-decorators", // 输入建议中，已包含头文件的项与还未包含头文件的项会以圆点加以区分
         "--header-insertion=iwyu", // 插入建议时自动引入头文件 iwyu
         "--include-cleaner-stdlib", // 为标准库头文件启用清理功能(不成熟!!!)
         "--log=verbose", // 让 Clangd 生成更详细的日志
         "--pch-storage=memory", // pch 优化的位置(Memory 或 Disk,前者会增加内存开销，但会提升性能)
         "--pretty", // 输出的 JSON 文件更美观
         "--ranking-model=decision_forest", // 建议的排序方案：hueristics (启发式), decision_forest (决策树)
         // "--query-driver=C:\\Users\\11850\\scoop\\apps\\msys2\\2023-07-18\\mingw64\\bin\\g++*", // windows下的mingw位置
         "-j=12", // 同时开启的任务数量
         "--query-driver=D:\\Program Files\\LLVM\\bin\\g++*"
     ],
     // Clangd 找不到编译数据库(例如 compile_flags.json 文件)时采用的设置,缺陷是不能直接索引同一项目的不同文件,只能分析系统头文件、当前文件和include的文件
     "clangd.fallbackFlags": [
         "-std=c++17",
         "-I${workspaceFolder}/src/includes",
         "--target=x86_64-w64-windows-gnu", // 默认使用window gcc(MinGW),如果你是linux，就改成"--target=x86_64-linux-gnu"
     ],
     "clangd.onConfigChanged": "restart", // 重启 clangd 时重载配置,具体方法: F1 + Fn 打开命令面板，然后搜索“clangd: restart”
     "clangd.serverCompletionRanking": true, // 借助网上的信息排序建议
     "clangd.detectExtensionConflicts": true, // 当其它拓展与 clangd 冲突时警告并建议禁用
     "editor.suggest.snippetsPreventQuickSuggestions": true, // clangd的snippets有很多的跳转点，不用这个就必须手动触发Intellisense了
    }
    ```
