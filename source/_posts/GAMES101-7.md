---
title: Illumination, Shading and Graphics Pipeline
comment: false
tags:
  - Computer Graphics
  - Shading
categories: 现代图形学入门 (GAMES101-Introduction to Computer Graphics)
abbrlink: 527175ac
date: 2021-04-08 16:20:55
type:
banner_img:
index_img:
translate_title:
top:
mathjax: true
---



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/EyWnXhjWYAEodJy.jpeg)

<div align=center>
  <font size="3">
    <i>
      <a href="https://twitter.com/MVC_discord">Twitter@MVC_discord</a>
    </i>
  </font>
</div>



### 引言

GAMES101 现代图形学入门是由闫令琪老师教授。今天我们开始讲着色、光照以及图形管线，并把上节课光栅化最后的深度测试结束。

<!--more-->





### Visibility / occlusion

#### Painter’s Algorithm

Inspired by how painters paint

Paint from back to front, **overwrite** in the framebuffer

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210408163045647.png)



在场景中有很多不同物体，我们要把物体都放在屏幕上自然会涉及到顺序的问题。很直观的想法是把最远的物体先画在屏幕上，然后逐渐把近的物体再补在屏幕上使之覆盖之前远处的物体。从远到近把这幅图画出来就可以得到准确的结果，这正是以前油画画家是如何作画的。

 

Requires sorting in depth (O(n log n) for n triangles)

Can have unresolvable depth order.  

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210408163807790.png)



在一定程度上画家算法是可以的，通过深度的排序从远到近画出来。但有一个情况非常特殊，三个三角形两两之间存在覆盖关系形成了一个环，在深度上存在互相遮挡的关系，在这种情况下我们没办法定义它们之间的深度关系，自然不能用画家算法提前排序。



#### Z-Buffer

This is the algorithm that eventually won. Idea:

+ Store current min. z-value **for each sample (pixel)**

+ Needs an additional buffer for depth values 

  \- frame buffer stores color values

  \- depth buffer (z-buffer) stores depth

IMPORTANT: For simplicity we suppose **z is always positive** (smaller z -> closer, larger z -> further)



为了解决这个问题，图形学里大家引入了一个概念叫深度缓存/深度缓冲，这是一个大家广泛采用的一个算法。这个算法其实就是说既然对于空间中的三角形不好排序远近顺序，但对每个像素而言可以记录像素所表示的几何最浅深度，换言之离我们最近的距离。

为了完成这个深度缓冲，图形学中一般生成这幅图像的同时生成另一个图像，这个图像只存任何一个像素看到几何物体的最浅深度的信息，我们管这幅图称为深度图/深度缓存，我们始终同步生成两个不同的东西，一个是最后的结果（frame buffer），另外一个对应的深度维护遮挡信息（depth buffer）。



#### Z-Buffer Example

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210408195344534.png)



对于一个场景来说，我们最后要渲染出一幅画面（左图），然后我们同时还要维护任何一个像素看到的深度（右图），这两幅图是同步生成的。观察右图可以发现，离视点近的颜色会比较深，而离视点远的颜色就比较浅。



#### Z-Buffer Algorithm

Initialize depth buffer to ∞

During rasterization: 

```c++
for (each triangle T)
	for (each sample (x,y,z) in T)
		if (z < zbuffer[x,y]) // closest sample so far
			framebuffer[x,y] = rgb; // update color
			zbuffer[x,y] = z; // update depth
		else
			; // do nothing, this sample is occluded
```



深度缓存中所有像素首先初始化深度为无穷，然后我们把一个个三角形光栅化成不同的像素。前两个`for`循环代表任意一个三角形中的任意一个像素；找到这个三角形对应的像素后我就知道新的三角形如果要画在像素内，那对于这个像素来说它的深度在新三角形中进行更新：如果其深度小于深度缓存，那么我们把深度缓存的值更新为小的深度，并且把新的三角形的这个像素的颜色进行更新。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210408200518975.png)



一开始所有像素的深度缓存全都是无限大的值`R`，然后光栅化三角形覆盖了好多像素并替换了原本为无限大的深度缓存；同理在此基础上再插入一个三角形，考虑每个像素的迭代情况，最后得到新的光栅化结果。





#### Z-Buffer Complexity

**Complexity**

+ O(n) for n triangles (assuming constant coverage)
+ How is it possible to sort n triangles in linear time? 

Drawing triangles in different orders?

**Most important visibility algorithm**

+ Implemented in hardware for all GPUs



之前的画家算法对$n$个三角形进行排序需要$O(nlogn)$时间复杂度，如果我们认为每个三角形都不是特别大或特别小，它会覆盖一定的常数个像素，那么深度缓存的时间复杂度是$O(n)$。虽然这看起来是一个顺序问题，我们只花了线性的时间得到了一个正确的顺序。这里我们并没有排序，对于任何一个像素我们只是在记录它当前所看到的最小值，而没有求其他三角形的遮挡关系。

有人可能会问光栅化顺序会不会产生影响，深度缓存算法有一个优点，假设不会有两个不同三角形在同一深度的情况（浮点数很大程度避免了这种情况），它和顺序是没有关系的，最后得到的是同样的结果。



总结一下深度缓冲/深度缓存，这是一个非常非常重要的算法，它广泛应用在所有的硬件中，目前来说所有的光栅化都会做深度缓存的测试，通过维护深度缓存最后得到一个正确的遮挡算法。





<br/>

### Shading

#### What We’ve Covered So Far

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210408201156677.png)



目前我们学了什么？首先我们在空间中定义了模型，可以对模型进行一些变换；然后我们通过视图变换把相机放在原点；变换完之后我们自然把三维的模型变成二维的，也就是投影变换；最后我们学习了从投影如何映射到二维的屏幕上，把它变成一个采样结果，光栅化的过程。



#### Rotating Cubes (Now You Can Do)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210410221201356.png)



#### Rotating Cubes (Expected)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210410221237384.png)



#### What Else Are We Missing?

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210409080747650.png)



大家可以看到某种巧克力奶茶的泡沫、蛋挞和葡萄等等，为什么不同的东西可以看到不同的颜色，显示五彩缤纷的颜色？在不同的光照下我们可以想象光源移动一下位置，物体并没有发生位置上的变化，但是颜色上发生了变化，这个问题就是着色。





#### Shading: Definition

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210409080421062.png)



所谓着色，就是它引入明暗和颜色的不同。着色在图形学中做的与素描中画一个球相似，光源打到球上某一块会形成较亮的高光，背向光源这一面由于接受不到光就比较暗形成投影。在这门课中，我们把着色定义为对不同的物体应用不同的材质这么一个过程。





#### A Simple Shading Model (Blinn-Phong Reflectance Model)

##### Perceptual Observations

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210409082626189.png)



大家首先看这几个茶杯，可以看到茶杯在某一个光源的照片。这个光源照亮了这些茶杯，基本看到茶杯上有高光、漫反射和间接光照。在这里我们做一个假设，在间接光照这个点可以接受来自四面八方来自环境的不同的反射光，而这个反射光是一个常量。





##### Shading is Local

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210409082720380.png)



我们来定义一些关于表面、光源和观测的东西。对于一个着色点它应该在物体表面上，可以是曲面，但我们认为在局部一个非常小的范围内它永远是一个平面，我们可以在平面定义法线`n`。同样我们可以连接着色点与相机定义观测方向`v`；从着色点看向光源同样可以得到一个方向，称之为光照方向。

需要注意的是这些向量都是单位向量，我们只关心它的方向不关心大小，长度永远是1。



**No shadows** will be generated! (**shading ≠ shadow**)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210409085647135.png)



我们所说的着色只考虑这个点和几个不同的方向，不考虑这个点是不是在阴影内。如图所示，这样做可以看到明暗变换但看不到阴影，阴影的生成之后再说。



##### Diffuse Reflection

**Light is scattered uniformly in all directions**

+ Surface color is the same for all viewing directions

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210409082849445.png)



有一根光线打到物体的某一个点的时候，光线会被均匀的反射到各个不同的方向上去，这就叫漫反射。上图就可以看到有一个入射的光线打到了一个点，反射会向各个方向去。



**But how much light (energy) is received?**

+ Lambert’s cosine law

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210409083011315.png)



当我的物体表面着色点的朝向和光照有一定夹角的时候，我会发现得到的明暗是不一样的，同样的光照到同样的表面上以不同的角度照上去为什么得到的明暗不一样呢？上图有六根离散的光线，每一根光线代表了固定的能量，如果平放表面可以接收到所有的光线；而60度只能接收到三根光线，物体表面就暗一点。

观察发现光线来源方向`l`与表面法线`n`的夹角决定了物体表面该有多么亮。一个更科学的理解是光是一种能量，于是物体应该接收能量，我们可以想象一个太阳能板，太阳能板越大接收到的能量越多；春夏秋冬的季节更替也是如此，在夏天太阳会直射地表，其夹角的周期往返导致了不同的季节。

朗伯余弦定律定义了接收到的能量和光照方向与法线方向之间余弦成正比，可以考虑特殊值验证。



##### Light Falloff

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210409083128044.png)



光是一种能量，如果我们假设这个光来自点光源，它无时无刻往四面八方辐射能量。有一个很聪明的观测方法是认为在任何一个时刻这个点光源辐射的能量一定是在一个球壳上，如果假设在真空中传播，根据能量守恒定律远球壳的能量和近处球壳能量相同。

我们发现一个问题，原本能量都集中在一个小的球壳，意味着球壳上每一个点/位置能量是很多的，然后传播过程中球越变越大，球壳的表面积也越变越大那也意味着在球壳某一个点上对应的能量越变越小。考虑一个单位距离定义光的强度为$I$，那么如果传播到距离为$r$，那么这时光的强度和距离平方成反比：$I/r^2$。

现在假设我们知道一个点光源，然后又知道着色点离点光源有多远，那我就知道有多少光真正传播到点光源的附近，如果还知道有多少光会被吸收，结合起来我们可以得到Diffuse表示方法。





##### Lambertian (Diffuse) Shading

Shading **independent** of view direction

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210409083233431.png)



假设点光源离着色点有一定的距离$r$，如果我们定义点光源的光单位强度是$I$，到达着色点的能量会被吸收。通过接收和到达多少能量，我们就能算出漫反射最后应该看到多少能量。这里的`max`函数是保证结果永远是正的，有实际物理意义的，考虑反射而不是折射；`kd`表示漫反射系数，如果为1表示这个点完全不吸收能量，0则意味着所有能量都被吸收了，没有能量反射出去。

漫反射打到着色点上，能量会被均匀的反射到各个不同的方向上去，意味着不管从哪里观测它看到的结果应该是一模一样的。漫反射项与观察方向`v`完全没有关系，从式子上看也是如此，我们考虑的是光线与法线之间的夹角。



Produces diffuse appearance

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210409083358190.png)









<br/>

<center>{% btn https://sites.cs.ucsb.edu/~lingqi/teaching/resources/GAMES101_Lecture_07.pdf,  GAMES101_Lecture_07, fas fa-download %}</center>

