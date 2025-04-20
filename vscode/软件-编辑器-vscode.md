## 1  介绍

[vscode archlinux 帮助手册](https://wiki.archlinuxcn.org/wiki/Visual_Studio_Code)

## 2  下载安装

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

## 3  配置C++

### 3.1  预安装

在 Visual Studio Code 中配置 C++ 开发环境时，以下插件能极大提升效率和体验。根据功能分类推荐如下：

---

#### 3.1.1  **一、核心开发工具**

1. **C/C++ (Microsoft)**
   - 官方插件，提供 IntelliSense、代码导航、调试支持
   - 支持 C++11/14/17/20 标准
   - 需配置 `c_cpp_properties.json` 文件定义编译器路径和头文件

2. **Code Runner**
   - 一键运行代码（快捷键 `Ctrl+Alt+N`）
   - 支持多文件编译，需在 `settings.json` 配置编译器路径：

	 ```json
     "code-runner.executorMap": {
         "cpp": "cd $dir && g++ $fileName -o $fileNameWithoutExt && $dir$fileNameWithoutExt"
     }
     ```

---

#### 3.1.2  **二、调试与构建**

1. **CMake & CMake Tools**
   - 自动化 CMake 项目构建，支持跨平台编译
   - 提供图形化 CMake 配置界面，适合中大型项目

2. **C/C++ Debugger (LLDB/GDB)**
   - 集成 LLDB/GDB 调试器，支持断点、内存查看
   - 需配合 `launch.json` 配置调试参数

---

#### 3.1.3  **三、代码增强**

1. **Clangd (替代 IntelliSense)**
   - 基于 Clang 的代码补全和静态分析（比默认 IntelliSense 更精准）
   - 需禁用 Microsoft C/C++ 插件的 IntelliSense 避免冲突

2. **Doxygen Documentation Generator**
   - 自动生成 Doxygen 注释模板，快捷键 `/**` + Enter

3. **GitHub Copilot / Tabnine**
   - AI 代码补全，支持上下文智能提示

---

#### 3.1.4  **四、代码规范**

1. **Clang-Format**
   - 自动代码格式化，支持 `.clang-format` 配置文件
   - 快捷键 `Shift+Alt+F`

2. **C++ Linter (Cppcheck)**
   - 静态代码分析，检测潜在错误
   - 需安装 `cppcheck` 工具

3. **SonarLint**
	- 实时代码质量检查，支持 C++ 代码规范

---

#### 3.1.5  **五、实用工具**

1. **C/C++ Header Switch**
	- 快速切换 `.h` 和 `.cpp` 文件（快捷键 `Ctrl+Alt+S`）

2. **Include Autocomplete**
	- 头文件路径自动补全，支持相对路径和系统路径

3. **Remote - SSH / WSL**
	- 远程开发必备，支持 Linux 环境下的 C++ 编译

---

#### 3.1.6  **六、辅助工具**

1. **GitLens**
	- 代码版本管理增强，显示代码作者和提交历史

2. **Todo Tree**
	- 高亮代码中的 `TODO`/`FIXME` 注释

3. **Bracket Pair Colorizer**
	- 彩色括号匹配，避免嵌套混乱

---

#### 3.1.7  **七、测试相关**

1. **TestMate C++**
	- 集成 Google Test、Catch2 等单元测试框架
	- 自动检测并运行测试用例

---

#### 3.1.8  **八、界面优化**

1. **Material Icon Theme**
	- 文件图标主题，提升项目文件辨识度

2. **One Dark Pro**
	- 高对比度暗色主题，减少视觉疲劳

---

#### 3.1.9  **配置建议**

- **Windows 用户**：安装 MinGW-w64 或 MSVC 编译器，配置环境变量
- **Linux/macOS**：使用系统自带的 GCC/Clang，通过终端安装 `gdb`/`lldb`
- 示例 `.vscode/tasks.json` 编译任务配置：

  ```json
  {
    "version": "2.0.0",
    "tasks": [{
      "label": "build",
      "type": "shell",
      "command": "g++",
      "args": ["-g", "${file}", "-o", "${fileDirname}/${fileBasenameNoExtension}"],
      "group": { "kind": "build", "isDefault": true }
    }]
  }
  ```

---

根据项目需求选择插件组合，避免过多插件影响性能。建议优先配置核心工具（C/C++、CMake、Clangd），再按需添加辅助功能。

### 3.2  配置文件

`.vscode`文件夹：

- tasks.json (compiler build settings) ，负责编译
- launch.json (debugger settings)，负责调试
- c_cpp_properties.json (compiler path and IntelliSense settings)，负责更改路径等设置

#### 3.2.1  tasks.json

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

- `command`：程序路径
- `args`：传给g++的命令行参数
- `label`：标签值是将在任务列表中看到的内容；可以随意命名它。
- `group`：
	- `isDefault`：
		- `true`：表示支持通过快捷键 `ctrl+shift+B` 来执行该编译任务。
		- `false`：从菜单中选择运行：终端(Terminal)->运行生成任务(Run Build Task)。

#### 3.2.2  launch.json

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

- `program`：指调试程序的位置，对应`tasks.json`中`args`对应value的最后一项
- `stopAtEntry`：
	- `false`：默认值，C++拓展不会向源代码添加任何断点。
	- `true`，将使调试器在开始调试时停止在 main 方法上。

#### 3.2.3  c_cpp_properties.json

1. `Ctrl+Shift+P`，启动命令模版
2. 在下拉菜单中选择，C/C++: 编辑配置(JSON)，生成`c_cpp_properties.json`文件

## 4  插件 - vim

配置优化

1. **解决快捷键冲突**
	在 `settings.json` 中添加：

	```json
    "vim.handleKeys": {
      "<C-c>": false,  // 允许 VSCode 处理 Ctrl+C
      "<C-v>": false   // 允许 VSCode 处理 Ctrl+V
    }
    ```

2. **自定义快捷键**
	通过 `keybindings.json` 扩展 Vim 功能，例如：

	```json
    {
      "key": "Ctrl+s",
      "command": "workbench.action.files.save",
      "when": "editorTextFocus && vim.mode == 'Normal'"
    }
    ```
