---
title: 词法分析
comment: false
tags: Compilers
categories: '编译原理 (Compilers Principles, Techniques, and Tools)'
abbrlink: 55180fbf
date: 2021-03-03 17:15:57
type:
banner_img:
index_img:
translate_title:
top:
mathjax: ture
---





![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/827e85100849161.Y3JvcCw0MDg1LDMxOTUsMjAyLDY0Nw.jpg)



<div align=center>
  <font size="3">
    <i>
      <a href="https://www.behance.net/gallery/100849161/American-Lighthouses">American Lighthouses</a> by 
      <a href="https://www.behance.net/AnnSophieDeSteur">Ann-Sophie De Steur</a>
    </i>
  </font>
</div>




### 引言

编译原理旨在介绍编译程序构造的一般原理和基本方法。内容包括语言和文法、词法分析、语法分析、语法制导翻译、中间代码生成、存储管理、代码优化和目标代码生成，本节主要是对词法分析部分进行展开讲解。

<!--more-->

### 词法分析程序功能

词法分析是对构成源程序的**字符串**从左到右进行扫描和分解，根据语言的**词法规则**识别出一个一个具有独立意义的单词



### 单词符号及输出形式

语言的单词符号是指语言中具有独立意义的最小语法单位。





### 字母表和字符串

#### 字母表

字母表：元素的非空有穷集合。例如$\Sigma = \{a,b,c\}$，根据字母表的定义，$\Sigma$是字母表，它由$a、b、c$三个元素组成。

字母表（Alphabet）$\Sigma$是一个非空有穷集合，字母表中的元素也称为该字母表的一个字母（Letter），也叫字符（Charater）。

例如，以下是不同的字母表：

+ $\{ a,b,c,d \}$
+ $\{ a,b,c,...,z \}$
+ $\{ 0,1 \}$
+ ASCII字母表

注意：

+ 字母表中至少包含一个元素
+ 字母表中的元素，可以是字母、数字或其他符号

例如：$\Sigma = \{ 0,1,a,(,* \}$是一个字母表，由$0$，$1$，$a$，$（$，$*$五个元素组成。



#### 字符

字母表中的元素称为字符，例如前述例子中：$a、b、c$是字母表$\Sigma$中的字符；$0、1、a、(、*$是字母表$\Sigma$中的字符。





#### 字符串

字符的有穷序列称为字符串。例如设有字母表$\Sigma = \{ a,b,c \}$，则有串$a,b,ab,ba,cba,abc...$

字符串总是建立在某个特定字母表上的且只由字母表上的有穷多个字符组成。字符串中字符的顺序是很重要的，例如$ab$和$ba$是字母表$\Sigma$上的两个不同的字符串。

不包含任何字符的字符串，称为空字符串，用$\epsilon$表示。空字符串由0个字符组成，其长度$|\epsilon|=0$。



### 字符串运算

#### 字符串的连结

设$x$和$y$是字符串，则串$xy$称为它们的连结。

例如设$X=ABC$，$Y=10A$，那么$XY=ABC10A$、$YX=10AABC$。对任意一个符号串$X$，有$\epsilon X = X \epsilon = X = ABC$



#### 集合的连接

设$A$和$B$是符号串的集合，则$A$和$B$的连接定义为：$AB=\{ xy|x \in A,y \in B \}$

集合的乘积是满足于$x \in A,y \in B$的所有符号串$xy$所构成的集合。

例如设$A=\{ c,d \}$，$B=\{ 0,1\}$，则：

$AB=\{c0,c1,d0,d1 \}$，$BA =\{ 0c,1c,0d,1d\}$，$AA = \{ cc , cd , dc, dd\}$，$BB=\{ 00,01,10,11\}$，$BBA=\{ 00c,01c,10c,11c,00d,01d,10d,11d\}$，$ABB=\{ c00,c01,c10,c11,d00,d01,d10,d11\}$

其中$(AB)B=A(BB)$，可以发现集合的运算满足结合律不满足交换律。

对于集合$|A|=2,|B|=2$，则$|AB|=|BA|=|A| \times |B|=4$，$|ABB|=|AB| \times |B| = 8$



特别指出，$\epsilon$是字符串，不是集合，而$\{\epsilon\}$表示由空字符串$\epsilon$所组成的集合。集合$\phi=\{\}$是空集合。



#### 字符串的幂运算

设$x$是字符串，则$x$的幂运算定义为：
$$
X^1=X=abc \\
X^2=XX=abcabc \\
X^3=XXX=abcabcabc \\
X^4=XXXX=abcabcabcabc \\
...... \\
X^n=XX...XXX=abcabc...abcabcabc
$$


#### 集合的幂运算

设$A$是字符串的集合，则集合$A$的幂运算定义为：
$$
A^0=\{\epsilon\} \\
A^1=A \\
A^2=AA \\
...... \\
A^n=AA...A=AA^{n-1}(n>0)
$$
举个例子，设$A=\{a,b\}$，则：
$$
A^0=\{ \epsilon \} \\
A^1=\{ a,b \} \\
A^2=\{ aa,ab,ba,bb\} \\
A^3=\{ aaa,aab,aba,abb,baa,bab,bba,bbb\}
$$




#### 集合的闭包

设$A$是字符串的集合，则$A$的闭包$A*$定义为：
$$
A*=A^0 \cup A^1 \cup A^2 ... \cup A^n ... \\
=\{\epsilon \} \cup A^1 \cup A^2 \cup ... \cup A^n ...
$$
例如设$A=\{a\},B=\{b\}$，试求：

1. $A*=\{\epsilon,a,aa,...a^n...\}(n>1)$
2. $B*=\{\epsilon,b,bb,...b^n...\}(n>1)$
3. $(AB)*=\{\epsilon,ab,abab,...(ab)^n...\}(n>1)$
4. $(BA)*=\{\epsilon,ba,baba,...(ba)^n...\}(n>1)$



### 复习回顾

#### 字符串

1. 由字母表中的字符组成的任何**有穷序列**称为字符串，例如$001110$是字母表$\Sigma=\{0,1\}$是字符串
2. 字母表$A=\{a,b,c\}$上的一些字符串有：$ab,c,bc,aaca$
3. 字符串是有序的，字符串$ab$就不同于$ba$
4. 可以使用字母表示字符串，如$X=STR$表示“X是由字符$S、T$和$R$并按此顺序组成的字符串”

#### 字符串的长度

如果某字符串$X$有$m$个字符，则称其长度为$m$，表示为$|X|=m$，如$001110$的长度是6

空字符串即不包含任何字符的符号串，用$\epsilon$表示，其长度为0即$|\epsilon|=0$



#### 字符串的连接

设$X$和$Y$是字符串，它们的连接$XY$是把$Y$的字符串写在$X$的字符之后得到的字符串，特殊情况有：$\epsilon X=X \epsilon=X$

例如$X=ST,Y=abu$，则它们的连接$XY=STabu，YX=abuST$看出$|X|=2,|Y|=3,|XY|=5$



#### 字符串集合的连接

+ 若集合$A$中所有元素都是某元素表$\Sigma$上的字符串，则称$A$为字母表$\Sigma$上的字符串集合
+ 两个字符串集合$A$和$B$的连接定义：$AB=\{XY|X \in A 且Y \in B\}$，若$A=\{ab,cde\}$，集合$B=\{0,1\}$，则$AB=\{ab0,ab1,cde0,cde1\}$，$BA=\{0ab,1ab,0cde,1cde\}$



#### 闭包

非空集合$\Sigma$上的一切字符串（包括空字符串$\epsilon$）组成的集合用$\Sigma*$表示，称为$\Sigma$的闭包。