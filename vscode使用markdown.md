## 1  vscode

- [1 vscode使用markdown](#1-vscode使用markdown)
- [2 Markdown All in One](#2-markdown-all-in-one)
  - [2.1 配置](#21-配置)
  - [2.2 操作](#22-操作)
- [3 Markdown Preview Enhanced](#3-markdown-preview-enhanced)
  - [3.1 配置](#31-配置)
  - [3.2 操作](#32-操作)
- [4 绘图 mermaid](#4-绘图-mermaid)
- [5 markdown语法检查](#5-markdown语法检查)

### 1.1  vscode使用markdown

插件

1. Markdown All in One
	markdown插件，各种markdown常见优化

2. Markdown Preview Mermaid Support
   markdown绘图

3. markdownlint
	markdown语法检查器
	[规则语法网站](https://www.jianshu.com/p/51523a1c6fe1)

4. Markdown Preview Github Styling
   markdown在github page上的样式预览

5. Markdown Preview Enhanced
   和Markdown All in One是一种类型的插件，但预览功能和导出功能更为强大

### 1.2  Markdown All in One

用户手册：<https://github.com/yzhang-gh/vscode-markdown#auto-completions>

#### 1.2.1  配置

1. 关于自动生成目录的配置
   在设置中搜索`Toc`，搜索出的选项就是关于自动生成目录的设置选项

#### 1.2.2  操作

1. 自动生成目录
   1. 打开命令面板
	  1. 右键，弹出面板最下面
	  2. `shift + ctrl + P`
   2. 在命令面板上输入`TOC`
   3. 选择`Create Table of Contents`
2. 自动添加/删除章节号
   1. 打开命令面板
   2. 在面板上输入section
   3. 选择添加或删除章节号
3. 打开实时预览：Ctrl + Shift + V
4. 快速打开和关闭大纲：Ctrl + Shift + O

### 1.3  Markdown Preview Enhanced

帮助手册: <https://www.bookstack.cn/read/mpe/zh-cn-pdf.md>

#### 1.3.1  配置

1. 打开markdown中的代码运行功能

   对`Enable Script Execution`选项勾选

#### 1.3.2  操作

1. 插入目录
   1. 插入`[TOC]`
   2. Html代码

	  ```markdown
      <!-- @import "[TOC]" {cmd="toc" depthFrom=2 depthTo=3 orderedList=false} -->
      ```

2. 快速预览：`ctrl k,v`

```c++
#include <iostream>
using namespace std;

int main(){

   cout << "asdasd" <<endl;

   return 0;
}
```

### 1.4  绘图 mermaid

[mermaid 帮助手册](https://mermaid.nodejs.cn/)

### 1.5  markdown语法检查

[markdown语法文档](https://github.com/DavidAnson/markdownlint/tree/main/doc)
