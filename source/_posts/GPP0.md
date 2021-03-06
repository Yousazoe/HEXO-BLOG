---
title: 序
comment: false
categories: 游戏设计模式 (Game Programming Patterns)
abbrlink: 334513da
date: 2021-05-01 16:06:41
type:
tags:
banner_img:
index_img:
translate_title:
top:
mathjax:
---

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/E2JU0jdWQAAtB7R.jpeg)

<div align=center>
  <font size="3">
    <i>
      <a href="https://twitter.com/tleyna101/status/1396772843074039811">Twitter@tleyna101
</a>
    </i>
  </font>
</div>

### 引言

游戏开发一直是热门的领域，掌握良好的游戏编程模式是开发人员的应备技能，本书细致地讲解了游戏开发需要用到的各种编程模式，并提供了丰富的示例。本章是游戏设计模式的序言。

<!--more-->



### 序

在五年级时，我和我的朋友被准许使用一间存放有几台非常破旧的TRS-80s的房间。 为了鼓舞我们，一位老师给我们找了一些简单的BASIC程序打印文档。

电脑的磁带驱动器已经坏掉了，所以每当我们想要运行代码，就得小心地从头开始输入它们。 因此，我们更喜欢那些只有几行长的程序：

```
10 PRINT "BOBBY IS RADICAL!!!"
20 GOTO 10
```

> 如果电脑打印的次数足够多，也许这句话就会魔法成真。

哪怕这样，过程也充满了困难。我们不知道如何编程，所以小小的语法错误对我们来说也是天险。 如果程序没有工作，我们就得从头再来一遍——这经常发生。

文档的最后几页是个真正的怪物：一个占据了几页篇幅的程序。 我们得花些时间才能鼓起勇气去试一试，但它实在太诱人——它的标题是“地道与巨魔”。 我们不知道它能做什么，但听起来像是个游戏，还有什么比自己编个电脑游戏更酷的吗？

我们从来没能让它运行起来，一年以后，我们离开了那间教室。 （很久以后，当我真的学会了点BASIC，我意识到那只是个桌面游戏角色生成器，而不是游戏。） 但是命运的车轮已经开始转动——自那时起，我就想要成为一名游戏程序员。

青少年时，我家有了一台能运行QuickBASIC的Macintosh，之后THINK C也能在其上运行。 几乎整个暑假我都在用它编游戏。 自学缓慢而痛苦。 我能轻松地编写并运行某些部分——地图或者小谜题——但随着程序代码量的增长，这越来越难。

> 暑假中的不少时间我都花在在路易斯安那州南部的沼泽里逮蛇和乌龟上了。 如果外面不是那么酷热，很有可能这就会是一本讲爬虫而不是编程的书了。

起初，挑战之处仅仅在于让程序成功运行。然后，是搞明白怎样写出内容超出我大脑容量的代码。 我不再只阅读关于“如何用C++编程”的书籍，而开始尝试找那些讲如何*组织*程序的书。

几年过后，一位朋友给我一本书：《设计模式：可复用面向对象软件的基础》。 终于！这正是我从青年时期就在寻找的书。 我一口气从头读到尾。虽然我仍然挣扎于自己的程序中，但看到别人也在挣扎并提出了解决方案是一种解脱。 我意识到手无寸铁的我终于有件像样的*工具*了。

> 那是我首次见到这位朋友，相互介绍五分钟后，我坐在他的沙发上，在接下来的几个小时中无视他并全神贯注地阅读。 我想自那以后我的社交技能还是有所提高的。

在2001年，我获得了梦想中的工作：EA的软件工程师。 我等不及要看看真正的游戏，还有专业人士是如何组织一切的。 像实况足球这样的大型游戏使用了什么样的架构？不同的系统是如何交互的？一套代码库是如何在多个平台上运行的？

分析理解源代码是种震颤的体验。图形，AI，动画，视觉效果皆有杰出代码。 有专家知道如何榨干CPU的最后一个循环并好好使用。 那些我都不知道是否*可行*的事情，这些人在午饭前就能完成。

但是这些杰出代码依赖的架构通常是事后设计。 他们太注重功能而忽视了架构。耦合充斥在模块间。 新功能被塞到任何能塞进去的地方。 在梦想幻灭的我看来，这和其他程序员没什么不同， 如果他们阅读过《设计模式》，最多也就用用单例。

当然，没那么糟。我曾幻想游戏程序员坐在白板包围的象牙塔里，为架构冷静地讨论上几周。 而实际情况是，我看到的代码是努力应对紧张截止期限的人赶工完成的。 他们已经竭尽全力，而且就像我慢慢意识到的那样，他们全力以赴的结果通常很好。 我花在游戏代码上的时间越多，我越能发现藏在表面下的天才之处。

不幸的是，“藏”是普遍现象。 宝石埋在代码中，但人们从未意识到它们的存在。 我看到同事重复寻找解决方案，而需要的示例代码就埋在他们所用的代码库中。

这个问题正是这本书要解决的。 我挖出了游戏代码库中能找到的设计模式，打磨然后在这里展示它们，这样可以节约时间用在发明新事物上，而非*重新*发明它们。



#### 书店里已有的书籍

书店里已经有很多游戏编程书籍了。为什么要再写一本呢？

我看到的很多编程书籍可以归为这两类：

- **特定领域的书籍。** 这些关于细分领域的书籍带你深入理解游戏开发的某一特定层面。 它们会教授你3D图形，实时渲染，物理模拟，人工智能，或者音频播放。 那些很多程序员穷其一生研究的细分领域。
- **完整引擎的书籍。** 另一个方向，还有书籍试图包含游戏引擎的各个部分。 它们倾向于构建特定种类游戏的完整引擎，通常是3D FPS游戏。

这两种书我都喜欢，但我认为它们并未覆盖全部空间。 特定领域的书籍很少告诉你这些代码如何与游戏的其他部分打交道。 你擅长物理或者渲染，但是你知道怎么将两者优雅地组合吗？

第二类书包含这些，但是我发现完整引擎的书籍通常过于整体，过于专注某类游戏了。 特别是，随着手游和休闲游戏的兴起，我们正处于众多游戏类型欣欣向荣的时刻。 我们不再只是复制Quake了。如果*你的*游戏与该类游戏不同，那些介绍单一引擎的书就不那么有用了。

相反，我在这里做的更*à la carte* 。 每一章都是独立的、可应用到代码上的思路。 这样，你可以用*你*认为最好的方式组合这些思路，用到你的游戏上去。

> 另一个广泛使用这种*à la carte*风格的例子是[*Game Programming Gems*](http://www.satori.org/game-programming-gems/)系列。



#### 和设计模式的关联

任何名字中有“模式”的编程书 都与Erich Gamma，Richard Helm，Ralph Johnson，和John Vlissides（通常被称为GoF）合著的经典书籍： 《设计模式：可复用面向对象软件要素》相关。

> 《设计模式》也受到之前的书籍的启发。 创建一种模式语言来描述问题的开放式解法， 这思路来自 [*A Pattern Language*](http://en.wikipedia.org/wiki/A_Pattern_Language)， 作者是Christopher Alexander (还有Sarah Ishikawa和Murray Silverstein).
>
> 他们的书是关于架构的（建筑和墙那样的*真正的*框架结构）， 但他们希望其他人能使用相同的方法描述其他领域的解决方案。 《设计模式》正是是GoF用这一方法在软件业做出的努力。

称这本书为“游戏编程模式”，我不是暗示GoF的模式不适用于游戏编程。 相反：本书的重返设计模式一节包含了《设计模式》中的很多模式， 但强调了这些模式在游戏编程中的特定使用。

同样地，我认为本书也适用于非游戏软件。 我可以依样画瓢称本书为《更多设计模式》，但是我认为举游戏编程为例子更为契合。 你真的想要另一本介绍员工记录和银行账户的书吗？

也就是说，虽然这里介绍的模式在其他软件上也很有用，但它们更合适于处理游戏中常见的工程挑战：

- 时间和顺序通常是游戏架构的核心部分。事物必须在正确的时间按正确的顺序发生。
- 高度压缩的开发周期，大量程序员需要能快速构建和迭代一系列不同的行为，同时保证不烦扰他人，也不污染代码库。
- 在定义所有的行为后，游戏开始互动。怪物攻击英雄，药物相互混合，炸弹炸飞敌人或者友军。 实现这些互动不能把代码库搞成一团乱麻。
- 最后，游戏中性能很重要。 游戏开发者处于一场榨干平台性能的竞赛中。 节约CPU循环的技巧区分了A级百万销量游戏和掉帧差评游戏。



#### 如何阅读这本书

《游戏设计模式》分为三大块。 第一部分介绍并划分本书的框架。包含你现在阅读的这章和下一章。

第二部分，重访设计模式，复习了GoF书籍里的很多模式。 在每一章中，我给出我对这个模式的看法，以及我认为它和游戏编程有什么关系。

最后一部分是这本书最肥美的部分。 它展示了十三种我发现有用的模式。它们被分为四类： 序列模式, 行为模式, 解耦模式,和优化模式。

每种模式都使用固定的格式表述，这样你可以将这本书当成引用，快速找到你需要的：

- **意图** 部分提供这个模式想要解决什么问题的简短介绍。 将它放在首位，这样你可以快速翻阅，找到你现在需要的模式。
- **动机** 部分描述了模式处理的问题示例。 不同于具体的算法，模式通常不针对某个特定问题。 不用示例教授模式，就像不用面团教授烘烤。动机部分提供了面团，而下部分会教你烘烤。
- **模式** 部分将模式从示例中剥离出来。 如果你想要一段对模式的教科书式简短介绍，那就是这部分了。 如果你已经熟悉了这种模式，想要确保你没有拉下什么，这部分也是很好的提示。
- 到目前为止，模式只是用一两个示例解释。但是如何知道模式对*你的*问题有没有用呢？ **何时使用** 部分提供了这个模式在何时使用何时不用的指导。 **记住** 部分指出了使用模式的结果和风险。
- 如果你像我一样需要具体的例子来真正地*理解*某物，那么**示例代码**部分能让你称心如意。 它描述模式的一步步具体实现，来展现模式是如何工作的。
- 模式与算法不同的是它们是开放的。 每次你使用模式，可以用不同的方式实现。 下一部分**设计决策**，讨论这些方式，告诉你应用模式时可供考虑的不同选项。
- 作为结尾，这里有**参见**部分展示了这一模式与其他模式的关联，以及那些使用它的真实代码。



#### 关于示例代码

这本书的示例代码使用C++写就，但这并不意味着这些模式只在C++中有用，或C++比其他语言更适合使用这些模式。 这些模式适用于几乎每种编程语言，虽然有的模式假设编程语言有对象和类。

我选择C++有几个原因。首先，这是在游戏制作中最流行的语言，是业界的*通用语*。 通常，C++基于的C语法也是Java，C#，JavaScript和其他很多语言的基础。 哪怕你不懂C++，你也只需一点点努力就能理解这里的示例代码。

这本书的目标*不是*教会你C++。 示例代码尽可能地简单，不一定符合好的C++风格或规范。 示例代码展示的是意图，而不是代码。

特别地，代码没用“现代的”——C++11或者更新的——标准。 没有使用标准库，很少使用模板。 它们是“糟糕”C++代码，但我希望保持这样，这样那些使用C，Objective-C，Java和其他语言的人更容易理解它们。

为了避免花费时间在你已经看过或者是与模式无关的代码上，示例中省略了部分代码。 如果是那样，示例代码中的省略号表明这里隐藏了一些代码。

假设有个函数，做了些工作然后返回值。 而用它作示例的模式只关心返回的值，而不是完成了什么工作。那样的话，示例代码长得像这样：

```c++
bool update()
{
  // 做点工作……
  return isDone();
}
```



#### 接下来呢

设计模式在软件开发过程中不断地改变和扩展。 这本书继续了GoF记录分享设计模式的旅程，而这旅程也不会终于本书。

你是这段旅程的关键部分。改良（或者否决）了这本书中的模式，你就是为软件开发社区做贡献。 如果你有任何建议，更正，或者任何反馈，保持联络！





### 架构，性能和游戏

在一头扎进一堆设计模式之前，我想先讲一些我对软件架构及如何将其应用到游戏之中的理解， 这也许能帮你更好地理解这本书的其余部分。 至少，在你被卷入一场关于设计模式和软件架构有多么糟糕（或多么优秀）的辩论时， 这可以给你一些火力支援。

> 注意我没有建议你在战斗中选哪一边。就像任何军火贩子一样，我愿意向作战双方出售武器。



#### 什么是软件架构？

如果把本书从头到尾读一遍， 你不会学会3D图形背后的线性代数或者游戏物理背后的微积分。 本书不会告诉你如何用α-β修剪你的AI树，也不会告诉你如何在音频播放中模拟房间中的混响。

> Wow，这段给这本书打了个糟糕的广告啊。

相反，这本书告诉你在这些之间的代码的事情。 与其说这本书是关于如何写代码，不如说是关于如何架构代码的。 每个程序都有一定架构，哪怕这架构是“将所有东西都塞到main()中看看如何”， 所以我认为讲讲什么造成了好架构是很有意思的。我们如何区分好架构和坏架构呢？

我思考这个问题五年了。当然，像你一样，我有对好的设计有一种直觉。 我们都被糟糕的代码折磨得不轻，你唯一能做的好事就是删掉它们，结束它们的痛苦。

> 不得不承认，我们中大多数人都该对一些糟糕代码*负责*。

少数幸运儿有相反的经验，有机会在好好设计的代码库上工作。 那种代码库看上去是间豪华酒店，里面的门房随时准备满足你心血来潮的需求。 这两者之间的区别是什么呢？



#### 什么是好的软件架构？

对我而言，好的设计意味着当我作出改动，整个程序就好像正等着这种改动。 我可以仅调用几个函数就完成任务，而代码库本身无需改动。

这听起来很棒，但实际上不可行。“把代码写成改动不会影响其表面上的和谐。”就好。

让我们通俗些。第一个关键点是*架构是关于改动的*。 总会有人改动代码。如果没人碰代码，那么它的架构设计就无关紧要——无论是因为代码至善至美，还是因为代码糟糕透顶以至于没人会为了修改它而玷污自己的文本编辑器。 评价架构设计的好坏就是评价它应对改动有多么轻松。 没有了改动，架构好似永远不会离开起跑线的运动员。



#### 你如何处理改动？

在你改动代码去添加新特性，去修复漏洞，或者随便用文本编辑器干点什么的时候， 你需要理解代码正在做什么。当然，你不需要理解整个程序， 但你需要将所有相关的东西装进你的大脑。

> 有点诡异，这字面上是一个OCR过程。

我们通常无视了这步，但这往往是编程中最耗时的部分。 如果你认为将数据从磁盘上分页到RAM上很慢， 那么通过一对神经纤维将数据分页到大脑中无疑更慢。

一旦把所有正确的上下文都记到了你的大脑里， 想一会，你就能找到解决方案。 可能有时也需要反复斟酌，但通常比较简单。 一旦理解了问题和需要改动的代码，实际的编码工作有时是微不足道的。

用手指在键盘上敲打一阵，直到屏幕上闪着正确的光芒， 搞定了，对吧？还没呢！ 在你为之写测试并发送到代码评审之前，通常有些清理工作要做。

> 我是不是说了“测试”？噢，是的。为有些游戏代码写单元测试很难，但代码库的大部分是完全可以测试的。
>
> 我不会在这里发表演说，但是我建议你，如果还没有做自动测试，请考虑一下。 除了手动验证以外你就没更重要的事要做了吗？

你将一些代码加入了游戏，但肯定不想下一个人被留下来的小问题绊倒。 除非改动很小，否则就还需要一些微调新代码的工作，使之无缝对接到程序的其他部分。 如果你做对了，那么下个编写代码的人无法察觉到哪些代码是新加入的。

简而言之，编程的流程图看起来是这样的：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/architecture-cycle.png)



> 令人震惊的死循环，我看到了。



#### 解耦帮了什么忙？

虽然并不明显，但我认为很多软件架构都是关于研究代码的阶段。 将代码载入到神经元太过缓慢，找些策略减少载入的总量是件很值得做的事。 这本书有整整一章是关于解耦模式， 还有很多设计模式是关于同样的主题。

可以用多种方式定义“解耦”，但我认为如果有两块代码是耦合的， 那就意味着无法只理解其中一个。 如果*解*耦了它们俩，就可以单独地理解某一块。 这当然很好，因为只有一块与问题相关， 只需将*这一块*加载到你的大脑中而不需要加载另外一块。

对我来说，这是软件架构的关键目标： **最小化在编写代码前需要了解的信息**。

当然，也可以从后期阶段来看。 解耦的另一种定义是：当一块代码有改动时，不需要修改另一块代码。 肯定也得修改一些东西，但耦合程度越小，改动会波及的范围就越小。



#### 代价呢？

听起来很棒，对吧？解耦任何东西，然后就可以像风一样编码。 每个改动都只需修改一两个特定方法，你可以在代码库上行云流水地编写代码。

这就是抽象、模块化、设计模式和软件架构使人们激动不已的原因。 在架构优良的程序上工作是极佳的体验，每个人都希望能更有效率地工作。 好架构能造成生产力上*巨大的*不同。它的影响大得无以复加。

但是，天下没有免费的午餐。好的设计需要汗水和纪律。 每次做出改动或是实现特性，你都需要将它优雅的集成到程序的其他部分。 需要花费大量的努力去管理代码， 使得程序在开发过程中面对千百次变化仍能*保持*它的结构。

> 第二部分——管理代码——需要特别关注。 我看到无数程序有优雅的开始，然后死于程序员一遍又一遍添加的“微小黑魔法”。
>
> 就像园艺，仅仅种植是不够的，还需要除草和修剪。

你得考虑程序的哪部分需要解耦，然后再引入抽象。 同样，你需要决定哪部分能支持扩展来应对未来的改动。

人们对这点变得狂热。 他们设想，未来的开发者（或者他们自己）进入代码库， 发现它极为开放，功能强大，只需扩展。 他们想要有“至尊代码应众求”。（译著：这里是“至尊魔戒御众戒”的梗，很遗憾翻译不出来）

但是，事情从这里开始变得棘手。 每当你添加了抽象或者扩展支持，你就是在*赌*以后这里需要灵活性。 你向游戏中添加的代码和复杂性是需要时间来开发、调试和维护的。

如果你赌对了，后来使用了这些代码，那么功夫不负有心人。 但预测未来*很难*，模块化如果最终无益，那就有害。 毕竟，你得处理更多的代码。

> 有些人喜欢使用术语“YAGNI”——[You aren’t gonna need it（你不需要那个）](http://en.wikipedia.org/wiki/You_aren't_gonna_need_it)——来对抗这种预测将来需求的强烈冲动。

当你过分关注这点时，代码库就失控了。 接口和抽象无处不在。插件系统，抽象基类，虚方法，还有各种各样的扩展点，它们遍地都是。

你要消耗无尽的时间回溯所有的脚手架，去找真正做事的代码。 当需要作出改动时，当然，有可能某个接口能帮上忙，但能不能找到就只能听天由命了。 理论上，解耦意味着在修改代码之前需要了解更少的代码， 但抽象层本身也会填满大脑。

像这样的代码库会使得人们*反对*软件架构，特别是设计模式。 人们很容易沉浸在代码中，忽略了目标是要发布*游戏*。 对可扩展性的过分强调使得无数的开发者花费多年时间制作“引擎”， 却没有搞清楚做引擎是*为了什么*。



#### 性能和速度

软件架构和抽象有时因损伤性能而被批评，而游戏开发尤甚。 让代码更灵活的许多模式依靠虚拟调度、 接口、 指针、 消息和其他机制， 它们都会加大运行时开销。

> 一个有趣的反面例子是C++中的模板。模板编程有时可以带来没有运行时开销的抽象接口。
>
> 这是灵活性的两极。 当写代码调用类中的具体方法时，你就是在*写*的时候指定类——硬编码了调用的是哪个类。 当使用虚方法或接口时，直到*运行*时才知道调用的类。这更加灵活但增加了运行时开销。
>
> 模板编程是在两极之间。在**编译时**初始化模板，决定调用哪些类。

还有一个原因。很多软件架构的目的是使程序更加灵活，作出改动需要更少的付出，编码时对程序有更少的假设。 使用接口可以让代码可与任何实现了接口的类交互，而不仅仅是现在写的类。 今天，你可以使用观察者和消息让游戏的两部分相互交流， 以后可以很容易地扩展为三个或四个部分相互交流。

但性能与假设相关。实现优化需要基于确定的限制。 敌人永远不会超过256个？好，可以将敌人ID编码为一个字节。 只在这种类型上调用方法吗？好，可以做静态调度或内联。 所有实体都是同一类？太好了，可以使用 [连续数组](https://gpp.tkchu.me/data-locality.html) 存储它们。

但这并不意味着灵活性不好！它可以让我们快速改进游戏， *开发*速度对创造更好的游戏体验来说是很重要的。 没有人能在纸面上构建一个平衡的游戏，哪怕是Will Wright。这需要迭代和实验。

尝试想法并查看效果的速度越快，能尝试的东西就越多，也就越可能找到有价值的东西。 就算找到正确的机制，你也需要足够的时间调试。 一个微小的不平衡就有可能破坏整个游戏的乐趣。

这里没有普适的答案。 要么在损失一点点性能的前提下，让你的程序更加灵活以便更快地做出原型； 要么就优化性能，损失一些灵活性。

就我个人经验而言，让有趣的游戏变得高效比让高效的游戏变有趣简单得多。 一种折中的办法是保持代码灵活直到确定设计，再去除抽象层来提高性能。



#### 糟糕代码的优势

下一观点：不同的代码风格各有千秋。 这本书的大部分是关于保持干净可控的代码，所以我坚持应该用*正确*方式写代码，但糟糕的代码也有一定的优势。

编写架构良好的代码需要仔细地思考，这会消耗时间。 在项目的整个周期中*保持*良好的架构需要花费大量的努力。 你需要像露营者处理营地一样小心处理代码库：总是让它比之前更好些。

当你要在项目上花费很久时间的时这是很好的。 但就像早先提到的，游戏设计需要很多实验和探索。 特别是在早期，写一些你*知道*将会扔掉的代码是很普遍的事情。

如果只想试试游戏的某些点子是否可行， 良好的架构就意味着在屏幕上看到和获取反馈之前要消耗很长时间。 如果最后证明这点子不对，那么删除代码时，那些让代码更优雅的工夫就付诸东流了。

原型——一坨勉强拼凑在一起，只能完成某个点子的简单代码——是个完全合理的编程实践。 虽然当你写一次性代码时，*必须* 保证将来可以扔掉它。 我见过很多次糟糕的经理人在玩这种把戏：

> 老板：“嗨，我有些想试试的点子。只要原型，不需要做得很好。你能多快搞定？”
>
> 开发者：“额，如果删掉这些部分，不测试，不写文档，允许很多的漏洞，那么几天能给你临时的代码文件。”
>
> 老板：“太好了。”

**几天后**

> 老板：“嘿，原型很棒，你能花上几个小时清理一下然后变为成品吗？”

你得让人们清楚，可抛弃的代码即使看上去能工作，也不能被维护，必须 重写。 如果有可能要维护这段代码，就得防御性地好好编写它。

一个小技巧能保证原型代码不会变成真正用的代码：使用和游戏实现不同的编程语言。 这样，在将其实际应用于游戏中之前必须重写。



#### 保持平衡

有些因素在相互角力：

1. 为了在项目的整个生命周期保持其可读性，需要好的架构。
2. 需要更好的运行时性能。 
3. 需要让现在想要的特性更快地实现。

> 有趣的是，这些都是速度：长期开发的速度，游戏运行的速度，和短期开发的速度。

这些目标至少是部分对立的。 好的架构长期来看提高了生产力， 也意味着每个改动都需要消耗更多努力保持代码整洁。

草就的代码很少是**运行时**最快的。 相反，提升性能需要很多的开发时间。 一旦完成，它就会污染代码库：高度优化的代码不灵活，很难改动。

总有今日事今日毕的压力。但是如果尽可能快地实现特性， 代码库就会充满黑魔法，漏洞和混乱，阻碍未来的产出。

没有简单的答案，只有权衡。 从我收到的邮件看，这伤了很多人的心，特别是那些只是想做个游戏的人。 这似乎是在恐吓，“没有正确的答案，只有不同的错误。”

但对我而言，这让人兴奋！看看任何人们从事的领域， 你总能发现某些相互抵触的限制。无论如何，如果有简单的答案，每个人都会那么做。 一周就能掌握的领域是很无聊的。你从来没有听说过有人讨论挖坑。

> 也许你会讨论挖坑；我没有深究这个类比。 可能有挖坑热爱者，挖坑规范，以及一整套亚文化。 我算什么人，能在此大放厥词？

对我来说，这和游戏有很多相似之处。 国际象棋之类的游戏永远不能被掌握，因为每个棋子都很完美地与其他棋子相平衡。 这意味你可以花费一生探索广阔的可选策略。糟糕的游戏就像井字棋，玩上几遍就会厌倦地退出。



#### 简单

最近，我感觉如果有什么能简化这些限制，那就是*简单*。 在我现在的代码中，我努力去写最简单，最直接的解决方案。 你读过这种代码后，完全理解了它在做什么，想不到其他完成的方法。

我的目标是正确获得数据结构和算法（大致是这样的先后），然后再从那里开始。 我发现如果能让事物变得简单，最终的代码就更少， 就意味着改动时有更少的代码载入脑海。

它通常跑的很快，因为没什么开销，也没什么代码需要执行。 （虽然大部分时候事实并非如此。你可以在一小段代码里加入大量的循环和递归。）

但是，注意我并没有说简单的代码需要更少的时间*编写*。 你会这么觉得是因为最终得到了更少的代码，但是好的解决方案不是往代码中注水，而是*蒸干*代码。

> Blaise Pascal有句著名的信件结尾，“我没时间写得更短。”
>
> 另一句名言来自Antoine de Saint-Exupery：“臻于完美之时，不是加无可加，而是减无可减。”
>
> 言归正传，我发现每次重写本书，它就变得更短。有些章节比刚完成时短了20%。

我们很少遇到优雅表达的问题，一般反而是一堆用况。 你想要X在Z情况下做Y，在A情况下做W，诸如此类。换言之，一长列不同行为。

最节约心血的方法是为每段用况编写一段代码。 看看新手程序员，他们经常这么干：为每种情况编写条件逻辑。

但这一点也不优雅，那种风格的代码遇到一点点没想到的输入就会崩溃。 当我们想象优雅的代码时，想的是*通用*的那一个： 只需要很少的逻辑就可以覆盖整个用况。

找到这样的方法有点像模式识别或者解决谜题。 需要努力去识别散乱的用例下隐藏的规律。 完成时你会感觉好得不能再好。



#### 就快完了

几乎每个人都会跳过介绍章节，所以祝贺你看到这里。 我没有太多东西回报你的耐心，但还有些建议给你，希望对你有用：

- 抽象和解耦让扩展代码更快更容易，但除非确信需要灵活性，否则不要在这上面浪费时间。
- 在整个开发周期中为性能考虑并做好设计，但是尽可能推迟那些底层的，基于假设的优化，那会锁死代码。

相信我，发布前两个月不是开始思考“游戏运行只有1FPS”这种问题的时候。

- 快速地探索游戏的设计空间，但不要跑得太快，在身后留下烂摊子。毕竟你总得回来打扫。
- 如果打算抛弃这段代码，就不要尝试将其写完美。摇滚明星将旅店房间弄得一团糟，因为他们知道明天就走人了。
- 但最重要的是，**如果你想要做出让人享受的东西，那就享受做它的过程。**
