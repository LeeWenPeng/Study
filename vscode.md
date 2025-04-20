includePath 配置时

**常见错误示例**

+   "includePath": ["include/*"]	无法找到子目录中的头文件	改为 "include/**"**
+   **"includePath": ["libs"]	仅包含 libs 目录本身，不包含其内容改为 "libs/**"


>    [!note] 在文件路径匹配中，通配符 `*` 和 `**` 的区别
>
>    -   **`\*`（单星号）**：匹配 **当前目录层** 的任意字符（不包括子目录）。
>    -   **`\**`（双星号）**：匹配 **所有层级的子目录**（递归匹配）。



## 问题：VSCode sigset_t 未定义

### 原因

`sigset_t ` 并不在 `C99 / C11 standard` 里。但是它是包含在 `POSIX standard` 里的。

### 解决方法

为了避免出现此错误提示，我们需要更改 VSCode C/C++ Extension 的配置。

1.   `Ctrl + Shift + P`呼出菜单
2.   选择 `C/C++ Edit Configurations （JSON）`，将其中的 从默认的 `c11` 改成 `gnu99` 即可。
     1.   也就是修改 `c_cpp_properties.json`文件中的`"cStandard": "gnu99"`
