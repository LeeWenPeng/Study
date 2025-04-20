# PowerShell 脚本

## 问题一

将一个目录下所有子目录中的文件移动到该目录中

```powershell
$mainDir = "PATH"

Get-ChildItem -Path $mainDir -Recurse -File | Move-Item -Destination $mainDir

Write-Host "文件移动完成！"
```

## 问题二

将一个目录
