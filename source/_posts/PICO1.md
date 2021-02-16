---
title: Pico-8—神奇的虚构游戏机
top: false
mathjax: false
tags:
  - Game
  - Pico-8
  - Reprint
categories: Pico-8 游戏引擎 (Pico-8 Game Engine)
abbrlink: 18a71cc2
translate_title: pico8—a-magical-fictional-game-console
date: 2020-10-29 23:40:43
comments: false
---



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1gk6mtusj1xj30sg0hs11h.jpg)



### 引言

由[Lexaloffle Games](https://pico-8.fandom.com/zh/wiki/LexaloffleGames)制作的[PICO-8](https://pico-8.fandom.com/zh/wiki/Pico8)是一台梦幻可编程游戏主机，用来制作，分享和玩小游戏和其他计算机程序（卡带，或“卡”）。这个主机提供了简单的内置工具来创造你自己的卡带。



<!-- more -->

> 本文转载了知乎专栏作家 [蓬岸 Dr.Quest](https://www.zhihu.com/people/peng-an-dr-quest) 翻译的 [Pico-8——神奇的虚构游戏机](https://zhuanlan.zhihu.com/p/30405996) 。原文刊载于《Skrolli》杂志，本文翻译自 2016.1E（国际版）：[Pico-8 – Fascinating fantasy console](https://link.zhihu.com/?target=https%3A//skrolli.fi/2016/07/pico-8-fascinating-fantasy-console/) 。



许多的电脑爱好者在它们的发烧之路上尝试过各种各样的硬件设备和软件平台。而很多时候它们会有意的搜集这些平台和设备，来尝试上面的游戏或是完成它们的艺术作品。这一探索过程也帮助这些发烧友们了解各个平台的特性，并帮助他们发掘自己喜爱或是感兴趣的电脑平台。而虚构的游戏机平台Pico-8就是其中别具趣味的一个。

对Pico-8最好的解释，就是它是一款并不真实存在的游戏机的模拟器。它的具有非常鲜明的8-bit风格，因此你可以把它像想为类似Game Boy Color这样的小掌机。它的提供一块128x128像素，16色的显示屏，以及四通道的音乐芯片。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1gk6myh5qnfj30g40f03yb.jpg)

不过，Pico-8却不仅仅是某种架空历史的实践，它设计的出发点与市面上已有的类似设备有着很大的不同。它并没有试图去最大化的利用有限的逻辑功能，而是提供了一批积木式的代码部件，尽可能的挖掘使用的乐趣。开发商希望随着时间的推移，Pico-8的技术框架将形成一种独特的审美观：极简主义并有着丰富的表现力。

### 第一印象

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/v2-9e2c70b8b1f9f12e73dba7cc4d0ee41c_720w.jpg)

Pico-8乍看上去有一点“精神分裂”。启动之后它给人的感觉并不是一台游戏机，而更像是一台带有键盘鼠标的家用电脑。它使用命令解释器来加载软件和输出提示，举例来说，按下ESC按钮，你会打开一个文本编辑器，它具有自己独立的区域来存储代码、图像和声音内容。不过，只有系统内置的应用程序可以访问键盘、鼠标和完整的文件系统——对于外部加载的应用程序来说，Pico是一台使用ROM卡带和双按钮手柄的游戏机。

Pico使用Lua作为它的开发语言，这款为游戏脚本而生的语言虽然功能有限，但却具有强大的表达能力。实际上，Pico虚拟机本身并不模拟任何处理器芯片——它甚至不会执行字节码。所有的东西全都使用Lua写成，这也是程序员们能访问到的最底层的东西。

分发Pico-8平台的游戏和软件主要有两种方式，一种方式被称作“卡带”（cartridges）或者“卡”（carts），它实际上是一张PNG图片，看起来像是一张带有封面贴纸的游戏卡，“卡带”图片使用了文件的低位（lower bits）来存储程序代码、图像和声音数据，类似某种文件指纹。而另一种方式则是将软件导出为HTML5格式并使用现代浏览器来运行，以这种方式运行的软件可以不需要Pico-8环境。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1gk6negts6uj30g40f0q43.jpg)



### 边界和限制

Pico最明显的技术特征就是128x128像素的屏幕分辨率以及固定的16色调色盘了，这一调色板具有相当独特而易于辨识的色彩组合，显示了其设计者对色彩的嗅觉相比一般的工程师更胜一筹。

虽然典型的Pico游戏通常使用8x8像素的方格来构成游戏地图，并使用8x8像素的动画精灵，但这却不是平台的限制之一。Pico的图形模式是纯粹的像素缓冲模式，它实际上可以绘制任何的图形——而机器的性能也足够流畅的运行90年代演示程序中的各种特效。不过，平台通过提供速度更快的绘制地图和精灵的功能函数，鼓励开发者使用8x8像素快而不是使用自己的代码逐个像素的绘制图形。

一张“游戏卡”可以存储15360字节（15KB）压缩后的代码，编辑器所能支持的最大长度是65536个字符或是8192个“标记”（tokens）。这一限制实际上并不容易达到，即使是许多Pico平台上最好的游戏其代码量也要明显低于这个数额。从另一个方面讲，这种限制鼓励开发者开发简单而线性的游戏逻辑，Pico上面没有空间容纳庞大的游戏引擎或多层的抽象逻辑。

“游戏卡”上还有12544字节（12.25KB）的空间预留给图像资源，另外4608字节（4.5KB）则留给声音。当然这些数据区域也可以被用作其他用途——内存操作指令可以在字节层面去操作它们。当程序开始运行之后，“游戏卡”中的数据将会被复制到RAM，然后程序就可以在需要的时候修改它们。用户可使用的RAM还包括了略低于7KB的用户保留空间，以及8KB的显存。

图形数据由8x8像素的精灵组成，它们可以包含调色板中的任意颜色。系统可以支持最多256个精灵，而地图则由128x32个精灵组成。如果只使用128个精灵的话，地图的尺寸还可以再翻倍。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1gk6nfqxlfdj30g40f0tby.jpg)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1gk6ng4qq1bj30g40f0jsz.jpg)

在声音方面，与“精灵”对应的是“声效”（sound effect - sfx），每个声效由32个音符位置（note locations）组成，每个音符位置都包含了音符和它的波形、音量和特效，每一个选项都有8种不同的设置可选，播放的速度也可以修改，较慢的播放速度更适合演奏音乐而不是音效。

与Tracker（序列器）音乐类似，一首歌曲由四个通道上定义了不同效果的“图案”（patterns）构成，Pico-8支持最多64个图案，通过使用循环和图案结束标记可以在一个文件中容纳多首歌曲。

虽然Pico-8的图形功能可以让开发者操作单个像素，但用户却无法直接访问声音系统的“寄存器”。理论上讲你可以通过实时修改声音数据来实现播放器功能，但虚拟机的时序限制很可能让这种功能无法被实现出来。不过，通过向音效内存里写入随机数据的方式，还是可以轻松的创造出若干试验性的声效的。

除了程序代码，数据RAM和卡带ROM之外，Pico还为Lua解释器提供了256KB内存空间。相比Pico的其他内存空间来说这一空间要大上不少，但它却比较容易被用完，比如说在操作大型表（Table - Lua中的一种数据结构）的时候。数字表的每个元素最多可以存储8字节，但实际的数据只能使用其中的一半。每个数字包含16 bit整数和16 bit小数部分，这些意味着通过位算数运算可以对它们进行比较。

当内存空间不足时，Pico也可以从其他ROM卡带中读取数据，甚至可以向卡带中写入数据。但程序代码有着严格的限制，只可以从它们原始的卡带中运行。Lua本身支持将数据作为代码运行，但Pico-8删除了这一功能，这意味着需要使用更多代码空间的程序需要构建它们自己的虚拟机。

Pico-8并不能以电脑处理器的全速执行Lua代码。执行不同函数所需的时间已经被预先设定好。而这种速度限制也可以减少典型的Pico软件开发时所可能出现的问题，同时也将其对硬件的需求标准化，并避免了硬件需求的螺旋上升。按照作者的描述，第一代的树莓派就足以让最复杂的Pico软件全速运行了。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1gk6ngt65gaj30g40f0q55.jpg)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/v2-6d32552c3b1c59afe54646f691845d57_720w.jpg)

### 如何编写代码？

Lua是一种全部使用大写字母的语言，因此它往往会让人联想起BASIC。举例来说许多人都会记得如何使用BASIC语言无限循环打印文本：

```qbasic
::START::
PRINT "HELLO"
GOTO START
```

不同于标准的Lua库，Pico提供了一组有限的BASIC风格的函数：其中包括了绘图函数，一组声音函数，控制器输入函数和一些内存管理、数学运算、位运算和字符串处理函数。

基本的绘图命令可以绘制像素、四边形、线段、圆形、文本、精灵和背景地图。绘图命令可以切换其使用的调色盘颜色，你也可以将精灵和背景的颜色变为透明色。

Pico绘制活动图形的功能更接近于PC而不是8-bit家用电脑。Pico没有“硬件精灵”或者“硬件卷轴”相反，通常每一次刷新都需要重新绘制：清除屏幕、绘制背景并绘制需要的精灵。

绘制精灵可以使用两个不同的函数：spr()可以在指定的坐标上绘制一个8x8像素的精灵，而sspr()则可以在任意区域以任意缩放比例绘制精灵。缩放功能可以帮助开发者实现在大多数经典硬件上开销较大的技巧，比如说Doom风格的纹理映射。

开发者可以将绘图命令放到一个无限循环当中，但更优雅的方式则是将其定义为名为_draw()的函数，这样每一次屏幕刷新都会触发到它，也就是说每秒会调用30次。因此上面的例子可以被这样改写：

```lua
FUNCTION _DRAW()
PRINT "TERVEHDYS"
END
```

btn()函数可以读取游戏手柄状态，它支持使用数字作为检查特定按钮是否被按下的参数。一段将0号精灵向左或向右移动的代码大概是这样：

```lua
X=64
FUNCTION _DRAW()
CLS()
SPR(0,X,112)
IF BTN(0) THEN X=X-1 END
IF BTN(1) THEN X=X+1 END
END
```

为了能够在屏幕上有所显示，在执行这段代码之前，您需要先在精灵编辑器里绘制0号精灵。

有时候_draw()函数可能包含了太多的功能，因此无法在每次屏幕刷新时执行。在这种情况下，开发者需要改用_update()函数来刷新游戏状态——理论上讲——它每秒也会被调用30次。同样的从理论上讲，由于没有使用定时器中断，如果_draw()花费的时间更长，它可能会被调用若干次。

一般来讲双缓冲（Double-buffering）的绘图技巧在Pico上面并不适用，因为只有当_draw()函数执行完成后更改显存的操作才其作用。另一方面来讲，即使在删除掉一些声音效果之后，用户内存也仅仅能够装下一个全屏双缓冲器。

声音方面Pico提供了sfx()和music()两个函数。前者会在第一个空闲的通道上播放指定参数的音效，而后者则会从指定的“图案”编号处开始播放音乐。

小型2D游戏的开发者们并不需要太在意命令执行的速度，只有当将要达到平台极限的时候才会出现问题。pset()函数刷新屏幕上所有像素所需的时间大概是正常情况下屏幕刷新的1.5倍。直接使用poke()函数写入显存则比一般情况下快将近三倍。然而，使用memcpy()和memset()函数的话，速度将会快上10倍，并且绘制背景图像的命令map()的速度也是一样快。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1gk6nhcialrj30g40f0gmw.jpg)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/v2-ba70fa875f4d1417f1cad188ee7671c3_720w.jpg)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1gk6nhra2naj30g40f0dh5.jpg)

### 像素方块的乐趣

Pico的许多功能都会让人联想起1980年代的家用电脑，但它却没有止步于对传统或技术的复原，而更加强调创作的乐趣和像素方块风格的美术效果。那些对这一点感到疑惑的人们应当考虑到它毕竟是一款虚构的游戏平台：虚拟世界并不总是完美无缺的，但它设定了许多有趣的事件，并能够激发参与者的想象力。

如果我们用一个词来总结Pico-8的精神的话，我想应该是“直截了当”。其中的一部分来自于8-bit电脑和运行在上面的BASIC语言：你可以在“开机”之后立刻编写程序，而不需要考虑如何配置操作系统、API和运行环境。所有的事情都简洁明了：内存里的某个比特总是会反馈到屏幕上某个位置的某个色块上。

然而这一概念并不止于此，它没有时钟周期和栅格线，没有颜色单元边界，没有折腾开发工具和文件的困扰。平台自身的限制避免了磨洋工式的细节调整。这得益于没有可以调节的调色盘、采样系统和机器语言指令，你不再需要对它们进行微调。而较少的像素数让完美主义者们也不会花太多时间在处理抗锯齿上。

对于那些对它感兴趣了人们来说，Pico-8确实有一些技术挑战和智力问题在等着它们。但我们也同样不会认为Pico-8的世界里需要极度关注细节。Pico程序写起来很快也很容易，熟悉这一平台基础只是的开发者可以在一晚上就写出一款相对精美的游戏。

当我写作这篇文章时，Pico仍然处于Alpha测试版本，至少在开发环境中这种不完善还是很容易被发觉的。代码编辑器不能自动跳到有错误的行，而绘制像素的时候键盘也不能使用。这些软件并不能很好的帮助用户进行开发，相反用户需要阅读零散的文档才能知道可以用ESC键打开编辑器这样简单的功能。地图编辑器也让人有点摸不着头脑，因为它没有任何地方标明地图里的零号精灵永远都是空白的。

但瑕不掩瑜，我还是推荐大家尝试Pico，即使新手程序员也是如此——至少是其中那些喜欢8-bit像素方块美术风格同时也不怕阅读文字说明的人。Lua语言没有明显的缺点，而Pico简化的接口鼓励开发者自行解决问题而不是寻找现成的方案。对于更有经验的开发者而言，Pico提供了一种轻松愉快的消遣方式，而其结果则比简单的涂鸦和水彩画丰富的多。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1gk6niel7jvj30g40f0wgc.jpg)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1gk6niqt745j30g40f0wfc.jpg)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1gk6nivzxeej30g40f0mxs.jpg)



### 社区和创意

Pico-8在开发之时就曾经参与众筹，并在发布之前就聚集了一大批热心粉丝。在我写下这篇文章之时，开发者论坛和Lexaloffle Games为Pico准备了超过250张卡带，包括游戏和各种软件。这其中大部分是平台游戏和各类传统2D动作游戏，但其中偶尔也夹杂着更加试验性的作品。在Pico平台上甚至可以找到一些Demoscene作品。

线上论坛从一开始就是Pico社区开发和发行的中心，这些论坛中有着温和和充满鼓励的气氛。社区中的成员以友好和互助的姿态欢迎初学者的加入。Pico开发团队的成员也经常参与讨论，这也让论坛成为讨论Pico技术细节的最佳去处。

Pico-8同样有着自己的发烧友杂志《Pico-8 Fanzine》，它收到了包括Lexaloffle的主力开发者“zep”在内的许多投稿。独立平台冒险游戏VVVVV的开发者Terry Cavanagh则是其中最有名的作者之一。发烧友杂志的作者和读者都是该平台的爱好者，截止到写作这篇文章的时候，这份发烧友杂志已经发行了三期。这份杂志和其他杂志类似，也包含了编写游戏的指导、采访、游戏测评、不同类型的Pico-8编程文章，当然还有爱好者们创作的美术作品。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/v2-3714e51f5188b199cf6927db5c5346e2_720w.jpg)

行文至此，我想许多读者们会非常确定的认为这款充满热血而开放的开发者文化的软件玩具一定是免费甚至开源的。但情况却并非如此，Pico-8是一款商业产品，目前正以$20的标价提供下载。二进制文件可以在三种重要的x86操作系统上运行：Windows，Mac OS和Linux。许多人都希望能推出一款基于硬件的Pico-8游戏机，但到目前为止，Pico-8仍然只能提供二进制格式的软件运行环境。

当然Pico是一款简单的平台，对其进行逆向工程未必很困难，并且Lua解释器本身已经是开源的。不过这一项目正被“友善光环”所围绕，因此没有多少黑客敢于开发免费和开源的Pico变种。相比之下我们更期待Lexaloffle自己会在客户们逐渐丧失兴趣的时候会将Pico开源。当社区衰退，开发也不再活跃之时，Pico可能会成为游戏开发的一个有趣的小众选项，乃至进入教育市场。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/v2-106cf0db903b13308093c99861c4dc41_720w.jpg)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1gk6njfmiooj30g40f0abi.jpg)

### 虚构平台的未来

像Pico-8这样的虚构游戏机是一种相对比较新的现象，虽然早在1970年代的微电脑爱好者中就已经存在Chip-8这样的虚拟机，并在某种程度上可以视为是它的前身，而许多教育软件也会使用简化的机器架构，而Pico的一个与众不同之处，就是它是“以创意作为第一考量”的。也因此它真正的前身可能只有Lexaloffle更早的Voxatron虚构游戏机。

在未来，很可能有相比Pico更小也更易于掌握的虚构平台出现，但其出现的原因却并不一定是要与Pico竞争或是比较——而很可能仅仅是出于好奇心。

Pico的功能鼓励人们在其上开发有趣可爱而又怀旧的作品，但选择不同的功能组合则可能创造出截然不同的精神世界和美术风格。比如说，如果人们开发出一款强调阴郁厚重风格的平台作为Pico的“邪恶双胞胎”就是一个颇为有趣的想法。当然，类似的现象在电脑平台发展史上时有发生，但创造虚构平台的亚文化可能会为研究这种现象提供某种有趣的试验环境。

无论未来的前景如何，Pico-8仍然是一个有趣的开发环境，相比那些经典的电脑和游戏机平台，它提供了一种更为轻松的选项。它将充满启发性的8-bit平台的种种限制和简单易用的现代设计理念结合起来，即使是那些对编程最不感冒的人群，也可能会被大颗像素的风格吸引，并从中找到诸多的乐趣。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1gk6njvray1j30g40f03ze.jpg)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/0081Kckwgy1gk6nk2wky5j30g40f040o.jpg)



> **芬兰语版本：**[Pico-8 – Fantasiakonsolin pauloissa](https://link.zhihu.com/?target=https%3A//skrolli.fi/2016/07/pico-8-fantasiakonsolin-pauloissa/) **文字作者：**Visa-Valtteri Pimiä, Ville-Matias Heikkilä
> **图片作者：**Laura Pesola, Ville-Matias Heikkilä



**Pico-8官网：**[http://www.pico-8.com/](https://link.zhihu.com/?target=http%3A//www.pico-8.com/)

### Pico-8游戏下载

+ [Duangle 2015 Intro](https://link.zhihu.com/?target=http%3A//www.lexaloffle.com/bbs/%3Ftid%3D1984)
+ [Dusk Child](https://link.zhihu.com/?target=http%3A//www.lexaloffle.com/bbs/%3Ftid%3D2274)
+ [Celeste](https://link.zhihu.com/?target=http%3A//www.lexaloffle.com/bbs/%3Ftid%3D2145)
+ [Ennuigi](https://link.zhihu.com/?target=http%3A//www.lexaloffle.com/bbs/%3Ftid%3D2232)
+ [Hybris](https://link.zhihu.com/?target=http%3A//www.lexaloffle.com/bbs/%3Fpid%3D17774)
+ [Hyperspace 1.1.1](https://link.zhihu.com/?target=http%3A//www.lexaloffle.com/bbs/%3Ftid%3D2688)
+ [Lemmtris](https://link.zhihu.com/?target=http%3A//www.lexaloffle.com/bbs/%3Ftid%3D2028)
+ [PICORACER-2048](https://link.zhihu.com/?target=http%3A//www.lexaloffle.com/bbs/%3Ftid%3D2243)
+ [Star Beast](https://link.zhihu.com/?target=http%3A//www.lexaloffle.com/bbs/%3Ftid%3D2950)














