---
top: false
mathjax: true
abbrlink: 1492ea3c
translate_title: malthusian-population-theory-and-mathematical-modeling
tags:
  - Math
  - Mooc
  - Population
  - Mathematical Modeling
categories: 数学建模 (Mathematical Modeling)
title: 马尔萨斯人口论与数学建模
date: 2020-10-24 13:41:27
comments: false
---

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1gk0dpddbq1j30xc0m80tg.jpg)

<div align=center>
  <font size="3">
    <i>
      <a href="https://www.behance.net/gallery/100474895/World-Population-Day_Advertisment?tracking_source=search_projects_recommended%7CPopulation">World Population Day_Advertisment</a> by 
      <a href="https://www.behance.net/vibinks">vibin ks</a>
    </i>
  </font>
</div>


### 引言

本文基于马尔萨斯的人口论，探讨人类社会人口的增长趋势并列举多种变体人口增长模型，同时领悟数学建模的主要思想和具体步骤，加深学习和理解。



<!-- more -->



### 问题

>  **群体的增长能不能预测？**

例如当前全球人口有72亿，我们能否预测30年后地球上有多少人呢？未来的趋势又是如何呢？



| 年度 |   人口总量    | 增长率% | 年度净变化率 |
| :--: | :-----------: | :-----: | :----------: |
| 1960 | 3,039,332,401 |  1.33   |  40,781,960  |
| 1961 | 3,080,114,361 |  1.80   |  56,083,390  |
| 1962 | 3,136,197,751 |  2.19   |  69,508,948  |
| 1963 | 3,205,706,699 |  2.19   |  71,110,065  |
| 1964 | 3,276,816,764 |  2.08   |  69,021,089  |
| ...  |    ......     |   ...   |    ......    |





对于上面的人口统计数据集，当然可以选择使用统计回归模型 **（数据型）**。这无疑可以是一个选择，但这里我们更多的想讨论机理型的数学模型 **（机理型）**。两种类型的模型中机理型更侧重于问题的分析和解决，数据型更注重于数据的结果。



### 群体的增长趋势是什么？

#### 马尔萨斯人口论

##### 马尔萨斯

马尔萨斯(1766—1834)，英国牧师，被称为西方思想史上最富有争议的经济学家、 人口学家，以他1798年出版的*《人口原理》* 而闻名于世。

##### 基本论题

人类食物供给增长趋势无法跟上人口增长的趋势

##### 基本原理

+ 食物为人类生存所必需
+ 两性间的情欲是必然，而且几乎会保持现状

##### 基本论述 

马尔萨斯认为：

+ 人口有 **几何增长** 的趋势（即按 **指数** 函数增长的趋势），如级数（1，2，4，8，16，... ）

+ 食物供应只有 **算术增长** 的趋势（即按 **线性** 函数增长的趋势），如级数（1，2，3，4，5，... ）

这样两种增长方式显然是不匹配的，所以他的结论是：**人口会有无限的增长的趋势，直至食物供应的极限为止**

##### 结论

要控制人口的无节制增长。



### 马尔萨斯人口模型

在马尔萨斯的著作里并没有数学化的论述，甚为遗憾。**公理的表述方式，则看出欧几里得对西方文化的影响**。这里我们按马尔萨斯的想法和原则，数学化这个问题：

$P(t)$  $t$ 时刻的人口数量

我们的问题始终是：

> 1. **已知当前或过去某个时刻的人口数量，预测未来某个时刻的人口？**
> 2. **遥远未来的趋势（$t$ 趋于无穷）？**



#### 高尔斯的推导

蒂莫西·高尔斯在《数学》里也讨论了人口预测问题：“人口可以表示为一组数对 $(t,P(t))$ 。其中 $t$ 表示时间，$P(t)$ 表示时刻 $ t $ 的人口规模。另外我们要用到两个数 $b$ 和 $d$ 来表示出生率和死亡率。”

假如2002年初人口总数是 $p$, 则2002年出生的人数和死亡的人数就分别是 $bp$ 和 $dp$, 所以2003年初的人口总数将是 $p+bp-dp=(1+b-d)p=(1+r)p$ ，这里的 $r$ 就是自然增长率。

高尔斯这个模型是离散的，但是人口的增长是时刻变化而不是离散的，如果当前人口量是 $P(t)$，经过一个 $\Delta t$ 的时间人口量达到 $P(t+\Delta t)$，则此时有 $P(t+\Delta t)-P(t)=rP(t)\Delta t$ 。接着取极限使 $\Delta t$ 趋近于0：$P(t+dt)-P(t)=rP(t)dt$  

> $\frac{dP(t)}{dt}=rP(t)$   -->   $P(t_0)=P_0$   -->  $P(t)=P_0e^{r(t-t_0)}$

最后我们发现人口数量函数是一个指数函数。通过推导出的上式我们解决了第一个问题，即已知当前或过去某个时刻的人口数量，预测未来某个时刻的人口只要带入当前人口就可以求解；而第二个问题由于是指数函数，这样的函数在 $t$ 趋于无穷时是快速趋于无穷的，所以马尔萨斯的论断是有理由的（他也确实使用欧洲的人口数据对模型进行验证）。



#### 回顾

首先我们面对一个**现实问题**：人口会是怎么增长的；接着把现实问题**表达为数学模型**，并**分析、求解模型**；之后模型解变为**问题的解决方案**；最后解决方案回到现实问题，通过数据对模型进行验证。如果与现实并不符合，也可能需要修改数学模型与求解过程。马尔萨斯也是基于这个模型对人口进行论断：要控制人口的无节制增长。



### Logistic模型

高尔斯推导的微分方程固然不错，可事实上自然增长率 $r$ 不是常量，它也在时刻变化中。在马尔萨斯那个年代，因为人口数量还不是特别多，所以人口受资源的约束还没有那么大，可以维持自然增长，自然增长率可以是一个常数。但现在的情况下 **自然增长率一定会是时间的函数 $r(t)$**。当人口量增长到一定量的时候，人口数量一定会关联自然增长率，所以可以通过人口总量让自然增长率成为 $t$ 的函数 ：$r(t)=r(P(t))$

Logistic模型中自然增长率 $r$ 依旧可以认为是一个常数，但是这个常数现在我们需要对它进行校正。下式可以发现相比高尔斯的模型多了一个参数 $K$，直观意义是地球最多能养活多少人，也就是 **环境承载量**。不同的社会学家和人口学家对这个问题没有统一的意见，但他们的共识是 **$K$ 这个参数一定是存在的**。

> $r(t)=r(P(t))=r(1-\frac{P(t)}{K})$

#### 基本共识

地球能养活的人一定是有限的

#### 比较

在这个共识下引入参数 $K$ 让Logistic模型比马尔萨斯更好一些。但马尔萨斯那个年代 $P(t)$ 远比 $K$ 要小，$\frac{P(t)}{K}$ 趋近于0 ，最后可以得到 $r(t)=r$，也就是马尔萨斯的猜想，没有什么问题。但到了19-20世纪的地球，后面的这一项 $\frac{P(t)}{K}$ 就变的不可以忽略了，马尔萨斯的模型因为太简单而不能解决现实问题，所以虽然引入参数让模型变得更加复杂，但也更符合实际情况。

#### 推导

> $\frac{dN(t)}{dt}=r(1-\frac{N(t)}{K})N(t)$  
>
> $N(t_0)=N_0$

$N(t)$表示时间 $t$ 处人口的数量，换个符号以区别于马尔萨斯模型

> $N(t)=\frac{K}{1+Ce^{-r(t-t_0)}}$
>
> $C=\frac{K-P_0}{P_0}$

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1gk9yk47wlkj30ev08sq3j.jpg)

回到之前的两个问题，第一个问题依然可以直接计算代入即可；第二个问题中令 $t$ 趋于无穷预测未来趋势，作图可以发现$K$ 是一个渐进线：如果初值比 $K$ 值小，人口会以“S”型曲线增长直至达到 $K$ 值饱和； 如果初值已经超过 $K$ 值，它会比较快速的下降到 $K$ 值之后稳定。



#### 模型离散化

将微分方程再化为差分方程，考虑这个模型的离散化：

>  $\frac{dN}{dt}=rN(1-\frac{N}{K})$  -->  $\frac{\Delta N}{\Delta t}=rN(1-\frac{N}{K})$
>
>  $\Delta N = N_{t+1}-N_t$
>
>  $\Delta t = 1$

这里差分方程的时间离散步长取为其，每一代就是一个时间步。

> $N_{t+1}-N_t=rN_t(1-\frac{N_t}{K})$
>
> $N_{t+1}=(1+r)N_t-\frac{r}{K}N_t^{2}$

取定参数 $K$ ，考虑不同的参数 $r$ 

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1gk9yjjz3r2j30gn08k3zt.jpg)

可以发现 $t$ 越来越大时愈发趋近于 $K$ 。让我们再看一看 $r$ 变大一点的效果：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1gk9yj5csmcj30fl080dhk.jpg)

我们可以发现在极限状态下呈现出一定的周期性，极限也不一定是之前稳态的 $K$ 了，更像是一种平均值，所以严格来说它并没有极限，或者说是2周期的解，每两步就回来。那如果 $r$ 继续增大呢？

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1gk9ylqp2m0j30gb07otaz.jpg)

我们可以观察到它还是周期的，但不再是2周期的了，而是4周期的。那我们继续让 $r$ 增大：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1gk9ygqasbdj30gh085ac9.jpg)

随着 $r$ 的不断增大，最后甚至会出现“混沌”的状态：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1gk9z26wrn9j30fj07576t.jpg)

也就是说如果对这个问题做一个小的扰乱比如初始值，整个曲线后面变化会非常大，也可以说是对初值敏感的依赖（“混沌”的标准）。所以从离散化的模型我们可以得到这么丰富的现象，结果非常意外。



### Leslie模型

言归正传回到原来的问题，之前的两个模型都只考虑了 **人口总量** 的问题，而忽视了 **人口分布** 的问题：人口总量一样、人口分布不一样。这个问题的核心在于**只有人口总量一个是否可以足够刻画人口**，而 **年龄分布** 的引入显然是对人口更完整的刻画。

假如现在以年为单位，年龄对人口进行切分：$N_t=\begin{pmatrix} n_0 \\\\ n_1 \\\\ ... \\\\ n_s \end{pmatrix}_t$

> $n_{0,t+1}=F_0n_{0,t}+F_1n_{1,t}+...+F_sn_{s,t}$
>
> $n_{1,t+1}=p_0n_{0,t}$
>
> ......
>
> $n_{s,t+1}=p_{s-1}n_{s-1,t}$

上式中我们不只关心人口的总量，还要注意不同年龄段人口的分布。由于模型是离散的，所以自然可以写成矩阵的形式：

> $N_{n+1}=LN_t$
>
> $L = \begin{pmatrix} F_0 & F_1 & F_2 & ... & F_s \\\\ p_0 & 0 & 0 & ... & 0 \\\\ 0 & p_1 & 0 & ... & 0 \\\\ 0 & 0 & ... & p_{s-1} & 0\end{pmatrix}$

该模型的复杂在于需要更多的参数：马尔萨斯需要1个参数、Logistic模型需要2个参数，而到了Leslie模型，我们需要更多的参数--人口分段的两倍。当有太多人为的参数的时候会出现许多不完全客观的东西，不可避免会带有主观性。那么利用数学模型去认知问题其实很重要的是 **理性的手段带来更好的客观性**。当这样的参数越来越多的时候，客观性就会受到损害。但也正是因为之前简单的模型无法解决今天越来越复杂的问题，我们才会去考虑更复杂的模型。

回到之前反复研究的两个问题，在这些参数都比较好得到的情况下只需要乘上矩阵就可以得到下一年或者下一个时刻的，可以完美解决。而对于第二个问题，假设已知矩阵的特征值（$\lambda_0，\lambda_1，...，\lambda_s$）和相应的特征向量（$\nu_0,\nu_1，...，\nu_s$），如果初始人口设为 $N_0$，则有 ：

> $N_0=c_0v_0+\sum^S_{i=1}c_i(\lambda_i)^t\nu_t$
>
> $N_t=c_0(\lambda_0)^t\nu_0+\sum^S_{i=1}c_i(\lambda_i)^t\nu_i$

当 $t$ 趋于无穷时，如果 $\lambda_0>|\lambda_i| \space i = 1，2，...,s$，则有 $\lim_{t \to \infty}N_t \propto c_0(\lambda_0)^t \nu_0$,所以渐进状态是由首特征大小和对应的特征向量决定的，$|\lambda_0|>1$ 人口会越来越多；$|\lambda_0|<1$ 会逐渐走向灭亡；$|\lambda_0|=1$则会进入一个稳态。





### 更复杂的模型

对于更复杂的问题是否要采用更复杂的模型，具体还是要看需求。Leslie模型是离散的，我们可以考虑将模型重新连续化。这样我们需要考虑这样一个函数：它是 $t$ 的函数，同时也应该是年龄的多元函数 $P(a,t)$。我们也需要将之前的切分年龄段参数变成连续的分布函数： `出生率-年龄`函数 和 `存活率-年龄` 函数。

真的问题都不是无病呻吟，如果可以解决问题，模型越简洁越好，没有复杂化的必要。模型变得越来越复杂，是因为有这种需求，这种需求不可避免的要做更复杂的模型，我们才去改进。回到人口问题本身，即使我们已经考虑到了年龄的影响因素，我们仍有许多影响因素没有考虑进来：

+ 地域差异
+ 移民的影响

对于这种情况最好使用 **随机模型**，在模型中体现出过程的随机性。



<div align=center>
  <font size="3">
    <i> Acknowledgement <br/> 
      <a href="https://www.behance.net/vibinks">vibin ks</a>
    </i>
  </font>
</div>



