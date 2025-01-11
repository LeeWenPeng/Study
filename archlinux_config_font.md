## 1. 相关网址

+ [archlinux wiki 字体](https://wiki.archlinuxcn.org/wiki/字体)
+ [archlinux wiki 字体配置](https://wiki.archlinuxcn.org/wiki/%E5%AD%97%E4%BD%93%E9%85%8D%E7%BD%AE)

## 2. 字体安装位置

+ 为个人用户安装：`~/.local/share/fonts`
+ 为全体用户安装：`/usr/local/share/fonts`
	+ 不存在该文件夹则需要自行创建
+ 包管理器安装：`/usr/share/fonts`
	+ 请勿手动修改

### 2.1. 验证字体是否安装成功

1 检查字体是否已经安装

```shell
fc-list | grep "字体名称"
```

2 检查字体路径

```shell
cd /Fonts/Path/Of/Yourself
```

## 3. 字体配置

### 3.1. Fontconfig 配置文件

Fontconfig 的配置文件可以设置默认字体和字体替代。

全局配置文件路径：

+ `/etc/fonts/local.conf`

用户配置文件路径：

+ `~/.config/fontconfig/fonts.conf`（如果不存在，手动创建）

配置文件内容

```xml
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
  <!-- 设置默认字体 -->
  <match target="pattern">
    <test name="family" compare="eq">
      <string>sans-serif</string>
    </test>
    <edit name="family" mode="assign" binding="strong">
      <string>Noto Sans</string> <!-- 替换为你的默认字体 -->
    </edit>
  </match>
</fontconfig>
```

### 3.2. Kitty

在 `~/.config/kitty/kitty.conf` 中设置字体：

```plaintext
font_family Font_Name
font_size 12
```

+ `Font_Name`：可以通过`fc-query`进行查询获取

### 3.3. hyprland 字体设置

hyprland 没有统一的字体设置，通过设置其依赖组件的字体，从而达到对 hyprland 的字体设置。

+ 编辑 `~/.config/hypr/hyprland.conf`，为终端模拟器指定字体：

  ```plaintext
  exec = kitty -o font_family='Font_Name'
  ```

### 3.4. Firefox

  1. 转到 **设置 > 常规 > 字体和颜色**。
  2. 设置默认字体。

## 4. 有用方法

### 4.1. 刷新字体缓存

在完成字体的安装和配置后，需要刷新字体缓存

```shell
fc-cache -fv
```

+ `-f`：强制
+ `-v`：显示详细信息

### 4.2. 列出全部字体名称

可以通过该操作查看字体是否安装成功

```shell
fc-list : family
```

### 4.3. 查询字体名称

可以通过该操作查询字体包的名称

```shell
fc-query -f '%{family[0]}\n' /FONT/PATH/OF/YOURSELF
```

### 4.4. 检测字体是否可用

验证字体渲染的可用性

```shell
fc-match "FontName"
```

### 4.5. 查看当前正在使用的字体

查看当前设置的字体

```shell
fc-match sans-serif
fc-match serif
fc-match monospace
```
