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

GAMES201高级物理引擎实战是由胡渊鸣老师教授。本节主要简单讲解拉格朗日、欧拉两种视角，配合太极语言编写简单的弹簧质点系统。



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

我们先来试一下demo的效果；

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703203550055.png)



其中两个参数非常重要：

+ `stiffness` 弹簧硬度

  `s`调大以后整个材料坚如磐石，变得非常坚硬；`S`调小以后让材料变软

+ `damping` 阻尼系数

  `d` 调大以后显得非常粘滞， `D`调小以后运行更加灵活。很多游戏里面会把`damping`调的比较大



#### Mass-spring Systems

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703155855699.png)



这边我们给出一些数学公式，大家不要被吓到，其实它还是非常简单的，就是胡克定律和牛顿第二定律。

胡克定律就是`i`到`j`受力$f_{ij}$等于弹簧刚度`k`乘上现在两个质点它们的距离减去弹簧静止距离的差，最后算出的标量乘上两个质点力的单位向量，这样我们就得到了两个质点间的受力。

有了力我们就可以根据牛顿第二定律力除以质量求出速度的导数。这里$\frac{1}{m_i}$是提前取倒数，乘法效率比除法高，等到需要时再拿出来使用。





#### Time integration

下面我们来看看时间积分是怎么做的。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163832597.png)



刚才我们写出的方程全部是连续的，相当于是常微方程。如果要在计算机中表示就遇到了一个问题：计算机中的时间全部都是离散的，计算资源也全部都是离散的，不可能取一个无穷小的时间。

这个时候大家会取一个$\Delta t$，一般来说可以是一个比较小的值比如$10^{-3}$、$10^{-4}$，会根据物理系统的各种参数去取。大家会选择一个比较大的$\Delta t$，代表模拟同样长时间的物理过程跑得比较快，$\Delta t$越大越好。当然$\Delta t$大了以后又会带来许多不稳定性的问题，后面会提到。



我们做了离散化以后$v$就不再是连续的，下标表示$t$时刻的$v$，而$v_{t+1}$表示的是下一时间步的$v$。通过比较简单的前向欧拉法（根据现有状态推测以后的状态）我们可以得到一个简单的公式：$v_{t+1}=v_{t}+\Delta t \frac{f_t}{m}$，对于$x$我们用同样的方式处理。

但是Forward Euler用的不多了，现在大家用的比较多的是Semi-implicit Euler。它也是另一个根据现有状态推出未来的一种时间计算方式，可以看到两者的区别在于$x_{t+1}$使用的速度$v$不同。这看起来是一个小的差异，但其实很多时候有一个准确性的提升。





##### Implementing a mass-spring system with symplectic Euler

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163714942.png)

我们只要三步：

+ 首先计算新的速度$v_{t+1}$
+ 和地面做一次碰撞
+ 用新的速度计算一下新的位置$x_{t+1}$



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163745562.png)

```python
@ti.kernel
def substep():
    # Compute force and new velocity
    n = num_particles[None]
    for i in range(n):
        v[i] *= ti.exp(-dt * damping[None]) # damping
        total_force = ti.Vector(gravity) * particle_mass
        for j in range(n):
            if rest_length[i, j] != 0:
                x_ij = x[i] - x[j]
                total_force += -spring_stiffness[None] * (x_ij.norm() - rest_length[i, j]) * x_ij.normalized()
        v[i] += dt * total_force / particle_mass
        
    # Collide with ground
    for i in range(n):
        if x[i].y < bottom_y:
            x[i].y = bottom_y
            v[i].y = 0

    # Compute new position
    for i in range(num_particles[None]):
        x[i] += v[i] * dt
```



这个`substep`的`kernel`非常简单，首先它把所有的`i`枚举一遍，总受力为$G = mg$。接着我们枚举其他所有的粒子，看它们之间是否有联系，如果`rest_length[]`为0代表没有弹簧，否则它们之间有一个弹簧。最后我们按照胡克定律的公式算出粒子的受力，用力更新速度。

之后我们与地面做一次碰撞。为什么在中间和地面做一次碰撞呢？如果我们在计算速度以后再和地面做碰撞，有可能在计算速度的时候粒子陷到地底，这就不是很自然了，所以对于弹簧质点系统一般计算完力和速度之后立刻做一次碰撞。

接下来我们把速度累加到位置上就可以计算新的位置了。



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

