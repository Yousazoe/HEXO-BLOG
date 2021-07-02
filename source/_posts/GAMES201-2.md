---
title: Lagrangian Simulation Approaches
comment: false
tags:
  - Computer Graphics
  - Physics
categories: 高级物理引擎实战 (GAMES201-Advanced Physics Engines)
abbrlink: 22a0791d
date: 2021-07-02 21:32:39
type:
banner_img:
index_img:
translate_title:
top:
mathjax:
---

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/E4v9qlcXEAUK9hf.jpeg)

<div align=center>
  <font size="3">
    <i>
      <a href="https://twitter.com/karyagart/status/1408498662326648841">Twitter@karyagart</a>
    </i>
  </font>
</div>



### 引言





<!--more-->





### 论坛问题

+ **代码格式化** `yapf` + `PEP8`

+ **论坛贴代码**（Markdown）

  ```markdown
  ​```python
  import taichi as ti
  ​```
  ```

+ **展示结果** 

  输出gif（这节课最后会提到细节） 

+ **Faster compilation**

  可以选择关闭高级优化，提高编译速度

  ```python
  ti.core.toggle_advanced_optimization(false)
  ```

  

### Lagrangian v.s. Eulerian

那么今天我们就来讲一讲基于物理动画的一些基本概念。说到基于物理模拟动画的介质，我们不得不谈到两个视角：拉格朗日视角和欧拉视角。





#### Lagrangian View

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210702221318783.png)

所谓的拉格朗日视角就是我们去模拟这个介质的时候想象我们在这个介质里面塞了很多很多随波逐流的小纸船，这些小纸船会跟着你的介质一起移动。由于小纸船跟介质一起移动，通常用拉格朗日视角去模拟各种介质的话可能会采用拉格朗日粒子或者三角网格，只要节点是随着材料一起动就是拉格朗日视角。

对于拉格朗日视角里面的节点，可以认为每一个节点就是一个很小的sensor，不断监测自己的位置和速度。



#### Eulerian View

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210702221435932.png)



欧拉视角放的这些sensor是永远不移动的，你可以认为它们是打在水里面的木桩。这些sensor不断检测穿过材料的速度是多少。有一句口诀是“拉格朗日随波逐流，欧拉岿然不动”可以方便大家记忆。



#### Continuum Simulation

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210702222632077.png)

通常来说，如果用拉格朗日视角你很可能在用这些粒子，欧拉视角很可能用网格（当然这不是绝对的）。





#### Continuum Simulation

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210702222835673.png)



当大家使用拉格朗日表示的时候最常见的是用各种各样的粒子。左边我们展示的是一个基于位置的动力学模拟，各种各样的粒子通过各种方式连接起来；右边是欧拉典型表示的烟雾模拟，一般是用一个网格，网格上的每一个点表示的是穿过这个点流体的速度。



#### Mass-Spring Systems

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210702223956163.png)

今天我们主要讲弹簧质点系统，它是一个非常非常简单的模型，但是非常非常的有用，可以模拟很多有意思的东西比如布料、头发、各种弹性的材料。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703001812224.png)

弹簧质点模型在游戏中依然有用。小时候玩过一款游戏叫做粘粘世界，这个游戏是要用它的质点模型，通过不断把它连接起来搭起一个桥，很有意思。





![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703001850057.png)







### Lagrangian Simulation Approaches

#### Mass-spring Systems







#### Time integration

