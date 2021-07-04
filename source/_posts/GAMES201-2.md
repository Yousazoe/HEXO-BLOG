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

简单介绍一下显式和隐式时间寄存器的区别：

+ 显式寄存器的一大特点就是未来的状态只依赖于过去的状态，所以它非常容易实现，整个程序就是一个递推，从以前的时间推到未来的时间。显式寄存器有很多种，像RK等数值精度会更高一些。

  显式寄存器有一个不好的点是非常容易爆炸（计算误差无法随时间衰减，而是随时间爆炸性增长）：$\Delta t <= c \sqrt{\frac{m}{k}}$，这个公式可以看出来当一个粒子质量变得越来越大的时候它允许的$\Delta t$就会变大；同样当弹簧的劲度系数越来越大，允许的$\Delta t$也会越来越小。所以这个系统对于特别硬的弹簧并不适合

+ 中点法和后向欧拉属于隐式寄存器，未来不只依赖你的过去，还依赖你的未来，这就像鸡生蛋问题一样。隐式寄存器复杂很难实现，这意味着很难优化比如向量化。另外一个问题是由于每一个时间步变得昂贵，有的时候需要衡量带来的是加速还是反作用。





##### Mass-spring systems

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163613291.png)

对于我们的弹簧质点系统，时间寄存器又是如何呢？

上面是后向欧拉表述，我们假设在这个时间段内速度是恒定的。首先公式（1）里它的$x_{t+1}$依赖于$v_{t+1}$，公式（2）在说下一个时间段的速度等于上一个时间段的速度加$\Delta t$乘这个时间段的加速度，而加速度此时用的是$x_{t+1}$，相当于（1）依赖于（2），而（2）又依赖于（1）。这里的$M^{-1}$是质量矩阵的逆，推导为$a = M^{-1} M a = M^{-1}F$。

化简把（1）带入（2）里得到公式（3），我们可以发现这是一个非线性方程，其中$v_{t+1}$是未知，$v_t$和$x_{t}$都是知道的，非线性来自$f$。后面我们用泰勒展开一阶得到公式（4），或者可以称为线性化，整个系统变成线性的。



##### After linearization

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163547142.png)



把（4）搬过来变成（5），稍微移项整理一下得到公式（6），其中线性系统为最左边的$[I-\Delta t^2 M^{-1}\frac{\partial f}{\partial x}]$。



##### Solving the system

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163507504.png)



解线性系统在物理模拟里面是一个非常重要的问题，今天我们介绍最简单的 Jacobi 迭代，除此之外还有 Gauss-Seidel 迭代和共轭梯度。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163355214.png)



再整理一步得到上面的形式 $Av_{t+1}=b$。



##### Solving linear systems with Jacobi iterations

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163423495.png)



```python
import taichi as ti
import random

ti.init()

n = 20

A = ti.var(dt=ti.f32, shape=(n, n))
x = ti.var(dt=ti.f32, shape=n)
new_x = ti.var(dt=ti.f32, shape=n)
b = ti.var(dt=ti.f32, shape=n)

@ti.kernel
def iterate():
    for i in range(n):
        r = b[i]
        for j in range(n):
            if i != j:
                r -= A[i, j] * x[j]
                
        new_x[i] = r / A[i, i]
        
    for i in range(n):
        x[i] = new_x[i]

@ti.kernel
def residual() -> ti.f32:
    res = 0.0
    
    for i in range(n):
        r = b[i] * 1.0
        for j in range(n):
            r -= A[i, j] * x[j]
        res += r * r
        
    return res

for i in range(n):
    for j in range(n):
        A[i, j] = random.random() - 0.5

    A[i, i] += n * 0.1
    
    b[i] = random.random() * 100

for i in range(100):
    iterate()
    print(f'iter {i}, residual={residual():0.10f}')
    

for i in range(n):
    lhs = 0.0
    for j in range(n):
        lhs += A[i, j] * x[j]
    assert abs(lhs - b[i]) < 1e-4

```



Jacobi迭代就是每一次迭代把未知数的一项换成一个值，这个值能够使得右端项能够被满足，最终收敛回一个值。



##### Unifying explicit and implicit integrators

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163321604.png)



如果我们往刚才的公式加入一个$\beta$，那么就可以把 forward/backward Euler 整合到一起。



##### Solve faster

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163252015.png)



如果我们有成千上万个弹簧该怎么办：

+ 稀疏矩阵
+ 共轭梯度
+ 预条件



#### Lagrangian fluid simulation: Smoothed particle hydrodynamics

##### Smoothed particle hydrodynamics

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163218816.png)



接下来我们讲讲拉格朗日解流体的方法。

SPH 的主体思想是有一堆粒子，每个粒子携带一些物理量，用和函数去近似一个连续的长度。其中 $A$ 可以是任何随着空间变化的物理量，比如速度、压力等等。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163137329.png)



SPH 的方法一开始是用来求天体物理，它最大的好处是不需要 meshes，非常适合模拟自由表面流体。还有一个好处是非常直观容易理解，每一个粒子就是一小包水。



##### Implementing SPH using the Equation of States (EOS)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163055764.png)



那么用 SPH 模拟流体最简单的方法叫做 WCSPH，最关键的是 $v$ 对 $t$ 的导数，$D$ 是材料导数（可以认为是粒子对时间的导数）。

那么速度的导数是什么呢？首先液体里面得有压强 $p$，压强的梯度会影响流体粒子的速度，除以密度 $\rho$ 得到加速度。压强 $p$ 的公式中 $B$ 为体积模量，$\rho_0$ 为理想密度。直观上来说，$\rho$ 非常大压强 $p$ 就会非常高，推着周围的粒子离开自己，尝试保持自己的体积。





##### Gradients in SPH

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703163027501.png)



刚才提到 $A(x)$ 公式来去在每一个粒子处计算出粒子所在位置物理量是多少，算梯度 $SPH$ 有一套特别的算法。但是它其实并不能从上面推出来，而且梯度值也不是特别准确，但大家还用是因为至少在 $SPH$ 中它还是对称的，保证动量守恒。



##### SPH Simulation Cycle

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703162912483.png)

讲了这么多写一个 SPH 也非常容易，左边一个不考虑粘性的欧拉方程，右边是一个压强关于密度的关系。对于 SPH Simulation Cycle：

+ 对于每一个粒子计算局部的密度（粒子只携带质量，密度由质量估计）
+ 对于每一个粒子用梯度公式计算压强的梯度
+ Symplectic Euler！

可以看到最后的 Symplectic Euler 和弹簧质点系统是非常像的，甚至可以认为 SPH 里弹簧遵循的不是胡克定律而是这些物理关系。



##### Variants of SPH

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703162739473.png)



SPH 有很多很多变种，PCI-SPH 是一个隐式的时间积分，但又为了性能做了取舍不完全隐式，使用预测矫正的格式每次先预测粒子的位置和速度，然后再根据预测做出矫正，得到一个比较好散度比较小的速度场。

另一个非常流行的变种是 PBF



##### Courant–Friedrichs–Lewy (CFL) condition

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703162652790.png)



##### Accelerating SPH: Neighborhood search

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703162626157.png)





##### Other particle-based simulation methods

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703162525016.png)



##### Exporting your results

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210703162424358.png)

