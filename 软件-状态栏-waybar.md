## 1  样式

### 1.1  用户自建样式

不直接在原本的样式文件上修改，而是，新建样式文件，并通过`import`关键字将用户自定义样式引入到主样式文件中

#### 1.1.1  语法

主样式文件

```css
@import url("用户自建样式文件路径");
```

> CSS 中对于相同元素的多个不同的样式设置，后来的样式会覆盖掉之前的样式

## 2  waybar配置生效

### 2.1  重启计算机

重启计算机配置文件重新加载

### 2.2  重启 waybar

1. 关闭 waybar

```bash
pkill waybar
```

2. 启动 waybar

```bash
waybar &
```

> 启动waybar 除了通过终端外，可以通过 bmenu 或 wofi等应用管理器
