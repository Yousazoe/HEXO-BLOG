---
title: Transformation Cont
comment: false
tags:
  - Computer Graphics
  - Math
  - Linear Algebra
categories: 现代图形学入门 (GAMES101-Introduction to Computer Graphics)
abbrlink: e1a90797
date: 2021-03-29 19:57:16
type:
banner_img:
index_img:
translate_title:
top:
mathjax: true
---



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/ExPC_w-WQAAggTf.jpeg)

<div align=center>
  <font size="3">
    <i>
      <a href="https://twitter.com/Zarbuz">Twitter@Zarbuz</a>
    </i>
  </font>
</div>




### 引言

GAMES101现代图形学入门是由闫令琪老师教授。这节课继续讲解三维变换，并且主要来说相对比较困难的观测变换，包括视图、投影、正交投影以及透视。

<!--more-->





### 3D Transforms

Use homogeneous coordinates again:
• 3D point = $(x, y, z, 1)^T$
• 3D vector = $(x, y, z, 0)^T$ 


In general, $(x, y, z, w)$ ($w != 0$) is the 3D point:$(x/w,y/w,z/w)$



三维变换只需要拿二维变换作对比即可，并不复杂。



Use 4×4 matrices for affine transformations

$\begin{pmatrix}x' \\\\ y' \\\\ z' \\\\ 1\end{pmatrix} = \begin{pmatrix}a & b & c & t_x \\\\ d & e & f & t_y \\\\ g & h & i & t_z \\\\ 0 & 0 & 0 & 1\end{pmatrix} \cdot \begin{pmatrix}x \\\\ y \\\\ z \\\\ 1\end{pmatrix}$

**What’s the order?** 

Linear Transform first or Translation first?



在之前二维空间的齐次坐标中，我们先应用线性变换，最后再平移，在三维空间也是一样。



Scale：$S(s_x,s_y,s_z)=\begin{pmatrix}s_x & 0 & 0 & 0 \\\\ 0 & s_y & 0 & 0\\\\ 0 & 0 & s_z & 0 \\\\ 0 & 0 & 0 & 1\end{pmatrix}$

Translation：$T(t_x,t_y,t_z)=\begin{pmatrix}1 & 0 & 0 & t_x \\\\ 0 & 1 & 0 & t_y \\\\ 0 & 0 & 1 & t_z \\\\ 0 & 0 & 0 & 1\end{pmatrix}$



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210329205934890.png)



在三维空间中如果我想把一个物体旋转要写出旋转矩阵，比如我们先考虑绕轴旋转（图中为绕x轴旋转），我们可以发现y与z在旋转，而所有的x坐标保持不变，反应在矩阵上就是第一行是$\begin{pmatrix}1 & 0 & 0 & 0\end{pmatrix}$。同样的道理可以运用在y与z轴上。



#### 3D Rotations

Compose any 3D rotation from Rx, Ry, Rz?

$R_{xyz}(\alpha,\beta,\gamma)=R_x(\alpha)R_y(\beta)R_z(\gamma)$

+ So-called Euler angles
+ Often used in flight simulators: roll, pitch, yaw

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210329214557527.png)



在图形学中我们能够解决简单的问题，对于复杂的问题我们也可以转换为简单的问题的组合。比如这里我不知道如何将任意旋转分解为绕轴旋转，但我们可以先思考能否通过三种绕轴方向旋转实现任意方向的旋转。

上图这三个角被称为欧拉角，我们可以先考虑一下飞机的飞行运动，它可以上下抬头/低头旋转、向左/右平移旋转、侧翼顺/逆时针旋转，通过这么几种不同的旋转飞机当然可以调整到任意一个方向。



#### Rodrigues’ Rotation Formula

**Rotation by angle α around axis n：**

$R(n,\alpha)=\cos{(\alpha)}I+(1-\cos{(\alpha)})nn^T+\sin{(\alpha)}\begin{pmatrix}0 & -n_z & n_y \\\\ n_z & 0 & -n_x \\\\ -n_y & n_x & 0\end{pmatrix}$



**How to prove this magic formula?**

Check out the supplementary material on the course website!



在图形学中就有人发明了一套办法，通过分解为三个方向可以把任意旋转写成这么一个矩阵，也就是罗德里格斯旋转公式。这个旋转公式非常复杂，推导过程如下：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210330074955431.png)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210330075031617.png)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210330075055898.png)

这个旋转公式定义了一个旋转轴和旋转角度，而旋转轴只用一个向量定义不太合理，旋转轴首先要和起点有关系，然后跟它方向有关系。为什么需要一个起点呢？之前我们默认旋转轴过原点，但实际上并不是所有旋转都过原点。

上节课变换的分解中我们提到二维旋转如果要绕任意一个点旋转，我们需要先把中心点平移到原点上，再做旋转，再把它平移回来。在三维空间中是完全相同的做法，如果我们沿任意轴旋转而起点并不为原点，没关系，先把所有的东西都移到使得轴过原点上，然后旋转，最后再把所有东西移回去，问题解决。



### View transformation

#### View/Camera Transformation

**What is view transformation?**

**Think about how to take a photo**

+ Find a good place and arrange people (model transformation)
+ Find a good “angle” to put the camera (view transformation)
+ Cheese! (projection transformation)



我们学这些的目的是把三维空间的物体变成二维空间中的照片，这个过程发生了什么我们要弄明白，但这个过程一定涉及了三维到二维的变换。

咱们一开始先说拿到一个场景我要规定场景和相机位置，然后我得到某一个投影出来，否则对于一个三维场景从不同的角度看，看到的一定不同，“怎么看”这个问题很重要。首先什么是视图变换，这里思考一个简单的问题：现实生活中怎么拍一张照片？

+ 首先找一个好的地方搭好场景摆好pose（模型变换）
+ 第二步**找到好的角度/位置将相机放置好**（视图变换）
+ 下一步是“茄子！”可以拍照（投影变换）



**How to perform view transformation?**

**Define the camera first**

+ Position $\vec e$

+ Look-at / gaze direction $\hat g$

+ Up direction $\hat t$

  (assuming perp. to look-at)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210330081309372.png)





那大家想一想如何确定相机的摆放。首先相机的位置一定非常重要，所以我们要定义它，但只确定位置并没有用，比如大家坐在座位上，头是可以扭动朝不同方向去看的，“往哪儿看”也是非常重要的，这个属性被称为Look-at direction。

只定义方向依然不够，我们还需要一个向上的方向：大家在拍照的时候相机逆时针旋转45度和顺时针旋转45度拍摄出来的照片一定不一样，旋转一定会影响拍出来的图是什么，所以我们用一个向量来定义这个向上的属性值把旋转固定住。到这里我们终于把相机固定在一个位置了。



**Key observation**

+ If the camera and all objects move together, 

  the “photo” will be the same

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210330083515330.png)

**How about that we always transform the camera to**

+ The origin, up at Y, look at -Z
+ And transform the objects along with the camera

下一步我们来想如何进行视图变换，在现实生活中也是这样：大家坐在车上不往窗户外面看，是感觉不到自己在移动，这个在物理上叫相对运动。那么在观察或者说拍照片上也是一个道理，摄影棚里相同的人、相同的相机、相同的摆放位置不管在哪个摄影棚大家拍出来的是一样的，也就是说当相机和包括前景背景所有的东西都一起移动的时候，那么拍出来的这张照片一定是一样的。

我们考虑到这点可以得出只要物体与相机之间没有相对运动，它拍摄的结果是一样的。更进一步思考，我们可以认为相机放置在固定的位置上，所有东西都是其他物体在移动并且相机永远在原点，约定俗成向上朝向y轴指向-z轴。



**Transform the camera by $M_{view}$**

+ So it’s located at the origin, up at Y, look at Z



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210330090221385.png)



**Mview in math?**

+ Translates e to origin
+ Rotates g to -Z
+ Rotates t to Y
+ Rotates (g x t) To X
+ Difficult to write!



我们要把相机从任意的一种摆放给放到标准位置上去，做一个一一对应。比如相机原本的中点在$\vec e$这个位置，朝向$\hat g$并且上方向是$\hat t$，现在我们需要改成上面以原点为中心的：

+ 中心从$\vec e$平移到原点
+ 观察方向由$\hat g$旋转到-Z
+ 向上方向由$\hat t$旋转到Y
+ 将$\hat g \times \hat t$旋转至X



**$M_{view}$ in math?**

+ Let's write $M_{view} = R_{view}T_{view}$

+ Translate e to origin

  

  $T_{view}=\begin{bmatrix}1 & 0 & 0 & -x_e \\\\ 0 & 1 & 0 & -y_e \\\\ 0 & 0 & 1 & -z_e \\\\ 0 & 0 & 0 & 1\end{bmatrix}$

+ Rotate g to -Z, t to Y, (g x t) To X

+ Consider its inverse rotation: X to (g x t), Y to t, Z to -g

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210401115305765.png)





对于这样一系列的操作我们转换为矩阵形式。旋转矩阵是正交矩阵，所以它的逆是它的转置。



**Summary**

+ Transform objects together with the camera
+ Until camera’s at the origin, up at Y, look at -Z

**Also known as ModelView Transformation**

**But why do we need this?**

+ For projection transformation!





#### Projection Transformation

**Projection in Computer Graphics**

+ 3D to 2D
+ Orthographic projection
+ Perspective projection

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210330100005157.png)



我在看立方体可以看到不同的结果，左边和右边它们两个分别用了两种不同的投影方式。左边这幅图立方体不同的面的平行线依然平行，然而右边这张图就不是了，如果延长两条线它会相交在某个点上。

如果大家学过画画或者素描，人眼的成像更类似右边这种，也就是透视投影。透视投影有一个性质，你会看到平行线不再平行，它们都会相交到某一个地方去。左边的正交投影更多用来工程制图，但它最本质的是不会带来近大远小的现象，而透视投影会有这个现象，成语一叶障目说的就是如此，最近还有一个“道理我都懂，但是鸽子怎么这么大？ ”的梗大家可以去搜一下。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/58e99490a88f4a94a134d87ad1857f8b-20210330233419071.jpeg)





Perspective projection vs. orthographic projection

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210330100058408.png)



那么我们反应到数学上该怎么说这个事情呢？我们之后会说。这里是两张图解释两种投影，左边就是透视投影，我们认为摄像机放置在某个位置上的一个点，这个点我们在空间中连出一个锥；相应的正交投影假设相机离得无限远，这样相当于近处的平面跟远处的平面就会越来越接近，最后进和远是完全一样的大小，投影出来的就一样了。





##### Orthographic Projection

**A simple way of understanding**

+ Camera located at origin, looking at -Z, up at Y (looks familiar?)
+ Drop Z coordinate
+ Translate and scale the resulting rectangle to $[-1, 1]^2$

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210330100502693.png)

我们从最简单的正交投影开始讲。正交投影就是不管远近挤到一个平面就可以了，首先我们把相机放在一个位置上（看向-Z，向上朝Y），然后这样摆放把z坐标扔掉得到结果自然是xy平面上的图了。

最后不管xy的范围多大，我们都约定俗成把它移到 $[-1, 1]^2$一个小的矩形，得到正交投影的结果。



**In general**

+ We want to map a cuboid $[l, r] \times [b, t] \times [f, n]$ to the “canonical (正则、规范、标准)” cube $[-1, 1]^3$**Slightly different orders (to the “simple way”)**

+ Center cuboid by translating
+ Scale into “canonical” cube



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210330100705375.png)



严格的做法是首先我们定义空间中的一个立方体，定义立方体的左右在x轴是多少，下上在y轴上是多少，远近在z轴各占多少。通过这6个数我们把立方体描述出来，然后我们把这样一个形状视图映射到最右图的这个标准立方体。

中间过程如上图所示，我们把立方体中心移到原点，然后把x、y、z轴分别拉成 $[-1, 1]^3$就可以了。特别要说的是和我们之前说的简单的把z轴扔掉是有不一样的地方，多了一个平移；还有一件事是我们看向-Z方向，如果一个面离我们远意味着z值更小，反之越近z值越大。



**Transformation matrix?**

+ Translate (center to origin) first, then scale (length/width/height to 2)

$M_{ortho} = \begin{bmatrix}\frac{2}{r-l} & 0 & 0 & 0 \\\\ 0 & \frac{2}{t-b} & 0 & 0 \\\\ 0 & 0 & \frac{2}{n-f} & 0 \\\\ 0 & 0 & 0 & 1\end{bmatrix}\begin{bmatrix}1 & 0 & 0 & -\frac{r+l}{2} \\\\ 0 & 1 & 0 & -\frac{t+b}{2} \\\\ 0 & 0 & 1 & -\frac{n+f}{2} \\\\ 0 & 0 & 0 & 1\end{bmatrix}$



我们现在需要把这么一个变换用矩阵写成数学形式。首先我们将其中心平移到原点，然后再做一个缩放，把x、y、z的宽度都变成2。对于正交投影非常简单，写成两个矩阵相乘的形式就好了。



**Caveat**

+ Looking at / along -Z is making near and far not intuitive (n > f)
+ FYI: that’s why OpenGL (a Graphics API) uses left hand coords.









#### Perspective Projection

+ Most common in Computer Graphics, art, visual system
+ Further objects are smaller
+ Parallel lines not parallel; converge to single point

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210330102231509.png)



透视投影是一种广泛的投影，满足近大远小的性质，它带来的效果是投影到的平行线看上去不再平行。在欧式几何中定义平行线是永不相交，而在下面的照片上却不对：



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210330102352159.png)



两条铁轨显然是平行的，在照片中不仅是相交的，甚至可以把交点指出来。在同一个平面两条平行线肯定是不会相交的，但如果一个平面被投影到另一个平面上，这个情况下就不是平行线了，这是透视投影带给大家不一样的地方。



**Before we move on**

**Recall: property of homogeneous coordinates**

+ $(x, y, z, 1), (kx, ky, kz, k != 0), (xz, yz, z^2, z != 0) $ all represent the same point $(x, y, z)$ in 3D
+ e.g. $(1, 0, 0, 1)$ and $(2, 0, 0, 2)$ both represent $(1, 0, 0)$ 

**Simple, but useful**

在做透视投影时有一些数学基础需要回顾一下。对于齐次坐标而言 $(x, y, z, 1), (kx, ky, kz, k != 0)$ 表示的是相同的，比如$(1,0,0,1)$和$(2,0,0,2)$都代表了$(1,0,0)$这个点，简单却有用。



**How to do perspective projection**

+ First “squish” the frustum into a cuboid (n -> n, f -> f) ($M_{persp \to ortho}$)
+ Do orthographic projection ($M_{ortho}$, already known!)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210330102656577.png)



透视投影和平行投影的区别就是这些线从左边投影到右边，那么这给了我们一种思路：可以先把f面与中间的东西挤压到与n相同，再进行正交投影。

正交投影我们已经熟悉了，现在只需要解决挤压。对于挤压的过程我们定义一些事情，首先近平面永远不变，挤压前后不变；远平面的z值不变，就在平面内收缩；对于f面的中心我们也认为不变。





**In order to find a transformation**

+ Recall the key idea: Find the relationship between transformed points (x’, y’, z’) and the original points (x, y, z)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210330102812268.png)



我们假设从侧面向Frustum看，我想知道对于任何一个点$(x,y,z)$，经过挤压之后会如何变换呢？拿出y来看可以发现一个相似三角形，可以得到 $\frac{n}{z} = \frac{y'}{y} \to y' = \frac{n}{z}y$，也就是任意一点如何被挤压是相对清楚的。





**In order to find a transformation**

+ Find the relationship between transformed points (x’, y’, z’) and the original points (x, y, z)

$y' = \frac{n}{z}y$    $\space x' = \frac{n}{z}x$ (similar to y')

**In homogeneous coordinates,** 

$\begin{pmatrix}x \\\\ y \\\\ z \\\\ 1\end{pmatrix} \to \begin{pmatrix}nx/z \\\\ ny/z \\\\ unknown \\\\ 1\end{pmatrix} == \begin{pmatrix}nx \\\\ ny \\\\ still unknown \\\\ z\end{pmatrix}$







**So the “squish” (persp to ortho) projection does this**

$M^{(4 \times 4)}_{persp \to ortho} \begin{pmatrix}x \\\\ y \\\\ z \\\\ 1\end{pmatrix} = \begin{pmatrix}nx \\\\ ny \\\\ unknown \\\\ z\end{pmatrix}$

**Already good enough to figure out part of $M_{persp->ortho}$**

$M_{persp \to ortho} = \begin{pmatrix}n & 0 & 0 & 0 \\\\ 0 & n & 0 & 0 \\\\ ? & ? & ? & ? \\\\ 0 & 0 & 1 & 0\end{pmatrix}$

通过矩阵运算的性质我们很容易可以推导出$M_{persp \to ortho}$矩阵部分元素（第一、二、四行），我们只剩第三行不知道。



**How to figure out the third row of $M_{persp \to ortho}$**

+ Any information that we can use?



**Observation: the third row is responsible for z’**

+ Any point on the near plane will not change
+ Any point’s z on the far plane will not change



在近、远平面上它们的z不变（其他面有可能变化），这就够了。任何一个点在近平面都不会发生变化，远平面虽然x、y会往里挤，但z不发生变化。





**Any point on the near plane will not change**

$M^{(4 \times 4)}_{persp \to ortho}\begin{pmatrix}x \\\\ y \\\\ z \\\\ 1\end{pmatrix} = \begin{pmatrix}nx \\\\ ny \\\\ unknown \\\\ z\end{pmatrix} \to \begin{pmatrix}x \\\\ y \\\\ n \\\\ 1\end{pmatrix} == \begin{pmatrix}nx \\\\ ny \\\\ n^2 \\\\ n\end{pmatrix}$

**So the third row must be of the form (0 0 A B)**

$\begin{pmatrix}0 & 0 & A & B\end{pmatrix}\begin{pmatrix}x \\\\ y \\\\ n \\\\ 1\end{pmatrix} = n^2$

利用近平面不变的性质，我们将$unknown$替换为$n$并同时乘上$n$可以得到，并且假设的第三行$(0 \space 0 \space A \space B)$可以得到一个与xy无关的定值$n^2$。



**What do we have now?**

$\begin{pmatrix}0 & 0 & A & B\end{pmatrix}\begin{pmatrix}x \\\\ y \\\\ n \\\\ 1\end{pmatrix} = n^2 \to An + B = n^2$

**Any point’s z on the far plane will not change**

$\begin{pmatrix}0 \\\\ 0 \\\\ f \\\\ 1\end{pmatrix} \to \begin{pmatrix}0 \\\\ 0 \\\ f \\\\ 1\end{pmatrix} == \begin{pmatrix}0 \\\\ 0 \\\\ f^2 \\\\ f\end{pmatrix} \to Af+b=f^2$



远平面同样满足该性质，并且中心点$f$也不会变化，将这两个情况带入矩阵，这样我们就得到了两个联立式子。



**Solve for A and B**

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210617201514599.png)


**Finally, every entry in $M_{persp \to ortho}$ is known!**

**What’s next?**

+ Do orthographic projection (Mortho) to finish 
+ $M_{persp} = M_{ortho}M_{persp \to ortho}$



通过联立方程我们可以解出$M_{persp \to ortho}$，再做正交投影就可以得到透视投影。



<br/>

<center>{% btn https://sites.cs.ucsb.edu/~lingqi/teaching/resources/GAMES101_Lecture_04.pdf,  GAMES101_Lecture_04, fas fa-download %}</center>

