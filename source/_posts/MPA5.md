---
title: 开始画像素画#5
abbrlink: 9b57cb2b
date: 2020-11-09 19:42:26
tags:
  - Art
  - Pixel
  - Aseprite
  - Reprint
categories: 开始画像素画 (Making Pixel Art)
index_img:
banner_img: https://tva1.sinaimg.cn/large/0081Kckwgy1glhuwy9e3aj30u00gwt9s.jpg
comment:
sticky:
---



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/008eGmZEly1gn5zjv505rj31hc0u0427.jpg)

### 引言

这是来自佩德罗・梅代鲁斯（Pedro Medeiros，[@saint11](https://twitter.com/saint11)）授权的一系列像素美术教程，转载自[风农](https://indienova.com/u/fengnong)的翻译整理。本文将讲解关于抗锯齿与色带。

<!--more-->



佩德罗・梅代鲁斯最为知名的作品莫过于《塞莱斯特山（蔚蓝，Celeste）》，不过他持续在网络上发布的像素美术教程也同样相当知名，indienova 已经做了完整转载。

这部分教程就是经过风农翻译整理的另一部分内容：《开始画像素画（Making Pixel Art）》。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1glhuxvnuszj30u008c74z.jpg)



系列第 5 节。

这节稍微复杂点，可能比其他的几篇更进阶点。

如果不能一下看懂也没关系，很多都是我的个人观点，而且抗锯齿和色带问题在像素画社区里观点很多。

开始我不会讲软件，而是重点讲解这些概念，在接下来部分我会推荐一些练习。

### 什么是锯齿，为什么大家不喜欢

在像素画里的 anti-alias 的 alias 我们一般说的是锯齿，或者说台阶效果。一种在低分辨下很容易注意到的效果。这个效果本身没有好坏，有时甚至是某种故意追求的风格，但有时候也会让画面很难看懂。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1glhuxu5ffrj30dp07fjr5.jpg)

上面的例子里能看到，第一个图有很多尖锐的边，尤其是火焰周围。有些区域甚至很难理解在发生什么。

这是因为像素画是事物的低分辨率表现。如果你这样想，就可以区分出“有意的线”和实际像素。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1glhuxs0u51j30fi07kwe9.jpg)

基本上整个像素画流程就包括了把线转化到低分辨率画布上，并**决定哪些像素要填充**。有些像素明显在线的范围内，所以要填充。有些明显在外面，就不用填充。问题是那些刚刚贴到线上或者一半在线上的，才是问题所在。抗锯齿就是用中间色来填充这些像素，来创造一种柔和过渡的错觉。

### 如何画抗锯齿

简单讲: 有时候画的线不能完全符合像素网格，就需要使用中间色来让它看起来好点。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1glhuxst7nsj306a09r741.jpg)

这个问题没有单一的解决方法，你可以用多种方法表现“想要的线”，取决于你的分辨率，画风，以及可用的颜色有多少。

使用中间混合颜色的像素，在远处看算是半个像素。你可以利用这个来把边角软化一点。

一个画反锯齿的好方法是搜索任何比 `1-1` 长的台阶图案：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1glhuxyf0g9j30rp04j0qh.jpg)



找到 `2` 个像素或者更长的台阶之后，可以开始柔化他们，通过在台阶末尾添加半色的像素。要添加的像素数量取决于台阶的长度，以及可用的颜色。有时候这样会让物体扩张太多，这样的话你可以用半色的像素替代一个（有时更多）原来图案里的像素。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1glhuxsa2xaj30rg04c0jq.jpg)

改变颜色或者饱和度影响不大，只要你是正确的在插值颜色的亮度。这在使用非常小的调色盘时很有用。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1glhuxuo4saj30ak0aiq2p.jpg)



在简单的斜坡上画这些就已经很复杂了，在真正的画上面复杂度更是几何级增加。小的画布上画抗锯齿会影响到其他东西，带来很多副作用。我们讲几个常见的。



**太多抗锯齿**

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1glhuxv3quwj30f00e7jr5.jpg)



最常见的问题就是过度的做抗锯齿，导致所有东西都很模糊。通过使用更少的半色，更少的台阶，以及不要在 `45` 度的线（`1-1` 的台阶）或者直线上用抗锯齿，来避免这种情况。



**抗锯齿太短**

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1glhuxtkq1xj30oa0ae3yd.jpg)



这是不太常见的情况，而且可能是有意为之，尤其是在受限的调色盘上，不过有时候抗锯齿的半色像素比台阶本身的长度短太多。记住一个长的台阶应该有个相对长的抗锯齿半色条纹。



**半色亮度错误**

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1glhuxwdze1j30gl0gn742.jpg)



之前也提到了，半色可以用不同的颜色，只要亮度感觉是两种要混合颜色的桥梁就可以。这里出的问题就是没有考虑这一点，相对于背景把半色画的太暗，或者太亮。

有时候，当背景比物体还亮，这可以用来模拟阴影，也算是有用。但记住这种情况下其实是在画明暗而不是画抗锯齿。



**色带**

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1glhuxx4ggpj30cu0bi0ni.jpg)



色带问题是当我们画了几个颜色完全不同的色带时出现的。这通常是个问题，会让物体看起来很平，有时候模糊。

在这个球体的例子里，我把色带压缩到很小的区域。我把这种方法称为色带压缩，之前的阴影教程了也提到了。

斜坡上就没办法这么压缩了。所以我旋转了渐变的方向。这也可以画出不错的抗锯齿，原来的是方向画错了，导致的色带问题。要总是注意这点，水平的斜坡应该加水平的抗锯齿，垂直的斜坡加垂直的抗锯齿。



### 接下来

现在我建议你去实际的试试我这里讲的东西。你可以先从简单的 `2-1` 黑色斜坡开始，再试试圆圈。保持低颜色数，画布不要超过 `48` 乘 `48`。

在这之后，你可以试试更多颜色，真实的画些东西。还是从简单的开始，像是球体，苹果，之后再到复杂的形状，比如人。

总是注意画面里画出的色带，或者可以改进的抗锯齿。记住每个像素都是个抉择，每个像素都应该让你的画更好，画的更可读。如果抗锯齿带来的效果弊大于利，就去掉它。