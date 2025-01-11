# obsidian

## 配置

### 1 多库共享

多个库的共享配置方法为：

[[Linux_1_命令#1-12 文件链接| Linux软链接]]

## 官方插件

### 插件列表

#### 1 白板

作用：使用卡片绘制思维图，简单便捷

## 第三方插件

[插件推荐链接](https://www.bilibili.com/video/BV1cs4y1H77h/?spm_id_from=333.337.search-card.all.click&vd_source=d9e178b992882410dc0927d40741958a)

插件使用原则：需要的就是最好的

1. 很多插件都已经被官方变成了自带的功能
2. 有很多很热门的插件，并不需要

### 1 第三方插件安装

1. 下载
	1. github
	2. PKmer

>[!note]
>从github上搜索插件的小技巧: 前往插件注册页面搜索插件，就能看到插件对应的仓库位置
>[github－obsidian插件注册页面](https://github.com/obsidianmd/obsidian-releases/blob/master/community-plugins.json)

2. 并解压好的插件移入仓库配置文件夹

	`.obsidian/plugins`

3. 在**设置**中，**第三方插件**处，打开**安全模式**，并勾选插件

### 2 插件列表

#### 1 obsidian-proxy-github——无效

作用：代理插件

#### 2 templater

作用：模版增强插件

+ 创建文件时，自动设置属性
+ 辅助快捷输入

#### 3 editing-toolbar

作用：增加一个类似于word的编辑条

#### 4 dataview

作用：类似于SQL的查询插件，很多插件的底层插件，必装

#### ５ style settings

作用：帮助设置主题样式，属于底层插件，必装

#### ６ image auto upload

作用：图片自动上传图床

#### 7 hover-editor——==GOOD!!!==

作用：增强悬浮窗

#### 8 excalidraw——==GOOD!!!==

作用：提供一个很自由的手绘风画板

+ 更自由强大
+ 类似于ipad笔记

#### 9 another quick switcher

作用：快速切换增强

+ 搜索
+ 快速切换
+ 历史使用笔记记录
+ 预览
+ 更高自由度

#### 10 outliner——无用

作用：列表增强插件

#### 11 settings search

作用：设置页面的搜索框

#### 12 Editor Syntax Highlight

作用：代码高亮

#### 13 Linter——==GOOD！！！==

作用：格式化样式化笔记

>[!bug] 注意在勾选自动添加H1标题后，就不要再勾选从H2标题开始了，这样会导致无限添加标题的BUG

#### 14 omnisearch

作用：全局搜索

[学习课程](https://www.bilibili.com/video/BV1184y1r7Un/?spm_id_from=333.337.search-card.all.click&vd_source=d9e178b992882410dc0927d40741958a)

对中文支持有限，**不如左侧搜索功能**

#### 15 Mind Map

作用：自动生成思维导图

#### 16 Surfing

作用：在ob内部打开网页

#### 17 Various complements

作用：根据字典和笔记提供自动补全

## 主题

### 1 主题安装

1. 下载主题
	1. github
	2. PKmer
2. 将下载解压后的文件放入主题文件夹
	1. 主题样式文件夹`.obsidian/themes`
	2. 主题额外样式文件夹`.obsidian/snippets`

>[!note]
>+ 对于主题，其实基本上只需要文件夹中的`theme.css`文件，因此可以将该文件改成对应主题名字放入到`.obsidian/themes`中
>+ 如果是将解压后的文件夹放入到`.obsidian/themes`中，则需要将文件夹改成对应主题名字。注意：==一定是在官方库中登记过的名字，否则不识别！！！==

### 2 主题列表

#### 1 Blue Topaz

已经不再维护，但仍然推荐这个

#### 2 Minimal

#### 3 AnuPpuccin

#### 4 Border

## 特性

### 13 种 callout

[callout 笔记](https://pkmer.cn/Pkmer-Docs/10-obsidian/obsidian%E5%9F%BA%E6%9C%AC%E4%BD%BF%E7%94%A8/callout/#:~:text=obsidian%20%E5%85%B1%E6%8F%90%E4%BE%9B%E4%BA%86%2013%20%E7%A7%8D%20callout%20%E4%BB%96%E4%BB%AC%E6%98%AF%E5%A4%A7%E5%B0%8F%E5%86%99%E4%B8%8D%E6%95%8F%E6%84%9F%E7%9A%84%EF%BC%8C%E4%BE%8B%E5%A6%82%3E%20%5B%21BUG%5D%2C%3E%20%5B%21bug%5D,callout%20%E5%8F%AF%E8%83%BD%E6%9C%89%E5%BE%88%E5%A4%9A%E7%A7%8D%E5%88%AB%E5%90%8D%EF%BC%8C%E4%BE%8B%E5%A6%82%20%3E%20%5B%21info%5D%20%E5%92%8C%20%3E%20%5B%21todo%5D%20%E7%9A%84%E6%A0%B7%E5%BC%8F%E6%98%AF%E4%B8%80%E6%A0%B7%E7%9A%84%EF%BC%9B)

语法：

```callout
>[!参数1]参数2 Title
>content
```

参数：

+ 参数1：callout类型，一共有13种类型
+ 参数2: callout栏是否展开
	+ 空：展开
	+ `+`：默认展开，但允许折叠
	+ `-`：默认折叠，但允许展开

![[obsidian_callout#callout 展示]]
