---
title: Overview of Computer Graphics
comment: false
tags:
  - Computer Graphics
categories: 现代图形学入门 (GAMES101-Introduction to Computer Graphics)
abbrlink: 2f575b64
date: 2021-03-22 22:29:06
type:
banner_img:
index_img:
translate_title:
top:
mathjax:
---



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/EwAS3QHWgAEDqyq.jpeg)

<div align=center>
  <font size="3">
    <i>
      <a href="https://twitter.com/coconut_mocha">Twitter@coconut_mocha</a>
    </i>
  </font>
</div>


### 引言

GAMES101现代图形学入门是由闫令琪老师教授。本节主要讨论什么是图形学，为什么要学图形学以及该系列课程内容的介绍。

<!--more-->



### Instructor

**闫令琪**

+ 2018 - now: Assistant Professor @ UCSB
+ 2013 - 2018: Ph.D @ UC Berkeley
+ 2009 - 2013: B.E. @ Tsinghua University
+ Website: www.cs.ucsb.edu/~lingqi/
+ Research: Rendering in Computer Graphics
+ Hobbies: research, video games, piano, traveling, NBA, etc.

老师主要做图形学中渲染、绘制这一方向，之前的研究成果被工业界采用：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210322225815910.png)



### Today’s Topics

+ What is Computer Graphics?
+ Why study Computer Graphics?
+ Course Topics
+ Course Logistics
+ Linear Algebra Review

今天的主题主要提到几点，什么是图形学？为什么要学图形学？以及课程的内容介绍。



### What is Computer Graphics?

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210322230339360.png)





### Why study Computer Graphics?

今天我们着重来讲图形学有哪些应用，我们为什么要学习它，它到底好在哪里？

#### Video Games

计算机图形学的应用首当其冲的就是游戏领域。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210322230637928.png)

《只狼》的游戏画面非常好，那么在现在这个时代什么才是好的画面呢？我们平常可能看不明白，我就觉得它好，从技术的角度，好的画面的标准只需要看**画面是不是足够亮**就可以了。为什么呢？这体现了图形学渲染中的关键技术：全局光照。如果全局光照做的好，那么整个画面就会亮，看起来就会很舒服；如果你看整个画面比较暗，可能在这一方面就会有一定的技术不足。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/20210322233200.png)

另一款想提到的游戏是《无主之地3》。这个游戏的画面完全不同于只狼，更偏向于卡通风格。那么卡通风格为什么看着是卡通的呢？图形学中又是通过什么方式表述的呢？这一系列都是图形学需要解决的问题。



#### Movies

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210322233516387.png)



在电影里图形学得到了广泛的应用，非常早的时候（1999年）的《黑客帝国》的特效非常优秀，诸如子弹时间这类电影特效也是从这类影片延伸出来的。电影特效是通过计算机图形学的技术合成出来并与实际存在的东西完美的结合到一块，让你觉得非常真实。

但特效是图形学最简单的应用，因为平常很难见到慢动作之类的特效。而最困难的东西是大家日常生活中见到的东西，比如生活中食物的渲染大家就做的不是很好。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210322234323946.png)

电影还有另外一个里程碑式的电影：《阿凡达》。它里程碑的原因是它引入了人的面部捕捉，或者说它做的非常好并且大量广泛的应用这种技术，由真人演员做出各种各样的表情直接反应到虚拟的人物中。那么这个技术是如何做到的？这也是计算机图形学需要研究的事情。



#### Animations

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210322235837554.png)

动画自然也是不能忽视的。《疯狂动物城》中有许多毛茸茸的小动物，而如果大家自己看真的可以看到一根一根的毛发，这些毛发聚集在一块又会呈现出什么效果呢？大家想想就觉得非常难，那动物身上多少根头发啊，起码有上百万根吧而每一根头发都要和光线作用，不同的头发之间又要相互作用，最后才达到人的眼睛。

计算机图形学如何去做呢？首先涉及到几何，如何去表述这些复杂的几何形体？然后是如何去渲染把它真正显示出来，计算光线在这些几何形体之间的传播方式。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210323000438198.png)

另一个奥斯卡获奖动画是《冰雪奇缘》。这里面涉及到各种不同的技术，图中Elsa正在放出各种各样的技能，可以看出各种不同的特效，比如烟雾、发光的粒子在空中盘旋形成不同的图案，这些东西是怎么做出来的？这就是图形学下面另一个重要的分支：模拟或动画。



#### Design

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210323125126123.png)



大家可能听过CAD，就是计算机辅助设计。现在的设计很少手绘设计了，正常来说都是用电脑来辅助。上面两幅图左边是电脑渲染出来的，右边是真实存在的照片，它是在Autodesk Gallary展示。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210323125716806.png)



这里看到的是一个国外的家装网站Ikea，这是由计算机生成的而不是真的装修的结果，只需要艺术家摆放再给予一定的光照条件，光线由右边的大窗户进来，进来后会有各种各样的阴影，光线在图像中各种各样弹跳最后进入人的眼睛，这个过程叫做渲染。

在Ikea网站中75%都是渲染出来的，而且这还是几年前的统计。国内现在也有一些这种公司，室内设计已经完全走入了平常的消费者的范围之内，这都是图形学的功劳。





#### Visualization

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210323134618506.png)

图形学会操纵这些视觉信息，一种实际的操控方式就是可视化。可视化就是把一些测量出来的一些三维的扫描比如CT、核磁共振信息，这些信息通过一定的办法把它变成视觉信息，这个过程我们就称之为可视化，也是属于计算机图形学的领域。





#### Virtual Reality

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210323191429116.png)



虚拟现实中的一切也都是全部由电脑生成的，这也是图形学的成果。



#### Simulation

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210323194415527.png)



模拟是图形学另一个非常重要的领域，比如左图的沙尘暴中模拟体现在模拟沙子如何在空气中飞舞，怎么样推过来，怎么把这些房屋摧枯拉朽。又如黑洞模拟的是光线，并不是尘埃这种实际的物质。而光线靠近黑洞应该发生偏折，这些都是要精确模拟的东西。



#### Graphical User Interfaces

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210323194904514.png)

这里提到一个GUI图形用户接口，大家有人用过Windows有人用过Mac有人用过各种Linux发行版，这些设计都是属于图形学的范畴。



#### Typography

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210324082210419.png)



再给大家介绍一下字体。如果咱们看一张图放大放大放大，最后会看到一个什么样的现象呢？变模糊了对不对？但是大家把字体字号调的非常大，还会发现很清楚。那么这个字体是拿什么表示的？它和图像有什么区别？为什么我们在任意放大的情况下都能看到连续的曲线呢？这时候就涉及到点阵和矢量这两个不同的概念，之后会给大家解释这个事情。

多给大家普及一个知识，*The Quick Brown Fox Jumps Over The Lazy Dog*这句话是在字体测试中很常见的句子，因为它用尽了英文中的26个字母，所以一般这句话会出现两次，一次大写一次小写，可以测试字体的完整性。





#### Fundamental Intellectual Challenges

+ Creates and interacts with realistic virtual world
+ Requires understanding of all aspects of physical world
+ New computing methods, displays, technologies

图形学为什么难呢？因为它包括了很多东西，比如研究在真实世界中如何去做各种各样的东西，需要理解不同方面的物理规则......这是输入需要不同的计算方法，输出需要不同的显示方法，例如裸眼3D和全息影像等等。



#### Technical Challenges

+ Math of (perspective) projections, curves, surfaces
+ Physics of lighting and shading
+ Representing / operating shapes in 3D
+ Animation / simulation 
+ ~~3D graphics software programming and hardware~~

根据个人对图形学的理解，这门课不会去做硬件的编程比如三维的应用OpenGL。计算机图形学就是OpenGL吗？图形学包括了很多东西，而OpenGL仅仅是图形学中的一个API。



Forget about the previous reasons：**Computer Graphics is AWESOME!**





### Course Topics

#### Rasterization

+ Project geometry primitives (3D triangles / polygons) onto the screen
+ Break projected primitives into fragments (pixels)
+ Gold standard in Video Games (Real-time Applications)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210324085708960.png)



什么是光栅化？把三维空间的几何形体显示在屏幕上，这就是光栅化。

它是所有游戏或者实时计算机图形学的主要应用，实时在不同的领域有不同的定义，在计算机图形学下面实时的定义是每秒钟能够生成30帧画面，也就是30fps。实时会广泛应用光栅化方法，主要是做投影。





#### Curves and Meshes

+ How to represent geometry in Computer Graphics

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210324090540152.png)



几何领域着重介绍如何表示一条光滑的曲线，如何表示曲面，如何用简单的曲面通过细分的方法得到更复杂的曲面，比如在形状发生变化时如何保持物体的拓扑结构。





#### Ray Tracing

**Shoot rays from the camera though each pixel**

+ Calculate intersection and shading
+ Continue to bounce the rays till they hit light sources

**Gold standard in Animations / Movies (Offline Applications)**

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210324091342276.png)



光线追踪在动画和电影中着重使用，它能够生成非常逼真的画面，比如右边会显得非常美观。

图形学中有很多事情为了达到某个目标牺牲一些其他的目标，光线追踪能达到很好的效果，但它就是慢。人都是贪婪的，但我认为这是好事情，正因为这样才会让人会去寻找一些两全其美的解决方法。





#### Animation / Simulation

+ Key frame Animation
+ Mass-spring System

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/slide_010.jpg)



动画模拟仿真会讲到很多不同东西，比如大家扔一个弹性的球落到地上，如何被挤压，如何弹上去再下来......上图是布料材质的模拟效果，结果非常令人惊讶。



#### GAMES101 is NOT about

+ Using OpenGL / DirectX / Vulkan

+ The syntax of Shaders

+ **We learn Graphics,   not Graphics APIs!**
+ After this course,  you’ll be able to learn these  by yourself (**I promise**)
+ 3D modeling using Maya / 3DS MAX / Blender, or   VR / game development using Unity / Unreal Engine  (where can I learn them?)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210324093233447.png)



+ Computer Vision / Deep Learning topics, e.g. XYZ-GAN  (where can I learn them?)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210324093143984.png)

图形学和计算机视觉往往被混淆在一起，在这门课我们不会教计算机视觉。什么是视觉，一切需要猜测的都是计算机视觉的内容，左图就是识别哪些是人，哪些是路面，哪些是障碍，像这些东西没有一个准确的答案，是计算机视觉需要理解的东西。同样的，深度学习在这门课中不会被特别提及。



#### Differences?

+ Personal Understanding



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210324094750517.png)



+ No clear boundaries
+ And I can’t define Computer Graphics



模型MODEL更像是描述三维几何形体或者对渲染来说是材质和光照，经过渲染后成为了图形。而从一张图IMAGE，我如何去识别各种各样的模型（语义分割）呢？从图像分析出它到底是什么样的结构，这就是计算机视觉。



### Course Logistics

#### General Information

**Modern Course**

+ Comprehensive but **without hardware programming!**
+ Pace / contents subject to change

**Course Website**

+ http://www.cs.ucsb.edu/~lingqi/teaching/games101.html
+ Has all the needed information
+ Syllabus, slides, reading materials, etc.



#### Course Website

Course slides and (pre)-reading materials



#### References

**No Required Textbooks**

+ Reading materials (if any) will available online before lectures
+ Lecture slides will be available after class

**Most recommended reference**

+ Steve Marschner and Peter Shirley, "Fundamentals of Computer Graphics", 3rd or later edition.





#### Assignments

**Assignments**

+ Mostly programming tasks with provided code skeletons and virtual machine image
+ Weekly (usually no more than 20 lines of code per week)
+ Language: C++



**Submission**

+ Submit your project by 11:59PM on/before the due dates (strictly enforced)

+ Feedback will be provided in a week





#### Use An IDE!

**IDE: Integrated Development Environment**

**Helps you parse a entire project**

+ And gives hints on syntax / usages of member functions, etc.

**Recommended IDEs**

+ Visual Studio (Windows only) / Visual Studio Code (cross platform)
+ Qt Creator (personal)

**Not Recommended IDEs (for C++ programming)**

+ CLion, Eclipse
+ Sublime Text, Vi / Vim, Emacs (not even IDEs)





#### Academic integrity

**Work alone for regular assignments**

+ no copy-pasting from any other sources

**Do not publish your code (on Github, etc.)   for assignments using our skeleton code**

**Do not post your solution online**

+ Discussion / explanation is welcomed





<br/>

<center>{% btn https://sites.cs.ucsb.edu/~lingqi/teaching/resources/GAMES101_Lecture_01.pdf,  GAMES101_Lecture_01, fas fa-download %}</center>

