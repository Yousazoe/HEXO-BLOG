---
title: Triangles
comment: false
tags:
  - Computer Graphics
  - Rasterization
categories: 现代图形学入门 (GAMES101-Introduction to Computer Graphics)
abbrlink: d3e5abd5
date: 2021-04-01 18:58:41
type:
banner_img:
index_img:
translate_title:
top:
mathjax: true
---





![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/Ex1FWvNWEAMtysd-20210402083825006.jpeg)

<div align=center>
  <font size="3">
    <i>
      <a href="https://twitter.com/MVC_discord">Twitter@MVC_discord</a>
    </i>
  </font>
</div>



### 引言

GAMES101现代图形学入门是由闫令琪老师教授。今天我们来讲三角形的光栅化，可能会提及遮挡或可视性。

<!--more-->





### Finishing up Viewing

#### Perspective Projection

**What’s near plane’s l, r, b, t then?**

+ If explicitly specified, good

+ Sometimes people prefer: 

  **vertical field-of-view** (fovY) and **aspect ratio** (assume symmetry i.e. l = -r, b = -t)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-04-01%20%E4%B8%8B%E5%8D%887.18.29.png)



我们如何定义视锥呢？我们从摄像机出发看向某个区域，如果我们看到的是近平面，那么我们可以给近平面定义一个宽度和高度，那么就可以定义宽高比`assume symmetry`。

还有一个可视角度`aspect ratio`，在图中表示为从相机连到屏幕的上下边，两边夹角就是垂直可视角度。广角相机就是可视角度比较大，适合拍近景；反之开口越小越像正交投影，远景成像更明显。





**How to convert from fovY and aspect to l, r, b, t?**

+ Trivial

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210401192129740.png)







#### What’s after MVP?

+ **M**odel transformation (placing objects)
+ **V**iew transformation (placing camera)
+ **P**rojection transformation
  + Orthographic projection (cuboid to “canonical” cube $[-1, 1]^3$)
  + Perspective projection (frustum to “canonical” cube)
+ Canonical cube to ?



#### Canonical Cube to Screen

**What is a screen?**

+ An array of pixels
+ Size of the array: resolution
+ A typical kind of raster display

**Raster == screen in German**

+ Rasterize == drawing onto the screen

**Pixel (FYI, short for “picture element”)**

+ For now: A pixel is a little square with uniform color
+ Color is a mixture of (red, green, blue)



在得到这样一个$[-1,1]^3$的立方体后，我们该画在哪儿呢？当然是画在屏幕上，对于图形学而言我们抽象的认为是一个二维数组，数组中的每一个元素是像素，比如平时大家电脑的分辨率是1920*1080，分辨率就是屏幕的大小1080p。

屏幕是一个典型的光栅成像设备，Raster是德语中的“屏幕”。光栅化就是把东西画在屏幕的过程，把名词换成动词。

多提一句，像素（Pixel）名字的由来是“picture element”，在这门课我们认为就是一个一个小方块，内部的颜色不会有变化，是最小的单位。





**Defining the screen space**

+ Slightly different from the “tiger book”

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210402082039954.png)



+ Pixels’ indices are in the form of (x, y), where both x and y are integers
+ Pixels’ indices are from (0, 0) to (width - 1, height - 1)
+ Pixel (x, y) is centered at (x + 0.5, y + 0.5)
+ The screen covers range (0, 0) to (width, height)



我们把屏幕的空间也定义一下。屏幕空间就是在屏幕中建立一个坐标系，虎书中有一套定义方案，不过我们采用自己的定义。上图的左下角是原点，从这个原点出发延伸出X和Y。

有一些约定俗成的规定，首先我们定义像素它的坐标/下标/位置写成(x,y)形式，并且使用整数来表述它；如果屏幕的宽高分别为width和height，那么我们认为所有像素就是从(0, 0)到(width - 1, height - 1)这么多可行的坐标；虽然我们用整数坐标(x, y)定义像素，但其实像素中心在(x + 0.5, y + 0.5)。





+ Irrelevant to z
+ Transform in xy plane: $[-1, 1]^2$ to $[0, width] x [0, height]$
+ Viewport transform matrix:

$M_{viewprt}=\begin{pmatrix}\frac{width}{2} & 0 & 0 & \frac{width}{2} \\\\ 0 & \frac{height}{2} & 0 & \frac{height}{2} \\\\ 0 & 0 & 1 & 0 \\\\ 0 & 0 & 0 & 1\end{pmatrix}$



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210402083530408.png)



现在我们要做的就是把右边的$[-1,1]^3$映射到左边的屏幕中。这里有一个问题是右边是一个三维坐标，映射到屏幕上如何处理它的z坐标？一个简单的方法是暂时不管它，自然而然之后会有它的用处，只盯着x、y来看就简单很多。

首先我们将$[-1,1]^3$缩放到$[width,height]$范围中，对应上面的矩阵中是左上角的3*3。缩放后中心还在原中心点上，而我们需要将其平移至左下角的原点，这个变换也被称为视口变换。





### Rasterization

#### Next: Rasterizing Triangles into Pixels

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210402085247459.png)



《少年派的奇幻漂流》大家都知道老虎是假的，但做的栩栩如生，这就是图形学的贡献。可以看到老虎上面有各种各样的多边形，这些多边形经过变换和各种各样的操作之后会形成在屏幕空间中的多边形，但这不够，我们要把多边形进一步打碎，打成像素，显示在一个个像素上告诉我每一个像素的值都应该是什么，这一步过程我们称之为光栅化。



#### Drawing Machines

##### CNC Sharpie Drawing Machine

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210402091742617.png)





##### Laser Cutters

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210402091843642.png)





#### Different Raster Displays

咱们来介绍各种各样不同的光栅显示设备。

##### Oscilloscope

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210402092345238.png)



上图是示波器，它在上面可以形成各种各样的曲线，早期很多电脑显示器都是这样。



##### Cathode Ray Tube

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210402092733339.png)



示波器的成像原理和我们早期显示器的成像原理一模一样：阴极射线管。左边产生很多的电子，经过加速发生偏转打在屏幕不同的位置上，如果这个过程进行的足够快，那么我们不会看到电子一个一个打在屏幕上，但这种CRT屏幕非常伤眼睛。



##### Television - Raster Display CRT

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404131942213.png)



关于CRT显示器有一个有意思的事情，早期的电视和电脑显示器，它们是如何把一个一个的点打在屏幕上从而形成一整个完整的画面呢？其实很简单，它们是通过一种扫描的方式控制电子打到的位置，从屏幕左上角画一道线，换一行接着画水平线循环往复......当这些线足够密集的时候它就可以覆盖整个屏幕了，当然它有个先后顺序，在右边的示意图上扫描线从上往下画过来。

还有一个有意思的现象，人们发现为了让画线成像快点每张图可以只画一半，隔一行画一条线，这个技术被称为隔行扫描技术，该技术到现在仍在视频压缩中起到一些作用。早期分两次画节约带宽保持低时延，并且人眼的视觉停留效应不会察觉只画了一半，每次都是完整的画面。



##### Frame Buffer: Memory for a Raster Display

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404135235083.png)



现在的一些显示设备其实我们只需要知道它们的原理就可以了。显示器通过显卡或者内存的一块区域（显存）映射到屏幕上，生成不同的图像存在显存中。





##### Flat Panel Displays

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404151047802.png)



现在的主要显示设备是平板显示设备，主力是LCD，还包括OLED等等。图中是两个不同的例子，上图是计算器，分辨率很低，可以看到一个一个的像素；下图是手机，其显示器分辨率就非常高了。到了现在的发展，人们发明了一些非常高分辨率的显示设备，高到屏幕分辨率已经超出视网膜的分辨率，这种屏幕我们称为“视网膜屏幕”。





##### LCD (Liquid Crystal Display) Pixel

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404160446849.png)

+ Principle: block or transmit light by twisting polarization
+ Illumination from backlight (e.g. fluorescent or LED)
+ Intermediate intensity levels by partial twist



LCD就是通常的液晶显示器，顾名思义就是利用液晶的原理控制一个像素的显示。

示意图中液晶会通过自己的不同排布影响光的极化，也就是光的偏振方向。大家可以看到液晶显示器的结构，它有两个不同的光栅以不同的方式排布（左边与右边），光经过一个光栅只会留下光栅规定方向上的振动能量，与光栅振动方向一致。例如下图光栅是竖直分布的，光试图通过左边的水平振动，但因为自己是竖直光所以无效。液晶显示的原理就是通过液晶的扭曲，把光的振动方向渐渐调整过来。大家可以看到上图光原本也是竖直的，经过液晶的扭曲后扭成了水平的，然后它就可以从水平的光栅出去了。





##### LED Array Display

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404161601285.png)



我们刚才提到LCD液晶显示器，还有一种广泛使用的显示设备叫发光二极管LED（Light emitting diode）。上图是一块板，上面有各种各样阵列的发光二极管，预定好发出红光、蓝光等等。





##### Electrophoretic (Electronic Ink) Display

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404162742612.png)



还有一种基于电子墨水的显示设备，如果大家买过亚马逊的Kindle就会知道它的原理。它有好多黑的、白的墨水，经过不同电压等不同的情况会发生翻转，进而控制不同的像素显示。当然它有一个严重的问题，它的刷新率很低，也就是说你要想改变一次要花费一定的时间，而且是肉眼可见的时间。



#### Drawing to Raster Displays

##### Polygon Meshes

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210402085247459.png)



我们已经提到怎么把一系列三维空间中的多边形变换到屏幕空间上，下一步实际上把多边形拆成不同的像素。



##### Triangle Meshes

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404164113500.png)



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404164433054.png)



##### Triangles - Fundamental Shape Primitives

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404164614690.png)

Why triangles? 

**Most basic polygon**

+ Break up other polygons

**Unique properties**

+ Guaranteed to be planar
+ Well-defined interior
+ Well-defined method for interpolating values at vertices over triangle (barycentric interpolation)



即使很复杂的图形其实也是由不同的三角形构成的，也就是说三角形表现能力很强，在图形学中得到广泛的应用。

它由很多独特的性质：

+ 最基础的图形，任何不同的多边形都可以把它拆成三角形
+ 三角形的三个顶点可以确定一个平面
+ 三角形的内外定义非常清晰





##### What Pixel Values Approximate a Triangle?

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404165318943.png)



既然三角形有很大优势，那么我们就盯着三角形来看。现在图中我们知道三角形的三个顶点，需要把这个三角形变成真正的像素。



#### A Simple Approach: Sampling

##### Sampling a Function

Evaluating a function at a point is sampling. 

We can **discretize** a function by sampling. 

```c++
for (int x = 0; x < xmax; ++x) 
	output[x] = f(x);
```

 Sampling is a core idea in graphics. 

We sample time (1D), area (2D), direction (2D), volume (3D) …



一种简单的办法是采样，采样就是给出一个连续的函数，我在不同的地方去问这个函数的值是多少，是一个离散化的过程。在图形学中采样是一个非常重要的概念，我们会涉及到不同的采样，这里我们涉及到的是利用像素中心对屏幕空间进行的采样。



##### Rasterization As 2D Sampling

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404170004561.png)







##### Sample If Each Pixel Center Is Inside Triangle

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404170050639.png)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404170118282.png)







##### Define Binary Function

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404171528836.png)



给定一个三角形和屏幕空间任何一个点的坐标，我们要确定它是否在三角形内。结合之前的示意图具体而言就是在不同的像素中心，我们要确定函数的值是1还是0。



##### Rasterization = Sampling A 2D Indicator Function

```c++
for (int x = 0; x < xmax; ++x)
	for (int y = 0; y < ymax; ++y)
		image[x][y] = inside(tri,x + 0.5,y + 0.5); 
```



##### Recall: Sample Locations

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404172244593.png)

![](/Users/apple/Library/Application Support/typora-user-images/image-20210404172304504.png)



##### Inside? Recall: Three Cross Products!

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404172221902.png)



在向量叉积中我们提到如何判断左右侧。我们有一个三角形$\bigtriangleup {P_0P_1P_2}$，判断点$Q$是否在三角形内。例如我们可以通过$\vec{P_1P_2} \times \vec{P_1Q}$，根据右手定则叉乘方向向屏幕外侧，所以$Q$在$P_1P_2$的左侧；同理$\vec{P_0P_1} \times \vec{P_0Q}$，得到的结果仍然在屏幕外侧，$Q$在$P_0P_1$的左侧；在我们判断$\vec{P_2P_0} \times \vec{P_2Q}$时，得到的结果是一个向里的向量，所以$Q$在$P_2P_0$的右侧，它不在三角形内部。



##### Edge Cases (Literally)

Is this sample point covered by triangle 1, triangle 2, or both?

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404172147529.png)



这里有人会问，如果有一点碰巧在三角形的边界上该怎么办？图形学里面我们经常会遇到这个问题，但对于这种问题要么不做处理要么特殊处理，在一些图形学的API比如OpneGL或DirectX中，它们有着非常严格的定义。



##### Checking All Pixels on the Screen?

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404172124336.png)



考虑一个三角形的光栅化，我就要把所有的像素都走一遍呢？没必要，一个三角形只能覆盖一定的区域，比如上图三角形只能覆盖到蓝色的区域，左边第一列的像素不在蓝色的区域，它就更不可能碰到三角形，所以我对于这些像素根本就不用看，三角形根本不可能填充到这些像素上。

对于这个蓝色区域我们管它叫三角形的包围盒，更严格意义上是一个轴向的包围盒，范围就是三角形的三个顶点的$x_{min}、x_{max}、y_{min}、y_{max}$区域。



##### Incremental Triangle Traversal (Faster?)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404172059864.png)



光栅化还有许多奇奇怪怪的加速方法，比如我可以对三角形覆盖区域每一行都找最左和最右，相当于每一行都有一个包围盒的概念，这样一个像素都不会多考虑。



#### Rasterization on Real Displays

##### Real LCD Screen Pixels (Closeup)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404170345850.png)



上图是两个手机屏幕显示同一个画面，大家可以看到左边是红绿蓝线性排列，右边则是形成了Bayer图案，这种分布方法可以让红绿蓝均匀的分布在空间上。如果仔细观察还可以发现右图绿色图案的分布要比红蓝多，这是因为人眼对绿色最为敏感，所以绿色多一些像素是有好处的。



##### Aside: What About Other Display Methods?

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404170448423.png)



彩色打印机上我们看到更复杂的图案，打印过程更多关注一些如何最省墨以及之后在颜色章节会说这是一个减色系统，往上加的颜色越多，最后得到的结果越黑。





##### Assume Display Pixels Emit Square of Light

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404170843569.png)







##### So, If We Send the Display the Sampled Signal

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404170804803.png)



通过这节课的学习，我们现在可以把像素填成三角形的颜色如上图所示。



##### The Display Physically Emits This Signal

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404170742835.png)



##### Compare: The Continuous Triangle Function

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404170724491.png)





##### What’s Wrong With This Picture? 

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404170704755.png)



虽然它基本保留了三角形的形状，但锯齿非常明显，它也是光栅化图形学里需要解决的一个严重的问题。像素本身有一定的大小，并且我们的采样率对于信号不够高，所以产生了走样问题。



##### Aliasing (Jaggies)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404170632049.png)



走样在光栅化图形学中表现出来就是锯齿。下一步自然而然的一步工作就是抗锯齿或者反走样。





<br/>

<center>{% btn https://sites.cs.ucsb.edu/~lingqi/teaching/resources/GAMES101_Lecture_05.pdf,  GAMES101_Lecture_05, fas fa-download %}</center>

