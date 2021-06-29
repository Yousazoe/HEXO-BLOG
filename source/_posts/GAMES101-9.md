---
title: Texture Mapping cont
comment: false
tags:
  - Computer Graphics
  - Shading
categories: 现代图形学入门 (GAMES101-Introduction to Computer Graphics)
abbrlink: 870f1283
mathjax: true
date: 2021-04-15 16:03:17
type:
banner_img:
index_img:
translate_title:
top:
---

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/Ey3xWthWgAUCH5l.jpeg)

<div align=center>
  <font size="3">
    <i>
      <a href="https://twitter.com/Abbot6611">Twitter@Abbot6611</a>
    </i>
  </font>
</div>



### 引言

GAMES101 现代图形学入门是由闫令琪老师教授。今天我们讲着色部分说完，主要是关于纹理的应用，包括重心坐标、双线性插值、Mipmap以及三线性插值。

<!--more-->



### Barycentric Coordinates

#### Interpolation Across Triangles

**Why do we want to interpolate?**

+ Specify values at vertices
+ Obtain smoothly varying values across triangles

**What do we want to interpolate?**

+ Texture coordinates, colors, normal vectors, … 

**How do we interpolate?**

+ Barycentric coordinates



首先我们为什么要在三角形内部插值？上节课中我们有很多操作是在三角形顶点上完成或计算，然后三角形内部我们希望得到一个平滑的过渡，所以当我知道顶点的属性时可以知道三角形内部任何一点的值。

那我们插值什么内容呢？定义在三角形的顶点可以有不同的属性，比如纹理映射中定义顶点映射到纹理的位置，进而插值出三角形内部的纹理。除此之外还可以定义其他属性并插值：颜色、法线......可以看出我们可以对三角形顶点上任意的属性进行插值，事实也是如此。

最后我们怎么做插值？引入一个重心坐标的概念！



#### Barycentric Coordinates

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210415164304622.png)



重心坐标定义在三角形上。如果有一个三角形$\triangle ABC$，那么重心坐标告诉我们的事情是在这个三角形$\triangle ABC$所形成的平面内任何一个点$(x,y)$都可以表示成这三个顶点$ABC$的线性组合。需要注意的是如果这个点在三角形内，还需要满足另外一个条件：$\alpha \space \beta \space \gamma$ 必须是非负的。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210415165144806.png)



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210415165335139.png)



从重心坐标的定义就可以知道$A、B、C$的坐标，如果我要求任何一个点它的重心坐标是多少呢？这里给出另外一套定义，这个点的重心坐标其实是可以通过面积比求出来的。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210415170749974.png)



从这个定义我们可以快速得到一个非常特殊的点它的重心坐标，这个点就是三角形自己的重心。三角形的重心有一个非常好的性质，当它分别与$A、B、C$连线后三角形面积被均等分为三份等面积的三角形。

对于任意一个点我们可以用面积来计算，这里列出了给定坐标如何算出任意点的$\alpha \space \beta \space \gamma$表达式：



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210415171057242.png)



#### Using Barycentric Coordinates

Linearly interpolate values at vertices

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210415171446405.png)



<center>{% btn https://sites.cs.ucsb.edu/~lingqi/teaching/resources/GAMES101_Lecture_08.pdf,  GAMES101_Lecture_08, fas fa-download %}</center>

如果大家读OpenGL的一些文章，可能会涉及重心坐标虽然不错，但在投影变换下是不能保证重心坐标不变的。假如图中的是一个空间中的三角形，我可以算出对应的重心坐标，但如果我投影到某一个平面上去，三角形的形状会发生变化，从投影后的三角形算点的重心坐标会发现得到不一样的重心坐标。

这也告诉我们如果要插值三维空间中的属性，我们就应该取三维空间中的坐标计算重心坐标，然后再做插值对应到二维的结果去而不是在投影之后的三角形内做，这一点主要体现在光栅化中的深度中。



### Applying Textures

#### Simple Texture Mapping: Diffuse Color

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210415173227399.png)



我们之前提到Shader的时候已经说了这个事情，屏幕上的任何一个采样点不管是像素还是MSAA来代表一个采样点，它肯定有一个位置，那么我们就能插值出它的纹理坐标，也就相当于把图贴在物体上。



### Texture Magnification

#### Texture Magnification - Easy Case

Generally don’t want this — insufficient texture resolution

A pixel on a texture — a **texel** (纹理元素、纹素)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210416181200609.png)



第一个问题我们称为纹理的放大，假如我们有一个三维场景渲染出来，然后墙上有一副贴画。现在问题是假如我们定义渲染出来的分辨率是4K，但我们的纹理只有256*256该怎么办？墙的分辨率非常高，任意一个点查纹理会查到非整数的值，纹理太小就会被拉大，就会看到图上的现象。

在游戏开发中，开发者会避免在重要的地方用很低分辨率的纹理，但这种情况在普遍意义上会发生的。对于墙上任何一个像素都可以找到纹理上的坐标，不是整数我们就四舍五入成整数，这样的话在一定范围内我们查找的是一个相同的纹理上的像素，也被称为 **texel**。



#### Bilinear Interpolation

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210416181349733.png)



我们的高分辨率的屏幕的一个像素映射到了一个非整数的的位置，而我们看到的4*4的格子是 **texel**。我想知道，纹理在这个红点处它的值是多少？一个最简单的办法就是找离它最近的点，形成一块一块的。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210416181421957.png)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210416181447153.png)

 

我们换一种方法，找它临近的这么四个点，定义水平距离`s`和竖直距离`t`范围为0～1，因为两个**texel**之间距离为1。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210416181528346.png)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210416181614064.png)



下一步我们定义一个操作：线性插值。插值$v_0$和$v_1$，当$x=0$时 $lerp=v_0$；当$x=1$时 $lerp=v_1$。我们不用关心具体线性插值的公式，直接为$u_0、u_1$插值，最后再做一次竖直的插值得到红点。

那么现在这个点就综合了四个点的颜色，靠近哪个点相应就更相似，如果红点在正中央，那么它应该是这四个点的平均值。通过水平和竖直的插值，我就可以在四个点围成的区域内得到一个平滑的过渡，所以这是一个不错的做法，而这个方法被称为“双线性插值”。

有人会问方向可以不可以反过来？当然，先水平后竖直也是一样的，没有什么问题。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210416181644010.png)



#### Texture Magnification - Easy Case

Bilinear interpolation usually gives pretty good results at reasonable costs

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210416181200609.png)



我们有一个很小的图，然后我要把它放大查询它的任何一个非整型位置上的值是多少，我希望它平滑过渡。所以我们找最近的四个点做一个双线性插值就可以得到平滑过渡的结果。这里中间这幅图就是大家看到的双线性插值的结果，而双线性插值可以看到效果挺不错的，比之前的什么也不考虑直接四舍五入为整型，很多像素被映射到同一个texel要好。

当然双线性插值也有它的问题，它的质量还是差一些，比如右边的Bicubic双向三次插值取周围邻近的16个点做竖直和水平的插值，只不过做的是一个三次而不是线性的插值。Bicubic的运算量更大，带来得结果就越好。



#### Point Sampling Textures — Problem

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/屏幕快照 2021-04-18 下午1.17.38.png)



大家看这么一个平面，往远处延伸可以看到地平线，该平面贴了一个格子的贴图，从某个角度看近处格子挺大远处格子挺小，也就是透视投影。如果我们还照之前的操作简单的应用纹理，会得到右图这样看上去非常不对的东西，可以看到远处的摩尔纹以及近处的锯齿，我们又遇到了走样问题，从近处的勉强能看到近处的越来越差。



#### Screen Pixel “Footprint” in Texture

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210419090029471.png)



一个像素来说它覆盖的纹理上的区域其实相对较小，在远处则覆盖了很大一片纹理，这告诉我们屏幕上的这些像素它们覆盖纹理区域大小是各不相同的。对于一个像素它覆盖纹理区域小，那我用像素中心查询一下它的值可以近似；可如果像刚才接近地平线的像素覆盖了纹理上的很大一块区域，再用中心点如何代表这么大一片区域呢？我们不能去这么简单的用像素中心去采样。



#### Will Supersampling Do Antialiasing?

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210419090123626.png)



之前我们解决锯齿引入了MSAA，一个像素我用更多的样本感知变换的函数。如果右图每一个像素我用512个采样点就可以得到一个不错的结果。超采样可以得到一个不错的结果，但很多采样点会让算法变得很慢。





#### Antialiasing — Supersampling？

**Will supersampling work?**

+ Yes, high quality, but costly
+ When highly minified, many texels in pixel footprint
+ Signal frequency too large in a pixel
+ Need even higher sampling frequency

Let’s understand this problem in another way
+ What if we don’t sample?
+ Just need to **get the average value within a range**!



我们遇到的是一个走样的问题，走样就是信号变化过快，我们的采样速度跟不上它。在这个纹理过大问题上一个像素有着非常高频的信息，我希望把像素内的值重构出来，那我应该要一个更高频的采样方法。

这里提供一个完全不一样的思路，采样会引起走样，那我们不采样会怎样？



#### Point Query vs. (Avg.) Range Query

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210419090453080.png)



这是数据结构和计算几何中的点查询问题和范围查询问题。说白了就是给你一幅图上面任何一个区域能不能快速告诉我平均值是多少，这就是我们要的结果。



#### Different Pixels -> Different-Sized Footprints

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210419094217815.png)



我们以实际渲染的这幅图为例，比如我想渲染这幅图，窗台这块离的比较近一个像素在纹理上覆盖区域相对较小；正对的墙面离的较远那里的像素在纹理上覆盖的区域非常大，不同的像素在纹理上覆盖着不同的大小，所以范围查询应该查询任意不同的大小。



### Mipmap

Allowing (**fast, approx., square**) range queries

#### Mipmap (L. Williams 83)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210419093424110.png)



这里我们引入Mipmap，可以让我们快速、近似地做方形范围查询。对应到图中Mipmap就是由一幅图生成一系列图，比如原始的128\*128的纹理我们称为第0层纹理；第1层我们把分辨率缩小一半重新表示成64\*64的一幅图，可以看到不同的像素被拉大了，分辨率变低；以此类推做到最后一个有$log_2{128}$层。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210419093504382.png)



对应到计算机视觉Mipmap也被称为图像金字塔。我们原本有一张图占据了一定的存储量，那我们生成了那么多其他的一些图，总共我们引入多大的额外存储量？假设本来的图为1，那么就是$1+\frac{1}{4}+\frac{1}{16}+\frac{1}{64}......=\frac{4}{3}$，也就是说我只多了$\frac{1}{3}$的存储量。







#### Computing Mipmap Level D

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210419093555234.png)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210419093628667.png)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210419101249276.png)





#### Visualization of Mipmap Level

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210419093745340.png)



如果对每个像素都算它会投影纹理上对应多大的区域，然后替换为Mipmap的层数做一个可视化，如上图所示。但我们可以发现，这个变换不怎么连续，层数本身是离散的。



#### Trilinear Interpolation

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210419093823618.png)



我们同样可以用插值来解决这个问题。比如1.8层先找第1层和第2层，然后这两层内部分别用这个双线性插值把对应的查询做出来，之后把插值的结果合在一块就可以在层与层之间做一个插值。

这个过程是三线性插值，现在我可以计算离散的Mipmap层，并且不管是整数还是非整数在任意层查询它的值。在纹理内部，我都可以双线性插值出来一个平滑过渡的值，层与层之间也可以插值出来连续的值，这样一来就没有任何死角，对任何查询区域都可以用三线性插值做一次查询就可以得到这个区域覆盖的面积平均。



#### Visualization of Mipmap Level

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210419093905649.png)



三线性插值得到的结果如上图，有了过渡的效果，不同区域有了连续变化的结果。



#### Mipmap Limitations

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210419093950544.png)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210419094021038.png)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210419094057813.png)



假设512倍的超采样能够给我们准确的结果，Mipmap到了远处细节会全部被糊掉，这种过分模糊的情况我们称为Overblur。这是因为插值本身是一种近似而非一个准确的结果，查询也是不够准确的近似。



#### Anisotropic Filtering

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210419105448654.png)



有一个办法可以部分解决三线性插值所产生的问题：各向异性过滤，效果比三线性插值要好，远处也不再糊掉了。



#### Irregular Pixel Footprint in Texture

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210419105515859.png)



屏幕上的任何一个像素映射到纹理上可不一定是规律的形状，很有可能出现会出现奇怪的情况，而这种情况下还近似为正方形显然不妥。如果我们引入各向异性过滤，对应这种问题就可以得到一个完美的解决。



#### Anisotropic Filtering

**Ripmaps and summed area tables**

+ Can look up axis-aligned rectangular zones
+ Diagonal footprints still a problem

**EWA filtering**

+ Use multiple lookups
+ Weighted average
+ Mipmap hierarchy still helps
+ Can handle irregular footprints



不同的长宽比是Mipmap本身所缺失的，只有对角线的1:1长宽比，换言之多出来的是不均匀的水平和竖直的压缩。EWA过滤通过讲不规则形状拆分为不同的圆形覆盖，多次查询花费也就越高，又回到了质量越好代价越高的问题。







<br/>

<center>{% btn https://sites.cs.ucsb.edu/~lingqi/teaching/resources/GAMES101_Lecture_09.pdf,  GAMES101_Lecture_09, fas fa-download %}</center>

