---
title: Layers
comment: false
tags:
  - Cpp
  - Game Engine
categories: 游戏引擎开发 (Game Engine Series)
abbrlink: e124e866
date: 2021-05-29 16:48:27
type:
banner_img:
index_img:
translate_title:
top:
mathjax:
---

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/c315cb71884743.5bd475c09da1a.jpg)

<div align=center>
  <font size="3">
    <i>
      <a href="https://www.behance.net/gallery/71884743/Crypto-Camp-Poster">Crypto Camp Poster</a> by 
      <a href="https://www.behance.net/MChahin">Mohamed Chahin</a>
    </i>
  </font>
</div>

### 引言

上一节我们借助GLFW为游戏引擎创建窗口事件，今天我们来看一看层堆栈以及我们该如何使用它们。


<!--more-->



每当我向人们谈论层次时，我通常最终都将其与类似Photoshop这样的东西比较，但显然它不像游戏引擎那样具有交互性，我们可以把其视为Photoshop中的一层，拥有一个有序列表（通常情况是栈）。

它们不仅决定图形绘制的顺序，也包含引擎中的事件、更新逻辑等等，所以在我们的引擎具有运行功能（基于`while`循环），这种循环不断重复到循环被终止。我们可以视为该层堆栈内的一层，就像可以打开图层一样在Photoshop中关闭，然后将其隐藏或禁用就可以了。同样的，只要启用了图层类型，我们就可以在这里进行同样的操作：通过游戏循环，各层将按照其实际顺序进行更新。
