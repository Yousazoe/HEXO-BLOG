---
title: 'Shading, Pipeline and Texture Mapping'
comment: false
tags:
  - Computer Graphics
  - Shading
categories: 现代图形学入门 (GAMES101-Introduction to Computer Graphics)
abbrlink: d3d02c34
mathjax: true
date: 2021-04-11 17:39:22
type:
banner_img:
index_img:
translate_title:
top:
---



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/EyoBGzMWQAAv63l.jpeg)

<div align=center>
  <font size="3">
    <i>
      <a href="https://twitter.com/MVC_discord">Twitter@MVC_discord</a>
    </i>
  </font>
</div>



### 引言

GAMES101 现代图形学入门是由闫令琪老师教授。今天我们讲着色的第二个部分，包括Blinn-Phong着色模型、图形管线和纹理映射。



<!--more-->

### A Simple Shading Model (Blinn-Phong Reflectance Model)

#### Blinn-Phong reflectance model


![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210409083233431.png)



简单复习一下漫反射项。首先这个光打到了某一个着色点，然后它会往四面八方反射出去，也就是说漫反射项和观测方向`v`没有任何关系。

我们推导了光源在传播的过程中会根据它传播的距离产生能量的衰减，$I/r^2$表示实际有多少能量到达了着色点；到达后还需要吸收，接收多少能量是和入射方向、法线方向的夹角余弦有关系；如果材质本身有颜色，那我们在前面加上一个漫反射系数$k_d$。当然这是一个很经验性的模型，但它有一定物理的道理在里面。



#### Specular Term (Blinn-Phong)

Intensity **depends** on view direction

+ Bright near mirror reflection direction

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210411202704724.png)



现在我们要把高光项加进去，什么情况我们能看得到高光？有高光平面应该比较光滑，它的反射具有一定特性：反射方向接近镜面反射的方向（对于镜子而言给出入射方向和法线就可以得到出射方向）。当我们的观察方向和镜面反射接近时，我能看到高光，也就是`v`和`R`足够接近的时候我们就得到这么一个高光项。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210411203227604.png)



但是Blinn-Phong模型做了一个很聪明的事情，它看到了一个现象，当我的观察方向和镜面反射方向接近的时候，其实就说明了法线方向和所谓半程向量很接近。如果我有一个入射方向`l`，出射方向`v`，那么我可以求它的角平分线`h`，那么`v`和`R`接近就可以表示为`n`和`h`接近。

如何衡量两个向量接近呢？点乘，如果两个方向足够相近，那么点乘的结果自然是接近1；如果两个方向离得比较远，那么就接近0，当然反方向我们就不考虑。从式子就可以看出来，多少能量到达着色点还是一样考虑，只不过这里我们要考虑的事情就是半程向量方向是否接近法线方向。同样道理，高光项我们也会给它颜色，不过高光通常来说认为是白的，所以$k_s$镜面反射系数通常认为是一个白的颜色。

这里有人会注意到，为什么这里不考虑有多少能量被吸收了呢，不管什么反射我们都要考虑啊。实际我们如果要做的对的话，我们确实还是要在镜面反射上考虑有多少能量被吸收，但这里没有考虑是因为Blinn-Phong模型毕竟是经验性模型，这一点把它简化掉了，主要关注是否能保证我们能看到高光。

还有一个问题是为什么要用半程向量和法线，如果我就用镜面反射方向和观察方向不行吗？完全可以，Blinn-Phong模型作为它的一种改进，因为半程向量实在太好算了，相对而言反射方向就相对困难，计算量会增加很多。



#### Cosine Power Plots

Increasing p narrows the reflection lobe

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210411205518135.png)



最后一个问题是为什么会存在一个指数项`p`。点乘确实能衡量两个向量是否足够接近，但是它的容忍度太高了，可以看上图当两个向量夹角在45度的时候，我觉得它已经离的很远了，但余弦仍然有一个较大的值，如果我们真用余弦会产生一个超级大的高光。

所以我们对夹角余弦做一个简单操作，在它上面加上若干指数。随着指数增加，角度增大的衰减速度加快，在Blinn-Phong模型中`p`的数值大概在100～200左右。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210411205915670.png)



上图显示的是漫反射项和高光项在一起。如果我从上到下考虑不同的行，就相当于镜面反射系数在增大表示它的亮度；如果我们横向来看最后一行，随着指数`p`增长，我可以看到越来越小的高光。





#### Ambient Term

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210412123125096.png)



最后一项是环境光照项。我们做一个大胆的假设，认为任何一个点接收到来自环境的光永远都是相同的，而强度为$I_a$，$k_a$为环境光的系数，结合两项得到近似的环境光。

环境光不讲究从哪个地方进来，与直接的实际光照方向没有任何关系；并且不管从哪里看得到的结果应该是一样的，和观测方向也没有关系，所以环境光是一个常数，保证没有地方完全是黑的，把所有其他项加起来提升一个亮度。



#### Blinn-Phong Reflection Model

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210412123208799.png)



把所有项加起来得到上面的结果，这里就是我们说的Blinn-Phong反射模型。



### Shading Frequencies

What caused the shading difference?

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210412172747111.png)



什么是着色频率？大家可以看这三个球，它们拥有完全相同的几何形状，但着色的结果各不相同。

着色频率就是说着色要应用在哪些点上，之前我们说着色是在着色点上，那如果我们把着色应用在一个面上，那么一个平面我只要做一次shading，得到的就是左图结果；中间它计算出顶点对应的着色，中间的部分用插值算出颜色；右图的着色应用在每个像素上，我们可以得到一个非常好的结果。



#### Shade each triangle (flat shading)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210412174137293.png)



在第一种方式中每一个三角形是一个平面，我把三角形的法线通过两边的叉积求出来，算出shading的结果就是三角形长什么样，自然对三角形内部没有着色的变化，得到一个完全一样的结果，这个方式叫做flat shading。



#### Shade each vertex (Gouraud shading)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210412174512306.png)



在第二种方式中我们可以在任意一个顶点求出法线，每个顶点做一次着色，那每个顶点就有颜色。三个顶点固定一个三角形，三角形内部颜色通过插值的方法算出来，可以看到结果比flat shading要好，我们称为gouraud shading。



#### Shade each pixel (Phong shading)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210412181629602.png)



在第三种方法中对于每一个像素都可以插值出独特的法线方向，对每一个像素进行一次着色，那么我们就可以得到一个相对比较好的结果，我们称为phong shading。需要注意与Blinn-Phong反射模型不一样，这里是着色频率，碰巧是同一个人发明的。



#### Shading Frequency: Face, Vertex or Pixel

![image-20210412214049243](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210412214049243.png)



这三种的区别取决于具体的模型，我们不能说flat shading一定就很差，我们可以来看这个$3 \times 3$的图。每一行用的模型都是一样的，而行与行之间用了更多的三级形，几何形体本身更加的密集，定义的更加光滑，在这种几何足够复杂的情况下我其实就可以用一些相对简单的着色模型，得到的结果也不错。

也就是说，着色的频率取决于面、顶点或者像素它们本身出现的频率，当我的面出现频率已经很高的情况下我就不再需要这么复杂逐像素的着色。



#### Defining Per-Vertex Normal Vectors

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210412215939413.png)



前面我们留下两个问题，第一个是逐顶点的法线是什么，，如何去计算顶点的法线？

一个理想化的情况是如果你知道这个模型是用一堆三角形表示，但其实我想表示一个球，那么任何一个顶点对应的就是球上面的一些点，我们就可以通过球所在的位置算出法线（从球心连向原点）。

平常不会有这么特殊的情况，怎么可能知道它背后试图表示的是什么呢？人们发明了一种很不错办法，既然任何一个顶点肯定会和很多三角形有所关联，那么顶点的法线就认为是相邻的这些面的法线求平均。需要注意的是这里简单的平均可能说明不了问题，那我们可能还需要做一个加权（面积）的平均。



**Barycentric interpolation** (introducing soon) of vertex normals

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210412221037051.png)



Don’t forget to **normalize** the interpolated directions



另一个问题是如何去真正定义一个逐像素的法线。在三角形的内部假如我已经知道它的顶点法线是什么了，那如何得到内部的平滑过渡的法线呢？这里需要用到重心坐标，马上就要给大家说。







### Graphics (Real-time Rendering) Pipeline

#### Graphics Pipeline

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210412221834660.png)



从场景到最后一张图经历的过程被称为管线，表示的是一系列不同的操作，可以理解为一种“流水线”。

一开始输入是一堆空间中的点，并且经过第一步我们要做一个投影，然后这些点会形成三角形通过光栅化把它离散成为Fragments打散成不同的像素，在此之后就可以进行着色输出图像。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210412221922349.png)



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210412221945518.png)



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210412222013417.png)



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210413095416204.png)



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210413095448930.png)



#### Shader Programs

+ Program vertex and fragment processing stages
+ Describe operation on a single vertex (or fragment)

Example GLSL fragment shader program

```glsl
uniform sampler2D myTexture; // program parameter
uniform vec3 lightDir; // program parameter
varying vec2 uv; // per fragment value (interp. by rasterizer)
varying vec3 norm; // per fragment value (interp. by rasterizer)
void diffuseShader()
{
 vec3 kd;
 kd = texture2d(myTexture, uv); // material color from texture
 kd *= clamp(dot(–lightDir, norm), 0.0, 1.0); // Lambertian shading model
 gl_FragColor = vec4(kd, 1.0); // output fragment color
}
```



+ Shader function executes once per fragment.
+ Outputs color of surface at the current fragment’s screen sample position.
+ This shader performs a texture lookup to obtain the surface’s material color at this point, then performs a diffuse lighting calculation.



现代GPU允许自己去编程解决顶点和像素如何做它们的着色。如果要实现一些复杂的东西正常情况下需要大家去写这个Shader，它本质上是能在硬件执行的语言，例如OpenGL是一个图形学的API，可以用它写一些Shader。





#### Goal: Highly Complex 3D Scenes in Realtime

+ 100’s of thousands to millions of triangles in a scene
+ Complex vertex and fragment shader computations
+ High resolution (2-4 megapixel + supersampling)
+ 30-60 frames per second (even higher for VR)



#### Graphics Pipeline Implementation: GPUs

Specialized processors for executing graphics pipeline computations

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210413101651194.png)



GPU自然是图形管线的硬件实现，它在硬件层面实现了例如三角形的光栅化、怎么样实现投影。有一部分是可编程的就是我们所说的着色器，顶点着色器和片段/像素着色器，但其实随着GPU的发展，有越来越多不同类型的着色器产生，是非常值得期待的发展。



#### GPU: Heterogeneous, Multi-Core Procesor

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210413102201416.png)



GPU本身大家可以理解成高度并行化的处理器，咱们平常说CPU买什么i7i9，核心的数量可以理解成可以并行线程的数量，如果学过高性能计算可以知道GPU的并行度是相当惊人的，远远超过CPU，所以特别适合做图形学并行计算。



### Texture Mapping

#### Different Colors at Different Places?

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210412222141257.png)



纹理映射通过上图来说明白，两个台灯照亮一个地板和一个球。如果我们只盯着这个球来看其实它的着色我们会写，无非是两个点光源加起来。但球上面有不同的颜色，它们的基本区别是共用一个着色模型，只是说它们本身的漫反射系数发生了一些改变，也就是说我们希望有一种方法能够定义对于一个物体它上面任何一个点它们的不同属性。



#### Surfaces are 2D

Surface lives in 3D world space

Every 3D surface point also has a place where it goes in the 2D image (**texture**).

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210412222224668.png)



我们把属性定义在物体表面上，当然我们要考虑物体表面任何一个点应该是什么样的颜色做着色。物体表面该怎样去理解？我做一个声明，任何一个三维物体表面都是二维的，例如地球仪显然是一个三维的物体，如果把地图拿出来往平面一放变为平面。

纹理就是一张图，这张图可以任意把它撕开用其中一块或者拉伸、压缩，把它蒙在三维物体的表面，这个过程就叫纹理映射。映射自然是一个一一对应的关系，那我们找到一个物体表面任何一个点和纹理上任何一个点它们之间的关系。



#### Texture Applied to Surface

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210412222259197.png)





#### Visualization of Texture Coordinates

Each triangle vertex is assigned a texture coordinate (u,v)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210412222332835.png)



纹理上定义一个坐标系，真正指定纹理上任何一个点的坐标。这个坐标系大家通常用(u,v)表示纹理上任何一个点，比如纹理是右图，那么任何一个物体上的三角形如何映射到纹理上把它显示出来。通常来说不管分辨率与长宽比，大家认为的(u,v)范围都是在0～1之内，约定俗成便于处理。



#### Texture Applied to Surface

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210412222355233.png)







#### Textures can be used multiple times!

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210413104734693.png)







<br/>

<center>{% btn https://sites.cs.ucsb.edu/~lingqi/teaching/resources/GAMES101_Lecture_08.pdf,  GAMES101_Lecture_08, fas fa-download %}</center>

