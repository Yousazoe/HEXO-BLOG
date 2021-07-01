---
title: 导论
comment: false
tags:
- Computer Graphics
- Physics
categories: 高级物理引擎实战 (GAMES201-Advanced Physics Engines)
abbrlink: ee59981a
date: 2021-07-01 13:45:14
type:
banner_img:
index_img:
translate_title:
top:
mathjax:
---

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/E4xJme9VUAEI0Cd.jpeg)

<div align=center>
  <font size="3">
    <i>
      <a href="https://twitter.com/AsyranHazwan/status/1408582367187398656">Twitter@AsyranHazwan</a>
    </i>
  </font>
</div>





### 引言

GAMES201高级物理引擎实战是由胡渊鸣老师教授。本节主要讲述了老师与物理引擎的故事、太极编程语言以及该系列课程内容的介绍。

<!--more-->



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701135720064.png)





### Physics Engine

> “A physics engine is computer software that provides an approximate simulation of certain physical systems, such as rigid body dynamics (including collision detection), soft body dynamics, and fluid dynamics, of use in the domains of computer graphics, video games and film.”
>
> —— https://en.wikipedia.org/wiki/Physics_engine

我们开门见山定义一下什么是物理引擎。在维基百科上可以看到物理引擎是一个计算机软件，它提供对物理系统近似的模拟，比如刚体物理的动力学、软体动力学以及流体动力学。主要的应用是在计算机图形、游戏和电影。



> Simulate the world in your computer!

这么长的定义换成一句话说就是在电脑里模拟这个世界。



### Application

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701140427097.png)



除了刚才说到的这些应用，它还可以应用在工业软件中，在计算机中完成测试迭代；还有一个很重要的应用是电影的视觉特效，基本每个动画电影都有非常多的镜头用物理效果模拟出来的；虚拟现实和增强现实更不用多说，如果在VR里有一个真实的物理世界，那么沉浸感会增强很多，虚拟世界和现实世界的物理规律是一致的。

当然，大家最关心的物理引擎的用途还是在游戏里面，所以今天就仔细讲一讲游戏。



#### The Incredible machines

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701141208877.png)



很小的时候就玩过很多游戏，它们构成了我童年的很大一部分，有一个我印象比较深的游戏叫做“不可思议的机器人”。这个游戏你可以摆入各种各样神奇的道具，模拟物理效果。



#### Angry Birds

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701141535906.png)

愤怒的小鸟也是一款很经典的游戏。你可以通过拖拽弹弓，小鸟撞到游戏里各种障碍物，里面的猪碰到障碍物就会被消灭掉。



#### Phun (Algodoo)

另外一个更可定制一点的是纯物理引擎，不是游戏。它可以在里面放齿轮、滑轮、棱镜等等，你可以在里面创建一个物理世界。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701141847711.png)



#### Besieged

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701142035182.png)

15年的时候又有一款比较有意思的游戏：围攻。你可以自己把各种个样的模块把它组装成一个攻城武器，去攻打各种各样的城池。





### My Own Physical Simulation Story

下面我讲讲自己和物理引擎的故事，从初中二年级到博士三年级（2009～2020）。



#### My first physics engine

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701142530213.png)

上图是09写的第一个物理引擎，其实非常简单，就是一个弹簧质点系统。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701142831662.png)







#### My own rigid body simulator

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701143209742.png)

这是高中时候做的，那时学了一点刚体动力学，受到愤怒的小鸟的影响写了一个刚体物理引擎。





#### My rigid body game

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701143701106.png)

这是大二写的基于物理引擎的游戏。



#### My fluid simulator

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701143946655.png)

大概16年的时候写了流体的模拟。



#### My smoke simulator

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701144022754.png)

17年的时候写了烟的模拟。



#### My continuum + cutting simulator

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701144336903.png)



这是我第一篇SIGGRAPH，做的是切割的模拟，实现了固体和液体显示的耦合。



#### Differentiable Simulation

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701144836220.png)



最近在搞可微模拟，希望求出初始状况的扰动对结果的影响。



#### Now

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701144953922.png)



### Keywords of this course

#### Discretization

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701145142621.png)



我们会简单讲讲各种各样的离散化，不会讲的特别深。因为自己是计算机方面的，所以更多会从程序员的角度讲讲怎样直观的理解各种各样的离散化。



#### Efficient Solvers

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701145338319.png)

我们会讲怎样写有效率的求解器，后面我们会详细介绍。



#### Productivity

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701164745250.png)



同样我们会讲讲怎么会提高生产力，怎么样用比较短的代码实现一个高效metric。





#### Performance

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701172105296.png)

当然我们也很在意性能，刚才提到很多模拟我们要等上一天的时间。





#### Hardware architecture

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701172240794.png)



我们也会简单介绍一下硬件的体系结构，因为如果你要写高性能求解器，需要去了解硬件是什么样子的，否则很难把它全部利用起来。



#### Data Structures

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701172608321.png)



还有一些复杂的数据结构，太极语言让这些数据结构的使用变得更加简单，后面我们会详细介绍。



#### Parallelization

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701173008944.png)



我们也会讲讲怎么去做复杂的并行，因为现在并行硬件大行其道，CPU和GPU如果算吞吐量真的是天壤之别，一般能差上一个数量级。





#### Differentiability

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701173318387.png)





最后我们会讲讲怎么求simulation的导数，做很多有意思的东西。







### Taichi Programming Language Introduction

#### Overview

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701173956881.png)



#### What is Taichi?

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701174147153.png)



什么是太极呢？太极是一个高性能领域特定语言，它嵌入在python里面，所以它的语法和python非常非常的像，如果你会python，那么可以很快上手太极。

这门语言是专门用于计算机图形学而设计的，我们在设计的时候非常非常注重生产力和可移植性，这两个东西以前在计算机图形学里面是非常难以做到的。这里的生产力不是说游戏引擎，而是针对想研究图形学算法的人。





#### Getting started

##### Installation

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701174726967.png)



我们先来看看如何安装。如果你有Python 3.6+可以直接用以下命令安装太极：

```shell
python3 -m pip install taichi
```



三个主流的操作系统都是支持的，太极程序既可以在CPU上运行又可以在GPU上运行（支持CUDA、OpenGL、Apple Metal）。如果你的CPU是一些神奇的配置或Python是3.9以上，那么需要下载太极源代码下来装了。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701181803381.png)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701192234480.png)



##### Initialization

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701192900786.png)

初始化太极非常重要，每当你运行一个太极程序的时候总是调用一下：

```python
import taichi as ti

ti.init(arch=ti.cuda)
```



其中`arch`可以选择在什么硬件上跑，建议大家使用`ti.cpu`或`ti.gpu`。





#### Data

##### Data types

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701212446360.png)



太极里支持的数据类型和C非常像，它有8、16、32、64位的整型，整型里又分为带符号的和不带符号的，还有32、64位的浮点数类型。

目前太极不支持`bool`类型：`true`、`false`，所有的比较返回值都是用整型存储。当然并不是所有的后端都支持所有的类型，因为比如OpenGL可能不支持64位的整数和浮点数，文档中有一个表详细写了每个后端支持什么样的数据类型。



##### Tensors

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701225455668.png)

接下来我们介绍数据里最重要的概念Tensors，一般来讲可以认为张量就是高维数组。你可以认为0维张量就是标量，1维的张量就是向量，2维的张量是一个矩阵，在太极中张量和矩阵会严格区分，是两个完全不一样的概念。

```python
import taichi as ti
ti.init()

a = ti.var(dt=ti.f32, shape=(42, 63))           # A tensor of 42x63 scalars
b = ti.Vector(3, dt=ti.f32, shape=4)            # A tensor of 4x 3D vectors
C = ti.Matrix(2, 2, dt=ti.f32, shape=(3, 5))    # A tensor of 3x5 2x2 matrices

loss = ti.var(dt=ti.f32, shape=())              # A (0-D) tensor of a single scalar

a[3, 4] = 1
print('a[3, 4] = ', a[3, 4])                    # "a[3, 4] = 1.000000"

b[2] = [6, 7, 8]
print('b[0] = ', b[0][0], b[0][1], b[0][2])     # print(b[0]) is not yet supported

loss[None] = 3
print(loss[None])                               # 3
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210701232400669.png)







#### Computation





#### Debugging
