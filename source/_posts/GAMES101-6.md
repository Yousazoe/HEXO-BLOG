---
title: Antialiasing and Z-buffering
comment: false
tags:
  - Computer Graphics
  - Rasterization
categories: 现代图形学入门 (GAMES101-Introduction to Computer Graphics)
abbrlink: 874dc08b
mathjax: true
date: 2021-04-06 21:28:29
type:
banner_img:
index_img:
translate_title:
top:
---



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/EyRZ2j_XAAMMk-k.jpeg)

<div align=center>
  <font size="3">
    <i>
      <a href="https://twitter.com/MVC_discord">Twitter@MVC_discord</a>
    </i>
  </font>
</div>



### 引言

GAMES101 现代图形学入门是由闫令琪老师教授。今天我们要把光栅化内容讲完，主要包括反走样和深度缓冲。

<!--more-->



### Antialiasing

#### Recap: Testing in/out △ at pixels’ centers

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210406213421926.png)



上一节课我们提到说一个三角形自然是连续的信号或者函数定义在屏幕空间内，然后我们可以给定任何一个点测试是否在三角形内部，而对于像素来说，我们认为是均匀颜色的小方块，最后得出的就是上图的红点和白点结合。



#### Pixels are uniformly-colored squares

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404170742835.png)



然后我们把对应的像素涂成这样的颜色，红色代表被三角形覆盖，白色代表未被三角形覆盖，得到一个类似三角形的图案。



##### Compare: The Continuous Triangle Function

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404170724491.png)



与我们理想的三角形有较大差距，以锯齿效应最为明显。







##### Aliasing (Jaggies)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404170632049.png)



锯齿的学名叫走样，例如左图三角形的尖放大可以看到锯齿或走样的现象。



### Sampling is Ubiquitous in Computer Graphics

#### Rasterization = Sample 2D Positions

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404170050639.png)



首先我们之前提到采样在图形学中是一个广泛存在的做法，光栅化的过程就是在屏幕空间用一系列离散的点/像素中心进行在三角形函数上的采样。



#### Photograph = Sample Image Sensor Plane

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407081357027.png)



对于任何一个我们拍出来的照片，如果我们放大可以看到一个个格子，图像的分辨率则决定了像素的多少，所以到达感光平面的光学信息把它离散成一系列图像上的像素进行采样。



#### Video = Sample Time

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407081831869.png)



采样不止发生在不同的位置，还可以发生在不同的时间。视频动画就是一系列的图按照一定时间给放出来，就可以形成一个动画，实质上就是时间中的采样，因为我们没有见过任何连续意义上的动画。如果我们把动画拆开，动画是定义在一帧一帧上，每秒给大家放出24帧连在一起，上图我们可以很清楚看到球员离散的击球过程。



### Sampling Artifacts (Errors / Mistakes / Inaccuracies) in Computer Graphics

采样广泛存在，采样的问题也广泛存在。在图形学中一切错误、不准确、不希望看到的结果被称为**Artifacts**，中文翻译为瑕疵。



#### Jaggies (Staircase Pattern)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210404170632049.png)

This is also an example of “aliasing” – a sampling error.



采样的第一个问题是会产生锯齿，上图这些锯齿很想楼梯的形状。



#### Moiré Patterns in Imaging

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407082855389.png)



这两幅图表示的就是采样中产生的另一个问题：摩尔纹。假如把左图的奇数行和奇数列全部去掉并且重新对接在一起，显示还是原来的大小，就会出现右图的效果。在日常生活中也可以看到，比如手机去拍摄电脑屏幕就会出现这样的现象，会出现扭曲的纹路，这也是采样带来的问题。



#### Sampling Artifacts in Computer Graphics

**Artifacts due to sampling - “Aliasing”**

+ Jaggies – sampling in space
+ Moire – undersampling images
+ Wagon wheel effect – sampling in time
+ [Many more] … 



前两者是空间上采样的问题，车轮效应则是时间采样的问题。



**Behind the Aliasing Artifacts**

+ Signals are changing too fast (high frequency), but sampled too slowly



这些问题的本质上都是信号/函数的变化太快了，以至于采样速度跟不上它。







### Antialiasing Idea: Blurring (Pre-Filtering) Before Sampling

#### Rasterization: Point Sampling in Space

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407085117492.png)



之前走样问题的产生是因为我们用像素中心采样三角形，然后我们发现有些点完全在三角形内，一些完全在三角形外，所以这些点要么是红的要么是白的，画出来就会产生走样。



#### Rasterization: Antialiased Sampling

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407091544645.png)



那现在我们拿到三角形，先做一个模糊操作把它变成一个模糊的三角形，然后我再用这些像素的中心点采样，比如右边的三角形采样到模糊三角形的边界颜色变为粉红色。

通过对原始函数/信号做一个模糊/滤波再去采样，就可以解决锯齿这么一个问题，在实际应用时效果也不错。



#### Point Sampling vs Antialiasing

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407085848998.png)



左图有非常严重的锯齿问题，通过刚才的反走样方法先模糊再采样可以达到右图的效果。有人可能会问，那我能不能先采样再进行滤波呢？



#### Antialiasing vs Blurred Aliasing

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407085944753.png)



答案是不行。很明显右图比左图看上去真实很多，而左边就是先采样后滤波的效果，它还有一个名字叫“ Blurred Aliasing”，也就是走样之后的模糊。



#### But why?

1. Why undersampling introduces aliasing? 
2. Why pre-filtering then sampling can do antialiasing? 



Let’s dig into fundamental reasons

And look at how to implement antialiased rasterization



### Frequency Domain

#### Sines and Cosines

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407132350777.png)



没有什么比余弦和正弦更简单的了，可以看到唯一的区别就是两者的相位不太一样，左右平移了一些。



#### Frequencies

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407132655072.png)

通过调整$x$前面的系数$f$，我会得到各种不同的余弦波，它们的不同就在于频率$f$。根据$f$我可以定义余弦波变化的快慢，$f = 2$变化的明显比$f=1$要快，余弦波的周期就是$\frac{1}{f}$。



#### Fourier Transform

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407132849050.png)



微积分都会提到函数的展开，其中就有一个傅立叶级数展开：任何一个周期函数都可以把它写成一系列正弦和余弦函数的线性组合以及一个常数项。



#### Fourier Transform Decomposes A Signal Into Frequencies

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407133602837.png)



这说明傅立叶级数展开和傅立叶变换紧密相连，两个概念非常相似。给定任何一个函数$f(x)$都可以让它经过一个相当复杂的操作把它变为另外一个函数$F(\omega)$；我也可以把$F(\omega)$通过逆变换变回原来的函数$f(x)$。很简单，就是把函数变成另外一个并且把它变回来，这个变换就叫傅立叶变换和逆傅立叶变换。



#### Higher Frequencies Need Faster Sampling

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407134946180.png)



所谓傅立叶变换，其实就是把函数变成不同的频率的段，并且把这些不同频率的段显示出来。上图的示例有五个不同的函数从上倒下从$f_1(x)$到$f_5(x)$，频率从高到低从上到下，我们假设用完全相同间隔的采样方法进行采样，可以发现第一个函数采样出不同的点连起来可以大概原来的函数长什么样。第二、三、四和五也可以这么做，但到第三个函数已经发现不太对劲了，如果还这么采样并连接采样点会发现很难恢复函数，和之前的$f_1(x)$相差较多，到$f_5(x)$已经不能看了。

通过频率的分析，我们可以看出对于一个函数来说它有自己的频率，然后我们采样也应该有一定的频率（间隔），如果采样的频率跟不上变化的频率如$f_5(x)$，没办法把原始的信号给恢复出来。



#### Undersampling Creates Frequency Aliases

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407135714405.png)

+ High-frequency signal is insufficiently sampled: samples erroneously appear to be from a low-frequency signal 

+ Two frequencies that are indistinguishable at a given sampling rate are called “aliases”



我们来通过频率分析走样。图中是一个变化剧烈的蓝色函数，我们继续采样并连接起黑色曲线，可以发现采样得到的结果不太行。我们考虑如果有两个函数，那么这样的采样方法采样两者频率截然不同的函数/信号会得到完全相同的结果。

也就是说同样的采样方法采样两种不同频率的函数，得出来的结果我们无法区分它，那么就是走样的概念。



### Filtering = Getting rid of certain frequency contents

从频率上讲，所谓滤波就是把某个特定的频段删掉，对应的信号发生相应变化。



#### Visualizing Image Frequency Content

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407143604890.png)



傅立叶变换它可以把函数从时域变成频域，左边这幅图我们对它做一个傅立叶变换，虽然图像本身不带有任何时间的信息，但我们认为空间上不同的位置也算是时域，也就是从图像的空间变为了频率的空间。

那右边这幅图我们该如何去理解呢？中心我们定义为最低频的区域，周围定义为高频的区域，不同频率位置的信息通过亮度来表示。示例图像的大多数信息集中在低频段，因为中间比较亮，对于自然的图片基本都是这样。



#### Filter Out Low Frequencies Only (Edges)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407143902994.png)



相比上一幅图，这里低频信号被抹掉，留下的只有一些高频信号。通过逆傅立叶变换返回为图像，高频的东西表现了图像内容的边界，这种滤波被称为高通滤波，只有高频信号可以通过。

为什么高频信息对应图像的边界呢？我们发现边界就是发生突变的地方，比如说图像中衣服与背景之间剧烈的变化，蕴含着高频的信息。那么如果只显示高频信息，那么自然找到边界。



#### Filter Out High Frequencies (Blur)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407143936056.png)



和之前图对比只留下了低频的信息，把高频信息全部抹掉，然后把它变回图。我们得到了一张相对模糊的图，基本还能看清是个人，绝大部分信息再也看不见了。这里我们对信号应用了低通滤波器，只让低频率通过，高频率被筛选掉。



#### Filter Out Low and High Frequencies

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407154342082.png)



这次我们去掉了高频和低频，留下了某一次高频段的信息。我们可以提取到不是那么明显的边界特征，中间大面积相同的色块也因低频信息而被去掉。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407155219787.png)



如果我们继续把圈扩大，更高频的逆变换图像更像边界。所以这一块通过频率的分析，把不同的频率和信号的变化建立关系。





### Filtering = Convolution (= Averaging)

#### Convolution

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407155447179.png)



我们有一个以数组方式存储的一维信号，还有一个大小为3的滤波器，它类似于一个窗口左对齐于信号最左侧。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407155520089.png)



卷积操作就是移动窗口的过程中把窗口对应这三个数和窗口覆盖的三个数做一个点乘，得出的结果写回窗口的中心值。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407155551930.png)



这其实就是一个平均，原始的信号在任何一个位置取周围三个数求一个加权平均，得到的结果最后会得到新的平均信号。当然这不是数学上的定义，是图形学简化后的定义。



#### Convolution Theorem

Convolution in the spatial domain **is equal to multiplication in the frequency domain**, and vice versa 

**Option 1:**

+ Filter by convolution in the spatial domain 

**Option 2:**

+ Transform to frequency domain (Fourier transform)
+ Multiply by Fourier transform of convolution kernel
+ Transform back to spatial domain (inverse Fourier)



卷积有一个定理：时域上如果想对两个信号做卷积，对应到两个信号各自的频域上是两个信号频域的乘积。通过卷积定理我们可以知道如何做一个卷积，可以直接拿到一幅图然后用某一个卷积的滤波器做一个卷积操作；也可以拿这幅图先傅立叶变换变到频域上，把卷积的滤波器变到频域上，把两者相乘的到频域的结果再把它逆傅立叶变换变到时域上。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407155749846.png)



我们想对这幅图进行平均或者卷积操作，然后它是一个$3 \times 3$的窗口，任何像素都是它周围$3 \times 3$像素的平均，那得到的结果就是模糊了的图像。刚才也说了可以先做图像和滤波器的傅立叶变换到频域上相乘，最后再逆傅立叶变换变回图像。

整个过程很像低通滤波，对应的就是之前说过的模糊的图像，也证明了卷积的正确性。



#### Box Filter

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407155824797.png)



回过头来看滤波器，它是个$3 \times 3$的盒子。这里的$\frac{1}{9}$是为了经过卷积操作后图像整体的颜色不会跟以前发生太大变化做的归一化操作，否则卷积得到的是周围九个像素颜色之和，影响图像亮度。



#### Box Function = “Low Pass” Filter

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407155850504.png)



#### Wider Filter Kernel = Lower Frequencies

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407155924759.png)



如果这个盒子在时域上变大，那么频域该如何变化呢？对应在频域上反而变小了，比如之前为了模糊一张图我们用了$3 \times 3$的卷积核，我们得到一个模糊的结果。那么我们想象一下如果我们用$63 \times 63$这样大小的box，对任何像素我们都取那么大一块的像素的平均，得到的结果可想而知越来越模糊。



### Sampling = Repeating Frequency Contents

#### Sampling = Repeating Frequency Contents

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407163820667.png)



采样就是在重复一个原始信号的频谱，这就是为什么会产生走样现象。



#### Aliasing = Mixed Frequency Contents

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407163855767.png)



采样的不同的间隔会引起频谱以另外一个不同的间隔进行移动。采样不够快会导致原始信号复制粘贴中间的间隔非常小，意味着采样点之间的距离很大。走样在频率的角度上说就是频谱在复制粘贴的情况下发生了混合/混叠，这就是产生走样的原因。



#### How Can We Reduce Aliasing Error?

**Option 1: Increase sampling rate**

+ Essentially increasing the distance between replicas in the Fourier domain
+ Higher resolution displays, sensors, framebuffers…
+ But: costly & may need very high resolution

**Option 2: Antialiasing**

+ Making Fourier contents “narrower” before repeating
+ i.e. **Filtering out high frequencies before sampling**



第一个办法是增加采样率，比如显示器是$600 \times 480$的古老显示器，一个像素非常大，我们用它光栅化一个三角形当然看起来锯齿化严重。那我如果用现在的视网膜显示器，像素和像素之间间隔小，意味着采样率高，频谱上对应间隔大不容易出现混叠。

然而这并不是反走样要做的事情。另外一个做法是做反走样，回到一开始先做模糊再做采样。通过频率分析我们可以知道先做模糊再做采样它是有意义的，对应频域就是低通滤波，





##### Antialiasing = Limiting, then repeating

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407170213916.png)



对于这么一个函数本身对应频谱是梯形，如果我们先对原始信号进行一个模糊把高频信号砍至虚线方块，那剩下的信号就是这样一个形状，我再以原本稀疏的采样率来采样，频谱在这个位置不再发生混叠。



##### Regular Sampling

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407233144174.png)

Note jaggies in rasterized triangle where pixel values are pure red or white.



##### Antialiased Sampling

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407233423082.png)

Note antialiased edges in rasterized triangle where pixel values take intermediate values .



现在先对这个信号做模糊，把三角形变成模糊三角形，然后再采样出结果。



##### A Practical Pre-Filter

A 1 pixel-width box filter (low pass, blurring) 

![image-20210407233645681](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407233645681.png)



我们实际操作中使用低通滤波器模糊三角形，对它进行卷积。在图像上最简单的一个块就是一个像素，而低通滤波器可以有效模糊。



##### Antialiasing By Averaging Values in Pixel Area

**Solution:**

+ Convolve f(x,y) by a 1-pixel box-blur Recall: convolving = filtering = averaging
+ Then sample at every pixel’s center



对于每个像素我对三角形求平均值，然后我再做采样。



##### Antialiasing by Computing Average Pixel Value

In rasterizing one triangle, the average value inside a pixel area of f(x,y) = inside(triangle,x,y) is equal to the area of the pixel covered by the triangle.

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407233820841.png)



对于任何像素，我都知道三角形可能会完全覆盖/一部分覆盖。不同的像素对覆盖面积求平均，对像素进行赋值。





### Antialiasing By Supersampling (MSAA)

#### Supersampling

Approximate the effect of the 1-pixel box filter by sampling multiple locations within a pixel and averaging their values:

对于任何一个像素，我认为一个像素被我划分为很多小的像素例如图中像素被划分为$4 \times 4$的16个小像素。假如每个小像素有一个中心，我可以判断它们是不是在三角形内，然后我们再把判断结果平均起来就是覆盖区域的一个近似。



#### Point Sampling: One Sample Per Pixel

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407235621770.png)





#### Supersampling: Step 1

Take NxN samples in each pixel.

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407235818827.png)



我们可以把像素内部多加一些采样点如上图所示，每个像素被划分为$2 \times 2$的4个小像素。



#### Supersampling: Step 2

Average the NxN samples “inside” each pixel.

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407235920114.png)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210407235953474.png)



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210408000028123.png)





#### Supersampling: Result

This is the corresponding signal emitted by the display.

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210408000110106.png)



通过四个像素点去感知是否在三角形内，算出覆盖率如上图所示。



<br/>

<center>{% btn https://sites.cs.ucsb.edu/~lingqi/teaching/resources/GAMES101_Lecture_06.pdf,  GAMES101_Lecture_06, fas fa-download %}</center>

