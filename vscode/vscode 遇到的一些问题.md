# Vscode 遇到的问题以及解决方案

## 1 打开 web 视图报错

解决方案：

1. 关闭 vscode
2. 打开 `cmd`
3. 输入代码 `code --no-sandbox`
4. 这时 vscode 就会自动打开

## 2 vscode 终端打印中文乱码

问题原因：windows 系统默认中文编码为 `GBK`，而vscode 新建文件默认编码为 `UTF-8`

解决方案：修改文件格式为 `GBK`

1. 点击底部状态栏中的 `UTF-8`，进行 `select encoding`
   
2. 在上方弹出的选项中选择 `save with encoding`
   
3. 然后从弹出窗口中搜索选择 `GBK`
   
4. 成功

