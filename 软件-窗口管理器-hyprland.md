## 1  配置文件位置

### 1.1  主配置文件

`~/.config/hypr/hyprland.conf`

### 1.2  source 关键字

不在主配置文件中对配置进行修改，而是新建配置文件，并通过关键字`source` 将用户自建配置文件引入到主配置文件中。

语法

```bash
source = 用户自建配置文件路径
```

## 2  样式修改

### 2.1  字体修改

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

## 3  hyprctl

### 3.1  语法

```bash
hyprctl [flags] <command> [args ...|--help]
```

### 3.2  常用命令

```bash
# 查看屏幕信息
hyprctl monitors 

# 查看所有窗口属性
hyprctl clients 

# 查看工作空间信息
hyprctl workspaces
```

## 4  应用绑定快捷键

将应用的启动与按键绑定，以快速启动应用

语法

```bash
bind = 按键1, 按键2, exec, 应用启动命令
```

+ 对于 archlinux 通过 pacman 工具安装的应用，会自动配置环境变量。
+ 对于用户自建应用，需要指定具体命令或配置 `PATH`

## 5  窗口规则

Hyprland 的窗口规则（`windowrule` 和 `windowrulev2`）的官方文档可以在以下地址找到：

---

### 5.1  **文档地址**

+ **Hyprland 窗口规则文档**
  [https://wiki.hyprland.org/Configuring/Window-Rules/](https://wiki.hyprland.org/Configuring/Window-Rules/)

---

### 5.2  **基础语法**

+ **`windowrule`**
  基本规则，格式为：

  ```ini
  windowrule = <规则>, <窗口匹配条件>


```cpp

  例如：  
  ```ini
  windowrule = float, ^(kitty)$
```

+ **`windowrulev2`**
  更灵活的规则（支持正则表达式和多重条件），格式为：

  ```ini
  windowrulev2 = <规则>, <匹配条件>


```cpp

  例如：

  ```ini
  windowrulev2 = float, class:^(firefox)$, title:^(Downloads)$
```

---

#### 5.2.1  **常用规则**

+ **窗口属性控制**
  + `float`：让窗口浮动。
  + `tile`：强制平铺。（hyprland 应用默认平铺打开）
  + `nofocus`：窗口打开时不自动获取焦点。
  + `size <宽度> <高度>`：设置窗口大小（如 `size 800 600`）。
  + `move <X> <Y>`：设置窗口位置（如 `move 100 100`）。
  + `center`：窗口居中。
  + `monitor <显示器名称>`：指定窗口在某个屏幕打开（如 `monitor HDMI-A-1`）。
  + `workspace <工作区>`：指定窗口到特定工作区（如 `workspace 3`）。
+ **高级规则**
  + `pin`：将窗口固定在所有工作区显示。
  + `noblur`：禁用窗口模糊效果。
  + `opacity <值>`：设置窗口透明度（如 `opacity 0.9`）。

---

### 5.3  **窗口匹配条件**

+ **匹配字段**
  + `class`：窗口类名（通过 `hyprctl clients` 或 `xprop` 查询）。
  + `title`：窗口标题。
  + `initialClass`：应用启动时的初始类名（用于多实例应用）。
  + `xwayland`：匹配 XWayland 窗口（`0` 或 `1`）。
+ **正则表达式**
  使用 `^` 和 `$` 精确匹配，例如 `class:^(Alacritty)$`。

---

### 5.4  **示例**

```ini
# 基础规则：让所有终端浮动
windowrule = float, ^(kitty|Alacritty)$

# 高级规则：将 Firefox 的下载窗口浮动并居中
windowrulev2 = float, class:^(firefox)$, title:^(Downloads)$
windowrulev2 = center, class:^(firefox)$, title:^(Downloads)$

# 指定 Obsidian 在屏幕 DP-1 和工作区 5 打开
windowrulev2 = monitor DP-1, class:^(obsidian)$
windowrulev2 = workspace 5, class:^(obsidian)$
```

### 5.5  **注意事项**

+ 规则需写在配置文件（`hyprland.conf`）的 **全局作用域**（不能放在 `bind` 或 `exec` 块内）。
+ 规则按顺序生效，后定义的规则可能覆盖前面的。
+ 部分规则（如 `monitor`）需要 Hyprland 版本 ≥ 0.30.0。

## 6  工作空间绑定窗口

```bash
workspace= n, monitor:显示器名称
```

+ 显示器名称查询：`hyprctl monitors`
