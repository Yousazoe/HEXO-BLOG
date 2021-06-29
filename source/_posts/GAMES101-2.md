---
title: Review of Linear Algebra
comment: false
tags:
  - Computer Graphics
  - Math
  - Linear Algebra
categories: 现代图形学入门 (GAMES101-Introduction to Computer Graphics)
abbrlink: e520f1c
date: 2021-03-25 16:14:44
type:
banner_img:
index_img:
translate_title:
top:
mathjax: true
---



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/Ew1VB9XW8AAFL2s.jpeg)

<div align=center>
  <font size="3">
    <i>
      <a href="https://twitter.com/m4ndrill">Twitter@m4ndrill</a>
    </i>
  </font>
</div>





### 引言

GAMES101现代图形学入门是由闫令琪老师教授。本节主要讲解向量与线性代数，包括向量的点积、叉积以及矩阵的乘法、转置和逆运算。

<!--more-->



> A **Swift** and **Brutal**   
>
> Introduction to Linear Algebra!
>
> (in fact it’s relatively easy...)





图形学其实依赖很多东西，咱们这节课主要是说线性代数，可以看到标题十分恐怖，但线性代数本身并不难，复习起来比较简单没什么问题。



### Graphics’ Dependencies

**Basic mathematics**

+ Linear algebra, calculus, statistics

**Basic physics**

+ Optics, Mechanics

**Misc**

+ Signal processing
+ Numerical analysis

**And a bit of aesthetics**



图形学依赖于线性代数，也有诸如微积分、统计这些基础数学。不仅如此，还有基础物理涉及光学和力学，并且随着图形学发展大家越来越看重更高深的物理学知识比如波动光学的研究。

还涉及到一些杂七杂八的东西，这里特别提到信号处理，因为很多情况下我们要分析走样与反走样，这背后解决的其实是信号处理的问题。另外数值分析也非常重要的事情，有时图形学就是在解决复杂的数学计算问题，比如渲染就是解一个递归定义的积分，模拟或仿真则很多时候在解有限元问题或者扩散方程之类的事情。

除此之外，图形学还需要一点点美学，大家做出来的东西都希望好看一些，所以一点点美感还是需要的。



### This Course

**More dependent on Linear Algebra**

+ Vectors (dot products, cross products, ...)
+ Matrices (matrix-matrix, matrix-vector mult., ...)



**For example**

+ A point is a vector (?)
+ An operation like translating or rotating objects can be matrix-vector multiplication



线性代数我们主要说一些向量、矩阵这些操作，向量就是点乘叉乘，矩阵就是矩阵与矩阵的乘积、矩阵和向量的乘积。比如图形学里面表示空间中的一个点有三个坐标`x`、`y`、`z`，我们用三个数来表示，这其实就是一种向量表示，还包括平移、旋转、缩放这种操作都可以表示成矩阵和向量的乘积。



### Vector

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210325193030642.png)

+ Usually written as $\vec {a}$ or in bold $a$ !
+ Or using start and end points $\vec {AB} = B - A$
+ Direction and length
+ No absolute starting position

数学上一般叫向量，物理上更喜欢称为矢量，它表示的是一个方向，用粗体表示。向量具有方向和长度属性，例如$\vec {AB}$表示的就是从A指向B的方向。平移向量表示的都是一个向量，指向同一个方向就是同一个向量，在向量中我们并不关心绝对位置。



#### Vector Normalization

**Magnitude (length) of a vector written as** $||\vec a||$

**Unit vector**

+ A vector with magnitude of 1
+ Finding the unit vector of a vector (normalization): $\hat a=\vec a / ||\vec a||$
+ Used to represent directions

向量的长度可以给我提供单位向量，它的长度表示为1。原始的向量除以它的长度可以得到单位向量：$\hat a=\vec a / ||\vec a||$，在图形学中一般用单位向量表示方向，不关心它的长度。



#### Vector Addition

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210325195031185.png)

+ Geometrically: Parallelogram law & Triangle law
+ Algebraically: Simply add coordinates

向量有很多基本操作，其中最简单的是向量求和。给出向量$\vec {a}$和$\vec {b}$，求$\vec a + \vec b$有平行四边形法则和三角形法则两种几何求解方法，代数上直接将坐标相加即可。





#### Cartesian Coordinates

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210325200455697.png)

X and Y can be any (usually orthogonal unit) vectors.

$A = \begin{pmatrix} x \\\\ y\end{pmatrix}$  $\space A^T=\begin{pmatrix}x,y\end{pmatrix}$  $\space ||A||=\sqrt{x^2 + y^2}$

这个例子同样是一个向量**A**，大家会看到有一个坐标系在这里，X向右Y向上。这里是用直角坐标系或者笛卡尔坐标系来描述这个向量，我就认为这个向量从原点开始，沿着X有一些单位向量向右走，沿着Y有一些单位向量向上走，那么向量**A**我们就可以用几个X加几个Y定义。

这样做的好处在于我们可以直接用$(4,3)$来表示这么一个向量，并且向量长度也易于计算，在这里向量**A**的长度为$||A||=\sqrt{4^2+3^2}=5$。在图形学中没有特殊声明默认列向量。



#### Vector Multiplication

##### Dot product

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210325202105379.png)

For unit vectors: $\cos{\theta}=\hat{a} \cdot \hat{b}$

向量的乘法和数字的乘法不太一样，向量的点乘定义为两者长度与其夹角的余弦的乘积：$\vec{a} \cdot \vec{b} = ||\vec a|| ||\vec b|| \cos{\theta}$。有一点需要注意的是两个向量点乘结果是一个数量。

点乘的应用主要在对点乘定义的变化，比如将夹角余弦放在一边其余放在另一边：$\space \cos{\theta} = \frac{\vec a \cdot \vec b}{||\vec a||||\vec b||}$，也就是说给定两个向量可以算出两个向量夹角的余弦，进一步可以快速算出夹角的角度。有一个特殊情况，当两个向量都是单位向量时它们的长度都是1，公式可以简化为$\cos{\theta}=\hat{a} \cdot \hat{b}$。



**Properties**

$\vec a \cdot \vec b = \vec b \cdot \vec a$    $\space \vec a \cdot (\vec b + \vec c) = \vec a \cdot \vec b + \vec a \cdot \vec c$    $(k \vec a) \cdot \vec b = \vec a \cdot (k\vec b) = k(\vec a \cdot \vec b)$

点乘本身作为一种运算有各种各样的性质，比如满足交换律、结合律和分配律。



**Component-wise multiplication, then adding up**

+ In 2D

  $\vec a \cdot \vec b = \begin{pmatrix}x_a \\\\ y_a\end{pmatrix}\begin{pmatrix}x_b \\\\ y_b\end{pmatrix} = x_ax_b + y_ay_b$

+ In 3D

  $\vec a \cdot \vec b = \begin{pmatrix}x_a \\\\ y_a \\\\ z_a\end{pmatrix} \cdot \begin{pmatrix}x_b \\\\ y_b \\\\ z_b\end{pmatrix} = x_ax_b + y_ay_b + z_az_b$

在直角坐标系下，点乘的运算会更加简单，对应元素的乘积相加即可。



**Dot Product in Graphics**

+ Find angle between two vectors  
   (e.g. cosine of angle between light source and surface)
+ Finding **projection** of one vector on another

点乘在图形学中最大的作用是找到两个向量间的夹角，特别是之后我们在做光照模型时夹角的计算就是通过点乘来运算的。



**Dot Product for Projection**

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210325211858208.png)

**$\vec{b_{\perp}}$：projection of $\vec b$ onto** $\vec b$

+ $\vec{b_{\perp}}$ must be along $\vec a$ (or along $\hat a$)

**What's its magnitude k?**

+ $k = ||\vec{b_{\perp}}||=||\vec b||\cos{\theta}$



点乘另外一个用途是找到向量投影到另一个向量长什么样，比如上图我们想把$\vec b$投影到$\vec a$上，$\vec{b_{\perp}}$可以理解为阴影。

既然是$\vec b$投影在$\vec a$上，那么$\vec{b_{\perp}}$一定与$\vec a$方向相同，所以我们一定可以将这个$\vec{b_{\perp}}$用$\vec a$表示，算出其长度即可。投影意味着直角三角形存在，根据三角函数可以很轻松的算出来。



**Dot Product in Graphics**

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210325225832123.png)

+ Measure how close   two directions are
+ Decompose a vector
+ Determine forward /   backward



投影可以让我们把一个向量分解成两个向量，其中一个方向平行于某个方向，一个方向垂直于某个方向。比如说这里我们知道$\vec{b_{\perp}}$怎么算，那另外一个方向的向量就可以表示为$\vec b - \vec{b_{\perp}}$，所以点乘可以把向量进行任意的平行与垂直的分解。





![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210325230758136.png)

+ Measure how close   two directions are
+ Decompose a vector
+ Determine forward /   backward



在图形学中点乘还可以通过计算点乘的结果计算两个方向向量有多么接近，还可以告诉大家前与后的信息。如果有一个向量**a**给定了方向，从**a**的起点向上/下面方向看过去各会形成一个半圆，在这里圆被分成了两部分，可以看到**b**被视为与**c**同方向，而**c**则是相反方向。

那我们该如何判断呢？点乘就是一个有效的手段，通过判断点乘的正负可以轻松判断。







##### Cross product

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210326081102970.png)



+ Cross product is orthogonal to two initial vectors
+ Direction determined by right-hand rule
+ Useful in constructing coordinate systems (later)



叉乘和点乘是完全不一样的计算，它会输入两个不同的向量计算出另外一个向量。通过右手定则我们可以得到叉乘的方向，可以发现$a \times b$与$b \times a$不同。

因为其相互垂直的特性，叉积可以让我们创建出三维空间中的直角坐标系。



**Cross product: Properties**

$\vec x \times \vec y = + \vec z \\\\$
$\vec y \times \vec x = - \vec z \\\\$
$\vec y \times \vec z = + \vec x \\\\$
$\vec z \times \vec y = - \vec x \\\\$
$\vec z \times \vec x = + \vec y \\\\$
$\vec x \times \vec z = - \vec y$


如果熟悉右手螺旋定则，上面这些都可以推导出来，我们只需要记住第一个$\vec x \times \vec y = \vec z$即可。同样的，这样的坐标系也称为右手坐标系，而OpenGL和一些图形API会使用左手坐标系。



$\vec a \times \vec b = - \vec b \times \vec a \\\\$
$\vec a \times \vec a = \vec 0 \\\\$
$\vec a \times (\vec b + \vec c) = \vec a \times \vec b + \vec a \times \vec c \\\\$
$\vec a \times (k\vec b) = k(\vec a \times \vec b)$

上面有一些不同的性质，叉乘没有交换律需要加负号，分配律和结合律仍然存在。



**Cross Product: Cartesian Formula?**

$\vec a \times \vec b = \begin{pmatrix}y_az_a - y_bz_a \\\\ z_ax_b - x_az_b \\\\ x_ay_b - y_ax_b\end{pmatrix}$

Later in this lecture：

$\vec a \times \vec b = A^*b = \begin{pmatrix}0 & -z_a & y_a \\\\ z_a & 0 & -x_a \\\\ -y_a & x_a & 0\end{pmatrix}\begin{pmatrix}x_b \\\\ y_b \\\\ z_b\end{pmatrix}$

代数上叉乘也可以非常明确的写出来，多说一句，在之后的学习中我们还可以将叉乘表示成矩阵形式，$\vec a$写成一个对应的矩阵，这个矩阵乘向量$\vec b$，也可以得到相同的结果。



**Cross Product in Graphics**

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210326084020874.png)

+ Determine left/right
+ Determine **inside/outside**

叉乘在图形学中非常重要，这里我列举了判定左右和里外的例子。比如给定两个向量**a**和**b**在XY平面中，那么通过右手螺旋定则可以求得$\vec a \times \vec b>0$，那么**b**在**a**的左侧，并且**a**在**b**的右侧。

叉积的另一个应用是判断里和外。直接的例子就是下面的三角形ABC，有一个P点，我想知道它是否在三角形内部。这个问题我们就需要叉积：$\vec{AB} \times \vec{AP} > 0$、$\vec{BC} \times \vec{BP} > 0$和$\vec{CA} \times \vec{CP}>0$，这就说明P在三角形内部，否则一定有一个边在P点左侧。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210326084400759.png)





##### Orthonormal bases and coordinate fra

**Important for representing points, positions, locations**

**Often, many sets of coordinate systems**

+ Global, local, world, model, parts of model (head, hands, ...)

**Critical issue is transforming between these systems/ bases**

+ A topic for next week



**Orthonormal Coordinate Frames**

+ Any set of 3 vector (in 3D) that

  $||\vec u|| = ||\vec v|| = ||\vec w|| = 1$

  $\vec u \cdot \vec v = \vec u \cdot \vec w = \vec u \cdot \vec w = 0$

  $\vec w = \vec u \times \vec v \space (right-handed)$ 

$\vec p = (\vec p \cdot \vec u)\vec u + (\vec p \cdot \vec v)\vec v + (\vec p \cdot \vec w)\vec w$



这样做有什么好处呢？我们可以通过投影把任意向量分解到这三个方向，投影长度可以用单位向量快速表示。



### Matrices

**Magical 2D arrays that haunt in every CS course**

**In Graphics, pervasively used to represent transformations**

+ Translation, rotation, shear, scale (more details in the next lecture)



几乎所有计算机类课程都会涉及到矩阵的一些操作，在变换上矩阵其实挺简单的，在后面我们会用矩阵表示平移、旋转、缩放、错切等等。



#### What is a matrix

+ Array of numbers (m × n = m rows, n columns)

  $\begin{pmatrix}1 & 3 \\\\ 5 & 2 \\\\ 0 & 4\end{pmatrix}$

+ Addition and multiplication by a scalar are trivial:  element by element



矩阵就是一堆数安排成几行几列的结构，例如上面的矩阵是3行2列，所以我们表示为$3 \times 2$。



#### Matrix-Matrix Multiplication

+ \# (number of) columns in A must = # rows in B  (M x **N**) (**N** x P) = (M x P)

$\begin{pmatrix}1 & 3 \\\\ 5 & 2 \\\\ 0 & 4\end{pmatrix}\begin{pmatrix}3 & 6 & 9 &4 \\\\2 &7 & 8 & 3\end{pmatrix}=\begin{pmatrix}9 & ? & 33 & 13 \\\\ 19 & 44 & 61 & 26 \\\\ 8 & 28 & 32 & ?\end{pmatrix}$

+ Element (i,j) in the product is

  the dot product of **row i from A** and **column j from B**



给定两个矩阵判断是否能相乘，来看上面的矩阵分别是3行2列和2行4列，也就是第一个矩阵的列数必须等于第二个矩阵的行数，乘的结果也很明白，最后是第一个矩阵的行数与第二个矩阵的列数的矩阵。

确定好矩阵的大小，相乘后新的矩阵每个元素又该如何求解呢？比如上面的26是2行4列，那么我们就去找第2行和第4列分别是在各自的矩阵求点积：$5 \times 4 + 2 \times 3 = 26$



**Properties**

+ **Non-commutative** 

  ($AB$ and $BA$ are different in general)

+ Associative and distributive

  $(AB)C=A(BC)$

  $A(B + C) = AB +AC$

  $(A + B)C = AC + BC$

属性中结合律存在，但不能对调顺序，交换律不成立。



+ Treat vector as a column matrix (m×1)

+ Key for transforming points (next lecture)

+ Official spoiler: 2D reflection about y-axis

  $\begin{pmatrix}-1 & 0 \\\\ 0 & 1\end{pmatrix}\begin{pmatrix}x \\\\ y\end{pmatrix} = \begin{pmatrix}-x \\\\ y\end{pmatrix}$



下节课一个最简单的变换就是二维中以Y轴对称操作，X取反Y不变。什么样的矩阵可以做到这件事呢？上面这个矩阵就可以做到，这里简单提一下就可以。



#### Transpose of a Matrix

+ Switch rows and columns (ij -> ji)

  $\begin{pmatrix}1 & 2 \\\\ 3 & 4 \\\\ 5 & 6\end{pmatrix}^T=\begin{pmatrix}1 & 3 & 5 \\\\ 2 & 4 & 6\end{pmatrix}$

+ Property

  $(AB)^T=B^TA^T$



矩阵还有转置操作，就是把行和列互换，原来`i`行`j`列换成`j`行`i`列。矩阵的转置性质是如果你对两个矩阵乘积做转置等于先对后一个矩阵做转置再对前一个矩阵做转置，需要调换顺序再做转置。





#### Identity Matrix and Inverses

$I_{3\times3}=\begin{pmatrix}1 & 0 & 0 \\\\ 0 & 1 & 0 \\\\ 0 & 0 & 1\end{pmatrix}$

$AA^{-1}=A^{-1}A=I$

$(AB)^{-1}=B^{-1}A^{-1}$

另一个特殊的矩阵是单位矩阵，是一个对角阵（只有对角线有非零元素），上面就是一个$3\times 3$的单位矩阵。单位矩阵可以用来定义矩阵的逆。





#### Vector multiplication in Matrix form

+ Dot product?

  $\vec a \cdot \vec b = \vec a^T \vec b=\begin{pmatrix}x_a & y_a & z_a\end{pmatrix}\begin{pmatrix}x_b\\\\y_b\\\\z_b\end{pmatrix}=\begin{pmatrix}x_ax_b + y_ay_b+z_az_b\end{pmatrix}$

+ Cross product?

  $\vec a \times \vec b = A ^* b = \begin{pmatrix}0 & -z_a & y_a \\\\ z_a & 0 & -x_a \\\\ -y_a & x_a & 0\end{pmatrix}\begin{pmatrix}x_b \\\\ y_b \\\\ z_b\end{pmatrix}$

点乘和叉乘都可以写成矩阵的形式。





<br/>

<center>{% btn https://sites.cs.ucsb.edu/~lingqi/teaching/resources/GAMES101_Lecture_02.pdf,  GAMES101_Lecture_02, fas fa-download %}</center>

