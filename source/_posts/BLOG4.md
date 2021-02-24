---
title: Hero-NexT写作技巧
comment: false
tags:
  - Hexo
  - NexT
  - Blog
categories: 写作技巧 (Write Skill)
abbrlink: 309a2d82
date: 2021-02-19 15:14:30
banner_img:
index_img:
translate_title:
top:
---



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/54f27e7fbe3b520.png)

<div align=center>
  <font size="3">
    <i>
      <a href="https://www.pixilart.com/art/desktop-54f27e7fbe3b520?ft=featured&ft_id=">Desktop</a> by 
      <a href="https://www.pixilart.com/charly-fox">Charly-Fox</a>
    </i>
  </font>
</div>



### 引言

本文介绍了 Hexo-NexT 中常用的内置标签，包括 note 标签、label 标签、button 标签、tab 标签以及代码块的高级用法，通过使用写作标签可以快速编写样式丰富的文档片段。

<!--more-->



### 常用技巧

- 阅读更多： `<!-- more-->`
- 空格： 1 个空格字符 ` `  1 个中文宽度 ` `
- 换 行： `</br>`
- 插入图片： `<img src=" " width="600" hegiht="400" >`
- 居中： `<center> </center>`



### 文本居中标签

参考 [内置标签 文本居中的引用](https://theme-next.iissnan.com/tag-plugins.html)

文本居中标签有以下三种写法：

```markdown
<!-- HTML方式: 直接在 Markdown 文件中编写 HTML 来调用 -->
<!-- 其中 class="blockquote-center" 是必须的 -->
<blockquote class="blockquote-center">文本居中</blockquote>

<!-- 标签方式 -->
{% centerquote %}文本居中{% endcenterquote %}

<!-- 标签别名 -->
{% cq %}文本居中{% endcq %}
```

#### 举例

```markdown
{% cq %}文本居中{% endcq %}
```

#### 效果

{% cq %}文本居中{% endcq %}





### 代码块

书写方式：

```markdown
​``` [language] [title] [url] [link text]
 code snippet
​```
```

其中，各参数意义如下：

- langugae：语言名称，引导渲染引擎正确解析并高亮显示关键字
- title：代码块标题，将会显示在左上角
- url：链接地址，如果没有指定 link text 则会在右上角显示 link
- link text：链接名称，指定 url 后有效，将会显示在右上角

如果不想填写 title，可以在 language 和 url 之间添加至少三个空格。

### note 标签

#### 修改主题配置文件

打开主题配置文件 `config.yml`, 修改 note 标签 ：

```yaml
# note 标签
# Note tag (bs-callout)
note:
  # Note tag style values:
  #  - simple    bs-callout old alert style. Default.
  #  - modern    bs-callout new (v2-v3) alert style.
  #  - flat      flat callout style with background, like on Mozilla or StackOverflow.
  #  - disabled  disable all CSS styles import of note tag.
  style: flat
  icons: true
  border_radius: 3
  # Offset lighter of background in % for modern and flat styles (modern: -12 | 12; flat: -18 | 6).
  # Offset also applied to label tag variables. This option can work with disabled note tag.
  light_bg_offset: 20%  # 默认背景减淡效果，以百分比计算
```

#### 效果展示

通过 note 标签可以为段落添加背景色，语法如下：

```markdown
{% note [class] %}
文本内容 (支持行内标签)
{% endnote %}
```

支持的 class 种类包括 `default` `primary` `success` `info` `warning` `danger`，也可以不指定 class。

#### 举例

```markdown
{% note default %}
default
{% endnote %}

{% note primary %}
primary
{% endnote %}

{% note success %}
success
{% endnote %}

{% note info %}
info
{% endnote %}

{% note warning %}
warning
{% endnote %}

{% note danger %}
danger
{% endnote %}
```

#### 效果

{% note default %}
default
{% endnote %}

{% note primary %}
primary
{% endnote %}

{% note success %}
success
{% endnote %}

{% note info %}
info
{% endnote %}

{% note warning %}
warning
{% endnote %}

{% note danger %}
danger
{% endnote %}



### button 按钮

通过 button 标签可以快速添加带有主题样式的按钮，语法如下：

```markdown
{% button /path/to/url/, text, icon [class], title %}
也可简写为：
{% btn /path/to/url/, text, icon [class], title %}
```

#### 举例

```markdown
{% btn #, 文本 %}
{% btn #, 文本 & 标题, 标题 %}
{% btn #, 文本 & 图标, home %}
{% btn #, 文本 & 大图标 (固定宽度), home fa-fw fa-lg %}
```

#### 效果

{% btn #, 文本 %}
{% btn #, 文本 & 标题, 标题 %}
{% btn #, 文本 & 图标, home %}
{% btn #, 文本 & 大图标 (固定宽度), home fa-fw fa-lg %}





### tab 标签

tab 标签用于快速创建 tab 选项卡，语法如下：

```markdown
{% tabs [Unique name], [index] %}
  <!-- tab [Tab caption]@[icon] -->
  标签页内容（支持行内标签）
  <!-- endtab -->
{% endtabs %}
```

其中，各参数意义如下：

- Unique name: 全局唯一的 Tab 名称，将作为各个标签页的 id 属性前缀
- index: 当前激活的标签页索引，如果未定义则默认选中显示第一个标签页，如果设为 - 1 则默认隐藏所有标签页
- Tab caption: 当前标签页的标题，如果不指定则会以 Unique name 加上索引作为标题
- icon: 在标签页标题中添加 Font awesome 图标

#### 举例

```markdown
{% tabs Tab标签列表 %}
  <!-- tab pixel1 -->
    标签页1文本内容
	<img src="https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/794d75495aab27d.png" width="600" hegiht="400" >
  <!-- endtab -->
  <!-- tab pixel2 -->
    标签页2文本内容
	<img src="https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/9d7671802b187e8.png" width="600" hegiht="400" >
  <!-- endtab -->
  <!-- tab pixel3 -->
    标签页3文本内容
	<img src="https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/67d649a40eb458c-20210219153648077.png" width="600" hegiht="400" >
  <!-- endtab -->
  <!-- tab pixel4 -->
    标签页4文本内容
	<img src="https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/f3b36762798dec9.png" width="600" hegiht="400" >
  <!-- endtab -->
{% endtabs %}
```

#### 效果

{% tabs Tab标签列表 %}
  <!-- tab pixel1 -->
    标签页1文本内容
	<img src="https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/794d75495aab27d.png" width="600" hegiht="400" >
  <!-- endtab -->
  <!-- tab pixel2 -->
    标签页2文本内容
	<img src="https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/9d7671802b187e8.png" width="600" hegiht="400" >
  <!-- endtab -->
  <!-- tab pixel3 -->
    标签页3文本内容
	<img src="https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/67d649a40eb458c-20210219153648077.png" width="600" hegiht="400" >
  <!-- endtab -->
  <!-- tab pixel4 -->
    标签页4文本内容
	<img src="https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/f3b36762798dec9.png" width="600" hegiht="400" >
  <!-- endtab -->
{% endtabs %}
---
