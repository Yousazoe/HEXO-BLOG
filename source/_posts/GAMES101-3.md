---
title: Transformation
comment: false
tags:
  - Computer Graphics
  - Math
  - Linear Algebra
categories: 现代图形学入门 (GAMES101-Introduction to Computer Graphics)
abbrlink: 3fd6625d
mathjax: true
date: 2021-03-27 10:28:14
type:
banner_img:
index_img:
translate_title:
top:
---





![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/ExYwvzlWUAA-EB8.jpeg)

<div align=center>
  <font size="3">
    <i>
      <a href="https://twitter.com/bktheone">Twitter@bktheone</a>
    </i>
  </font>
</div>





### 引言

GAMES101现代图形学入门是由闫令琪老师教授。这节课主要讲解为什么学习变换、二维空间的变换、齐次坐标以及三维空间的变换。

<!--more-->



### Why study transformation

+ Modeling
+ Viewing



变换可以表达各种各样的旋转以及它们互相错综复杂联系在一起之后的变换，上面提到两种变换：模型变换和视图变换。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210327110616510.png)



正如在本门课开始时所讲到的，光栅化成像也大量运用了变换。上面左图是一个人坐在室内向窗户外看，成像出来就是右图这样的二维平面，这个从三维转向二维的过程就是投影。



### 2D transformations

+ Representing transformations using matrices

- Rotation, scale, shear

二维变化最重要的是把变换和矩阵联系起来。



#### Scale

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210327130650404.png)



我们首先提到缩放变换，上图就是大家在ps中经常做的图像的缩放，这种缩放也是一种变换没有问题。如果我们用数学方法表示：$x'=sx$    $y'=sy$

对于这两个式子我们也可以写成矩阵的形式：

$\begin{bmatrix}x' \\\\ y'\end{bmatrix}=\begin{bmatrix}s & 0 \\\\ 0 & s\end{bmatrix}\begin{bmatrix}x \\\\ y\end{bmatrix}=\begin{bmatrix}sx + 0 \cdot y \\\\ 0 \cdot x + sy\end{bmatrix}=\begin{bmatrix}sx \\\\ sy\end{bmatrix}$

在这里$\begin{bmatrix}s & 0 \\\\ 0 & s\end{bmatrix}$被称为缩放矩阵，$s=0.5$就对应着横轴纵轴缩小一半的变换。



#### Scale(Non-Uniform)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210328200705165.png)



如果我们的缩放不是均匀的呢？当x和y缩放的比例各不相同如上图纵坐标没有变化，横坐标改变时，我们仍然可以依据该矩阵进行变换：

$\begin{bmatrix}x' \\\\ y'\end{bmatrix}=\begin{bmatrix}s_x & 0 \\\\ 0 & s_y\end{bmatrix}\begin{bmatrix}x \\\\ y\end{bmatrix}=\begin{bmatrix}s_x \cdot x + 0 \cdot y \\\\ 0 \cdot x + s_y \cdot y\end{bmatrix}=\begin{bmatrix}s_xx\\\\s_yy\end{bmatrix}$





#### Reflection Matrix

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210328201341212.png)



下面我们讲讲反射/对称，左图经过一个关于Y轴的翻转就可以得到右图。相对于Y轴翻转在数学上如何表达呢？

$x' = -x$

$y' = y$

很显然$x$进行了翻转，$y$并没有发生变换。我们同样可以用矩阵表示：

$\begin{bmatrix}x' \\\\ y'\end{bmatrix}=\begin{bmatrix}-1 & 0 \\\\ 0 & 1\end{bmatrix}\begin{bmatrix}x \\\\ y\end{bmatrix}=\begin{bmatrix}-1 \cdot x + 0 \cdot y \\\\ 0 \cdot x + 1 \cdot y\end{bmatrix}=\begin{bmatrix}-x \\\\ y\end{bmatrix}$



#### Shear Matrix

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210328202331302.png)



**Hints:**

+ Horizontal shift is 0 at $y=0$
+ Horizontal shift is a at $y=1$
+ Vertical shift is always 0



错切变换会比较难理解一些。我们可以想象拿到的图具有弹性，你可以拽着某一条边向右拉，然后会发现这张图会被拉歪成右上图这样。通过分析前后坐标间的关系，咱们发现竖直方向/纵坐标上没有发生变化，错切导致的拖拽发生在水平方向。我们盯着底下那条边，它水平方向前后并没有发生变化；而顶边每一点都移动了a个距离；如果我们再看中间那条$\frac{y}{2}$边移动了$\frac{a}{2}$，也就是说任何水平方向的移动都是$a \cdot y$：

$\begin{bmatrix}x' \\\\ y'\end{bmatrix} = \begin{bmatrix}1 & a \\\\ 0 & 1\end{bmatrix}\begin{bmatrix}x \\\\ y\end{bmatrix}=\begin{bmatrix}1 \cdot x + a \cdot y\\\\ 0 \cdot x + 1 \cdot y\end{bmatrix}=\begin{bmatrix}x + ay \\\\ y\end{bmatrix}$



从中可以看出我们要想写出一个变换，我们就要找一个对应（或者是前后之间的关系）。只要找到这个关系，我们就可以自然而然的写出变换矩阵。





#### Rotate

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210328204954129.png)



这里我们来谈谈更复杂但非常常见的变换：旋转变换。我们规定旋转变换是在二维平面内旋转，并且默认在原点进行旋转；另外不说旋转方向，我们默认逆时针方向。

既然是一种变换，那旋转的矩阵该如何写出来呢？我们可以看到旋转矩阵的结果：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210328205616158.png)



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210329121348717.png)





#### Linear Transforms = Matrices



$x' = ax + by$    $y' = cx + dy$

$x' = M x$    $\begin{bmatrix}x' \\\\ y'\end{bmatrix} = \begin{bmatrix}a & b \\\\ c & d\end{bmatrix}\begin{bmatrix}x \\\\ y\end{bmatrix}$



这里大家会发现有一个共同点，这些变换都可以写成上面的矩阵形式。如果我们可以把变换写成这样一种形式，也就是矩阵去乘输入的坐标可以得到输出的坐标，这种变化我们起个名字叫做线性变换。

需要注意的是必须是相同维度的矩阵来乘向量，在后面会提到。





### Homogeneous coordinates

+ Why homogeneous coordinates
+ Affine transformation



#### Translation

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210328212144952.png)



为什么要提到齐次坐标？我们为什么要引入这么复杂的东西？有一种变换它非常特殊：平移变换。上图进行了平移（x方向`tx`、y方向平移`ty`），我们可以很快写出对应关系：

$x' = x + t_x$

$y' = y + t_y$

写出来是挺简单的，但好像有个问题，我们不能和刚才一样写成矩阵的形式。



#### Why Homogeneous Coordinates

+ Translation cannot be represented in matrix form

  $\begin{bmatrix}x' \\\\ y'\end{bmatrix} = \begin{bmatrix}a & b \\\\ c & d\end{bmatrix}\begin{bmatrix}x \\\\ y\end{bmatrix} + \begin{bmatrix}t_x \\\\ t_y\end{bmatrix}$ 

  **(So, translation is NOT linear transform!)**

+ But we don’t want translation to be a special case

+ Is there a unified way to represent all transformations? (and what’s the cost?)



根据之前矩阵的乘法我们可以知道$\begin{bmatrix}a & b \\\\ c & d\end{bmatrix}\begin{bmatrix}x \\\\ y\end{bmatrix}$得到的结果一定是$mx+ny$，这个矩阵并不能表示类似之前加减的操作，必须通过加上$\begin{bmatrix}t_x \\\\ t_y\end{bmatrix}$来表达。由此可知，平移变换并不属于线性变换的范畴，而是一个特殊的变换。

但我们并不想把平移当作特殊的变换，有没有办法把所有的变换用一种最简单的形式去表示？



#### Solution: Homogenous Coordinates

**Add a third coordinate (w-coordinate)**

+ *2D point* = $(x, y, 1)^T $
+ *2D vector* = $(x, y, 0)^T$ 



**Matrix representation of translations**

$\begin{pmatrix}x' \\\\ y' \\\\ w'\end{pmatrix} = \begin{pmatrix}1 & 0 & t_x \\\\ 0 & 1 & t_y \\\\ 0 & 0 & 1\end{pmatrix} \cdot \begin{pmatrix}x \\\\ y \\\\ 1\end{pmatrix}=\begin{pmatrix}x + t_x \\\\ y + t_y \\\\ 1\end{pmatrix}$

**What if you translate a vector?**

人们在长期的斗争中引入了新的形式来表示物体的坐标，二维的点或向量可以增加一个维度。通过矩阵的运算我们可以发现平移操作可以通过矩阵乘向量的形式表现出来。这样我们引入齐次坐标最大的目的达到了，通过增加一个数来把平移变换包含进来。

有人可能会问为什么点和向量要区别出来。回想之前我们讲的概念，向量表示的是方向性，具有平移不变性，而这时我就希望它不会因为平移的`t_x`、`t_y`而发生改变，在矩阵的形式中就是$w$。



#### Homogenous Coordinates

**Valid operation if w-coordinate of result is 1 or 0**

+ *vector + vector = vector*

+ *point – point = vector*

+ *point + vector = point*

+ *point + point = ??* 

**In homogeneous coordinates,** 

$\begin{pmatrix}x \\\\ y \\\\ w\end{pmatrix}$ is the 2D point $\begin{pmatrix}x/w \\\\ y/w \\\\ 1\end{pmatrix},w\ne 0$



从这个定义上说，*point + point*在齐次坐标中表示的是这两个点的中点，推导的重点在于$w=2$：

$\begin{pmatrix}x_1 \\\\ y_1 \\\\ 1\end{pmatrix}+\begin{pmatrix}x_2 \\\\ y_2 \\\\ 1\end{pmatrix}=\begin{pmatrix}x_1 + x_2 \\\\ y_1 + y_2\\\\ 2\end{pmatrix} \to \begin{pmatrix}\frac{x_1 + x_2}{2} \\\\ \frac{y_1 + y_2}{2} \\\\ 1\end{pmatrix}$





### Affine Transformations

+ Affine map = linear map + translation 

  $\begin{pmatrix}x' \\\\ y'\end{pmatrix} = \begin{pmatrix}a & b \\\\ c & d\end{pmatrix} \cdot \begin{pmatrix}x \\\\ y \end{pmatrix} + \begin{pmatrix}t_x \\\\ t_y\end{pmatrix}$

+ Using homogenous coordinates:

  $\begin{pmatrix}x' \\\\ y' \\\\ 1\end{pmatrix} = \begin{pmatrix}a & b & t_x \\\\ c & d & t_y \\\\ 0 & 0 & 1\end{pmatrix} \cdot \begin{pmatrix}x \\\\ y \\\\ 1\end{pmatrix}$



对于任何一种变换我们可以起一个仿射变换的名字。所有的放射变换都可以写成齐次坐标的形式，我们只需要用一个矩阵就可以得到新的向量，用一个矩阵统一了所有的操作。



#### 2D Transformations

+ Scale $S(S_x,S_y) = \begin{pmatrix}s_x & 0 & 0 \\\\ 0 & s_y & 0 \\\\ 0 & 0 & 1\end{pmatrix}$
+ Rotation $R(\alpha) = \begin{pmatrix}\cos{\alpha} & -\sin{\alpha} & 0 \\\\ \sin{\alpha} & \cos{\alpha} & 0 \\\\ 0 & 0 & 1\end{pmatrix}$ 
+ Translation $T(t_x,t_y)=\begin{pmatrix}1 & 0 & t_x \\\\ 0 & 1 & t_y \\\\ 0 & 0 & 1\end{pmatrix}$

这样一来线性变换统一写成这样的形式。然而天下没有免费的午餐，它的代价就是它引入了额外的数字，但观察可以发现最后一行基本都是$\begin{pmatrix}0 & 0 & 1\end{pmatrix}$（二维仿射变换），理论上只需存储前面的就可以了，存储上并没有付出很大的代价，是一个非常好的发明。



#### Inverse Transform

$M^{-1}$ is the inverse of transform $M$ in both a matrix and geometric sense

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210329152723166.png)



逆变换就是把操作反过来。比如左上图我们经过$M$变换变成了右上的图，如果我们想变换回原来的形状，应该经历原来变换的逆变换$M^{-1}$，这个逆变换在数学上正好对应乘以变换的逆矩阵，而逆矩阵就是乘以本身等于单位矩阵。





#### Composing Transforms

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210329153815046.png)



我们再来讨论讨论组合变换。上面左图通过某些变换到了右图，那么我们自然而然就要问这个变换是怎么得到的呢？



**Translate Then Rotate?**

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210329154038371.png)



我们可以先让这个图平移一个单位$T(1,0)$，然后再旋转45度$R_{45}$我们就可以得到最右，但与我们的示意图不对，并不是我们想要的结果，这个尝试不成功。



**Rotate Then Translate**

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210329154056891.png)



我可以先做一个旋转操作$R_{45}$，然后再把它平移一个单位$T(1,0)$，通过这样一个组合方式得到了我们想要的结果。这里提到两个事情：

1. **复杂的变换可以通过一系列简单的变换得到**
2. **变换的顺序是非常重要的**

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210329161609918.png)





#### Transform Ordering Matters!

**Matrix multiplication is not commutative** 

$R_{45} \cdot T_{(1,0)} \ne T_{(1,0)} \cdot R_{45}$

**Note that matrices are applied right to left:**

$T_{(1,0)} \cdot R_{45} \begin{bmatrix}x \\\\ y \\\\ 1\end{bmatrix} = \begin{bmatrix}1 & 0 & 1 \\\\ 0 & 1 & 0 \\\\ 0 & 0 & 1 \end{bmatrix}\begin{bmatrix}\cos{45^{\circ}} & -\sin{45^{\circ}} & 0 \\\\ \sin{45^{\circ}} & \cos{45^{\circ}} & 0 \\\\ 0 & 0 & 1\end{bmatrix}\begin{bmatrix}x \\\\ y \\\\ 1\end{bmatrix}$



矩阵乘法不满足交换律刚才已经证明了，这里着重提到对于列向量运算**从右到左**的。





**Sequence of affine transforms A1, A2, A3, ...**

+ Compose by matrix multiplication
+ Very important for performance!

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210329165247073.png)



这个概念是可以推广的，如果有一个点我们连续应用很多不同的变换($A_1,A_2...A_n$)，那么我们从右到左应用。虽然矩阵没有交换律，但有结合律，所以我们可以把这些变换矩阵先乘起来，最后再与向量作用，这也意味着仅需要$3 \times 3$的矩阵我们可以表达非常复杂的变换。





#### Decomposing Complex Transforms

**How to rotate around a given point c?** 

1. Translate center to origin
2. Rotate
3. Translate back

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210329175445273.png)



**Matrix representation?**

$T(c) \cdot R(\alpha) \cdot T(-c)$



变换不止能合成，还能分解，当我们在猜测先平移还是先旋转的时候已经是在做分解这件事了。

之前我们提到过旋转默认按原点旋转，那如果我们以任意点$c$为中心进行旋转而不受限于原点呢？我们可以先把对应的点移到原点去$T(-c)$，在原点进行旋转$R(\alpha)$后，再从原点移回去$T(c)$。





<br/>

<center>{% btn https://sites.cs.ucsb.edu/~lingqi/teaching/resources/GAMES101_Lecture_03.pdf,  GAMES101_Lecture_03, fas fa-download %}</center>

