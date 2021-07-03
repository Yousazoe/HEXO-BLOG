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
mathjax: true
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

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703155855699.png)



这边我们给出一些数学公式，大家不要被吓到，其实它还是非常简单的，就是胡克定律和牛顿第二定律。

胡克定律就是`i`到`j`受力$f_{ij}$等于弹簧刚度`k`乘上现在两个质点它们的距离减去弹簧静止距离的差，最后算出的标量乘上两个质点力的单位向量，这样我们就得到了两个质点间的受力。

有了力我们就可以根据牛顿第二定律力除以质量求出速度的导数。这里$\frac{1}{m_i}$是提前取倒数，乘法效率比除法高，等到需要时再拿出来使用。





#### Time integration

下面我们来看看时间积分是怎么做的。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163832597.png)



##### Implementing a mass-spring system with symplectic Euler

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163714942.png)





![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163745562.png)





##### Explicit v.s. implicit time integrators

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163636950.png)



##### Mass-spring systems

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163613291.png)





##### After linearization

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163547142.png)





##### Solving the system

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163507504.png)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163355214.png)





##### Solving linear systems with Jacobi iterations

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163423495.png)







##### Unifying explicit and implicit integrators

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163321604.png)





##### Solve faster

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163252015.png)





#### Lagrangian fluid simulation: Smoothed particle hydrodynamics

##### Smoothed particle hydrodynamics

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163218816.png)







![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163137329.png)







##### Implementing SPH using the Equation of States (EOS)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163055764.png)





##### Gradients in SPH

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163027501.png)





##### SPH Simulation Cycle

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703162912483.png)





##### Variants of SPH

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703162739473.png)



##### Courant–Friedrichs–Lewy (CFL) condition

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703162652790.png)



##### Accelerating SPH: Neighborhood search

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703162626157.png)





##### Other particle-based simulation methods

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703162525016.png)



##### Exporting your results

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703162424358.png)

