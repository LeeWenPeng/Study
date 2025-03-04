## 1  archlinux系统中使用VLC

### 1.1  下载

```bash
sudo pacman -S vlc
```

### 1.2  设置语言

VLC 在其“首选项”菜单中不提供更改语言的选项。但是可以修改VLC的桌面文件来修改语言。

1 打开 VLC 的桌面文件

```bash
sudo vim /usr/share/applications/vlc.desktop
```

2 修改启动项

文件原启动项为

```ini
Exec=/usr/bin/vlc %U
```

在等号后添加`env LANGUAGE=你要修改的语言缩写 `，修改后为

```cpp
Exec=env LANGUAGE=你要修改的语言缩写 /usr/bin/vlc %U
```
