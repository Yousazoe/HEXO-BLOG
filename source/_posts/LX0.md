---
title: LATEX现学现用抢救指南
top: false
mathjax: true
abbrlink: d27a4a46
translate_title: latex-rescue-guide
tags:
  - Write
  - Latex
  - Markdown
categories: 写作技巧 (Write Skill)
date: 2020-11-02 23:43:56
comments: false
---



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1gkb9od3oecj314g0mg755.jpg)



### 引言

本文作为即忘即看的备忘文档，适用于各种编写博客需要专业数学公式但不熟悉的Latex的读者，所有内容摘自 [常用数学符号的 LaTeX 表示方法](http://mohu.org/info/symbols/symbols.htm)。

<!--more-->



### 指数与下标

指数和下标可以用`^`和`_`后加相应字符来实现。比如:

```latex
$a_{1}$ \qquad 
$x^{2}$ \qquad 
$e^{-\alpha}$ \qquad 
$a^{3}_{i,j}$ \qquad 
$e^{x^2} \neq {e^x}^2$
```

效果如下：

> $a_{1}$ $\qquad$ $x^{2}$ $\qquad$ $e^{-\alpha}$ $\qquad$ $a^{3}_{i,j}$ $\qquad$ $e^{x^2} \neq {e^x}^2$



### 根号

平方根（square root）的输入命令为：`\sqrt`，n 次方根相应地为:` \sqrt[n]`。方根符号的大小由LATEX自动加以调整。也可用`\surd` 仅给出符号。比如：

```latex
$\sqrt{x}$ \qquad 
$\sqrt{x^{2}+\sqrt{y}}$ \qquad 
$\sqrt[3]{2}$ \qquad 
$\surd[x^2+y^2]$
```

效果如下：

> $\sqrt{x}$ $\qquad$ $\sqrt{x^{2}+\sqrt{y}}$ $\qquad$ $\sqrt[3]{2}$ $\qquad$ $\surd[x^2+y^2]$



### 水平线

命令`\overline` 和`\underline` 在表达式的上、下方画出水平线。比如：

```latex
$\overline{m+n}$ \qquad
$\underline{m+n}$
```

效果如下：

> $\overline{m+n}$ $\qquad$$\underline{m+n}$



### 水平大括号

命令`\overbrace` 和`\underbrace` 在表达式的上、下方给出一水平的大括号。

```latex
$\underbrace{a+b+\cdots+z}_{26}$
```

效果如下：

> $\underbrace{a+b+\cdots+z}_{26}$



### 向量

向量（Vectors）通常用上方有小箭头（arrow symbols）的变量表示。这可由`\vec` 得到。另两个命令`\overrightarrow` 和`\overleftarrow`在定义从A 到B 的向量时非常有用。

```latex
$\vec a\quad\overrightarrow{AB}$
```

效果如下：

> $\vec a\quad\overrightarrow{AB}$



### 分数

分数（fraction）使用`\frac{...}{...}` 排版。一般来说，1/2 这种形式更受欢迎，因为对于少量的分式，它看起来更好些。

```latex
$1\frac{1}{2}$~hours
$\frac{x^{2}}{k+1}$ \qquad
$x^{\frac{2}{k+1}}$ \qquad
$x^{1/2}$
```

效果如下：

> $1\frac{1}{2}$ $~hours$ $\qquad$ $\frac{x^{2}}{k+1}$ $\qquad$ $x^{\frac{2}{k+1}}$ $\qquad$ $x^{1/2}$



### 积分 求和 乘积

积分运算符（integral operator）用`\int` 来生成。求和运算符（sum operator）由`\sum` 生成。乘积运算符（product operator）由`\prod` 生成。上限和下限用`^` 和`_`来生成，类似于上标和下标。

```latex
$\sum_{i=1}^{n}$ \qquad
$\int_{0}^{frac{\pi}{2}}$ \qquad
$\prod_\epsilon$
```

效果如下：

> $\sum_{i=1}^{n}$ $\qquad$$\int_{0}^{frac{\pi}{2}}$ $\qquad$ $\prod_\epsilon$



### 常用符号表示方法

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0xpQm8wMTEwMTA5MjE=,size_16,color_FFFFFF,t_70.png)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/2.GIF)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/3.GIF)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/4.GIF)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/5.GIF)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/6.GIF)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/7.GIF)

