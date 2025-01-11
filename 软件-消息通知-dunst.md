## 1. 前倾提要

[archlinux wiki dunst 网址](https://wiki.archlinuxcn.org/wiki/Dunst)

[dunst 官网](https://dunst-project.org/)

## 2. 安装

直接通过 `pacman` 安装 `dunst` 软件包

示例配置文件位于 `/etc/dunst/dunstrc`

用户配置文件位于 `/.config/dunst/dunstrc`

## 3. dunstctl

使用 `dunstctl` 控制 `dunst`

关闭所有通知

```shell
dunstctl close-all
```

显示历史记录

```shell
dunstctl history-pop
```

切换 dunst 状态

```shell
dunstctl set-paused true/false/toggle
```

查看 dunst 是否在运行/暂停

```shell
dunstctl is-paused
```

禁用/重启 dunst

```shell
killall -SIGUSR1 dunst
killall -SIGUSR2 dunst
```

## 4. dunstrc 介绍

dunst 的配置文件。

[dunstrc](https://dunst-project.org/documentation/)

以类似 ini 的格式划分为多个部分：

+ 每一部分都是以方括号中的节名开头。
+ 之后是指定设置的键值对列表。
+ 空白纯粹是装饰性的，不会改变结果。
+ `#` 符号被解释为注释

语法

```dunstrc
[section_name]
	key = value 
	...
```

section 分为三类：

+ global section
+ urgency sections
+ normal sections

其中，global section 和 urgency sections 是两种特殊部分。

每一个 section 中，都是由指定设置的键值对列表组成。

在键值对中，有部分特殊的键值对，称之为规则。

## 5. global section

 `global` 包含适用于所有 dunst 的常规设置。

```dunstrc
[global]
	moniter = 0
	follow = mouse
Rules

```

> `global` 部分没有过滤器，匹配所有通知。

## 6. urgency sections

## 7. rules

**规则为指定设置的键值对**。规则允许有条件地修改通知。它们可以位于任何名称的部分中，即使是特殊部分。特殊部分不允许添加过滤器，因为它们默认具有隐含的过滤器。

特殊部分：

+ `global`：包含适用于所有 dunst 的常规设置。
+ `urgency sections`：紧急部分允许写入过滤器，因为其自带过滤器。
	+ `urgency_low`
	+ `urgency_normal`
	+ `urgency_critial`

配置规则包含两部分：

+ 过滤器规则： filtering rules，定义控制何时应用规则的过滤器。
+ 修改规则 ： modifying rules，定义匹配规则时应采用的操作。

**规则是按照顺序应用的**。如果通知被前面的规则修改，将会对其是否被之后的规则匹配造成影响。

### 7.1. filtering rules

使用过滤规则，可以匹配通知，以便仅将规则应用于通知的子集。

如果在小节中不指定任何过滤器，则规则将匹配所有的通知。

过滤器规则基于字符串过滤，可以使用正则表达式。通过设置`enable_posix_regex = true`，可以使用POSIX扩展正则表达式语法。

过滤器规则是通过过滤器属性分配给要匹配的值来创建的。匹配值时支持类似 Shell 的 globbing。

如果存在多个过滤器表达式，则所有过滤器表达式都必须匹配要应用的规则。（也就是说，所有过滤器表达式之间的逻辑关系为 AND 关系）。

重要的过滤器规则

```dunstrc
appname = "***"


```

### 7.2. modifying rules

修改规则通过为规则定义中的通知属性赋值来创建的。

重要的修改规则

```dunstrc
format = "..."

urgency = "..."


```

通过`history_ignore=yes`，可以完全将某些通知从历史记录中排除。

## 8. 脚本

在规则中，您可以通过将“script”选项分配给要运行的脚本的名称来指定每次匹配规则时要运行的脚本。

当脚本被调用时，触发它的通知的细节将通过环境变量传递。

可用环境变量：

+ DUNST_APP_NAME
+ DUNST_SUMMARY
+ DUNST_BODY
+ DUNST_ICON_PATH：是图标文件的绝对路径
+ DUNST_URGENCY
+ DUNST_ID
+ DUNST_PROGRESS
+ DUNST_CATEGORY
+ DUNST_STACK_TAG
+ DUNST_URLS
+ DUNST_TIMEOUT
+ DUNST_TIMESTAMP
+ DUNST_DESKTOP_ENTRY
+ DUNST_STACK_TAG
如果取消通知，则除非always_run_script设置为true，否则不会运行脚本。
