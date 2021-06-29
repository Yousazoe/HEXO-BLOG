---
title: Introduction and Overview
comment: false
tags:
  - Computer Graphics
categories: 高质量实时渲染 (GAMES202-Real-Time High Quality Rendering)
abbrlink: 26c49312
date: 2021-04-11 17:14:14
type:
banner_img:
index_img:
translate_title:
top:
mathjax:
---



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/EyXC_9OWQAQK1XB.jpeg)

<div align=center>
  <font size="3">
    <i>
      <a href="https://twitter.com/MVC_discord">Twitter@MVC_discord</a>
    </i>
  </font>
</div>



### 引言

GAMES202 高质量实时渲染是由闫令琪老师教授。

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

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210414010925520.png)







### What is GAMES202 about?

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210414153449049.png)

**Real-Time** High Quality Rendering

+ Speed: more than 30 FPS (frames per second), even more for Virtual / Augmented Reality (VR / AR): 90 FPS
+ Interactivity: Each frame generated on the fly

Real-Time **High Quality** Rendering

+ Realism: advanced approaches to make rendering more realistic
+ Dependability: all-time correctness (exact or approximate), no tolerance to (uncontrollable) failures



实时指的是一种速度，渲染中人们通常认为到达30FPS可以被称为实时，当然不同的领域有不同的标准，虚拟现实和增强现实会对实时的要求更高：90FPS。实时渲染讲究的是互动性，能够得到反馈肯定比一直渲染要好。

高质量也是需要强调的一点，指的是真实感，我们渲染的最终目标是以假乱真，但这个目标付出的代价很可能就是高额的计算。为了保证实时渲染，我们通常会牺牲一部分质量，但人们是贪婪的，如何两全其美也是实时渲染最大的挑战。



Real-Time High Quality **Rendering**

+ What is Rendering?

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210414161418776.png)



渲染是图形学的一个重要分支，它所做的事情是把一个三维的场景通过计算方式模拟光线如何从光源中发出并在场景中弹射最后进入人的眼睛的，我们在试图模拟一个虚拟的摄像机如何看到一个虚拟的场景，这就是渲染的事情。





Highest level: 4 different parts on real-time rendering

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210414161732806.png)



这门课我们会讲四个话题：阴影、全局光照、真实着色/基于物理着色以及实时光线追踪。



### Course Topics

+ Shadow and Environment Mapping
+ Interactive Global Illumination Techniques
+ Precomputed Radiance Transfer
+ Real-Time Ray Tracing





#### What is GAMES202 NOT about?

+ 3D modeling or game development using Unreal Engine (where can I learn them?)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210414220632404.png)



+ Expensive (but more accurate) light transport techniques in movies / animations (where can I learn this?)

![image-20210414221015811](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210414221015811.png)









+ Using OpenGL
+ Scene / shader optimization
+ Reverse engineering of shaders
+ High performance computing e.g. CUDA programming





### How to study GAMES202?

**Understand the difference between science and technology**

+ Science != technology
+ Science == knowledge
+ Technology == engineering skills that turn science into product

**Real-time rendering = fast & approximate offline rendering + systematic engineering**

**Fact: in real-time rendering technologies, the industry is way ahead of the academia**

**Practice makes perfect**



### Course Logistics





