## 1. 配置文件位置

### 1.1. 主配置文件

`~/.config/hypr/hyprland.conf`

### 1.2. source 关键字

不在主配置文件中对配置进行修改，而是新建配置文件，并通过关键字`source` 将用户自建配置文件引入到主配置文件中。

语法

```bash
source = 用户自建配置文件路径
```

## 2. 样式修改

### 2.1. 字体修改

Hyprland 本身没有直接设置字体的选项，但它依赖其他组件（例如 Waybar、dmenu、终端模拟器等）的字体配置。

因此，要通过组件的配置文件指定字体。

archlinux字体文件夹

+ `~/.local/share/fonts`
+ `usr/share/fonts`

```shell
mkfontdir
mkfontscale

# 刷新字体缓存
sudo fc-cache -f -v
```

## 3. 应用快捷键

将应用的启动与按键绑定，以快速启动应用

语法

```bash
bind = 按键1, 按键2, exec, 应用启动命令
```

+ 对于 archlinux 通过 pacman 工具安装的应用，会自动配置环境变量。
+ 对于用户自建应用，需要指定具体命令或配置 `PATH`
