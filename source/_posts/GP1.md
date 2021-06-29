---
title: 游戏开发导论
comment: false
tags:
  - Game
categories: 游戏程序设计 (Game Programming)
abbrlink: d10a3b2
date: 2021-02-28 19:15:47
banner_img:
index_img:
translate_title:
top:
mathjax:
---







![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/c61aa566966371.5b292fe8c68c9.jpg)

<div align=center>
  <font size="3">
    <i>
      <a href="https://www.behance.net/gallery/66966371/PromaxGames-Sponsor-Titles">PromaxGames Sponsor Titles</a> by 
      <a href="https://www.behance.net/BlakeFawley">Blake Fawley</a>
    </i>
  </font>
</div>



### 引言

今天给大家介绍的课程主要是游戏开发导论，首先给大家讲一下什么是游戏，然后讲一下游戏是怎么开发出来的并介绍一下游戏引擎，最后讨论一下怎么去成为一个游戏开发者。

<!--more-->





### 什么是游戏

电子游戏（Electronic Game）是一种在电脑、手机或其它专用电子设备上运行的，具有目标和规则的娱乐形式，简称为游戏。



#### 游戏发展历程

关于游戏的整个发展历程，我们会从家用游戏主机的发展历程来回顾一下。为什么会选择家用游戏主机为代表？主要是因为家用游戏主机主要功能就是用来玩游戏，而像电脑、手机其实游戏只是它们功能中的一部分。



##### 第一世代 1972-1977

代表机型：Odyssey、Telstar系列

1972年是整个家用游戏主机发展的起点，第一款商业化产品Odyssey的推出，标志着家用游戏主机正式迈入第一个世代。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/watermark,image_d2F0ZXJtYXJrLnBuZw,g_se,x_10,y_10-20210228235333117.png)

上图是游戏《PONG》，它是第一款电视游戏，游戏内容是模拟乒乓球对战。



##### 第二世代 1977-1983

代表机型：Atari2600、ColecoVision、Odyssey2、Color TV Game

8-bit处理器，可更换游戏的设计，标志着家用游戏主机进入第二个世代。

第三方游戏开发合法化，由于缺乏监管标准导致涌现出大量垃圾游戏，最终引发了“雅加达震荡”事件。美国的游戏业陷入萧条，家用市场开始由美国向日本转移。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/IMG_7381.jpg)



##### 第三世代 1983-1987

代表机型：任天堂FC、世嘉Master System、Atari7800

进入第三时代后，家用游戏游戏机的重心完全倒向日本，甚至于可以说是任天堂与世嘉一对一的竞争。涌现出诸如《超级马里奥兄弟》《勇者斗恶龙》《最终幻想》等至今仍然活跃的经典游戏系列。

无论硬件产品还是软件阵容，第三世代都是重大的转折点，对未来游戏主机的发展产生了深远的影响。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/quality,q_90.jpeg)





##### 第四世代 1987-1994

代表机型：Mega Drive、Super FamiCom、Neo-Geo、PC Engine

家用游戏主机开始步入16-bit芯片时代。

任天堂的SFC依然是本世纪销量最高的主机，世嘉凭借MD迎来了其在主机硬件历史上的黄金时代。更强的处理芯片、更丰富的控制器设计、更出众的图像表现效果等等，基本都是本世代游戏主机的特色。

缺少具有革命性的重大变革，更多的是稳扎稳打的完善与进步。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/maxresdefault-20210303002455811.jpg)





##### 第五世代 1993-1999

代表机型：Jaguar、3DO、SEGA Saturn、PlayStation、N64

游戏画面的呈现方式逐渐由2D向3D转变。

光盘存储介质也真正全面取代了卡带成为主流的游戏载体，在家用游戏机史上是具有革命意义的里程碑，行业格局发生了天翻地覆的变化。

作为一个后来者，索尼凭借PlayStation一举颠覆了整个行业，获得了巨大的成功。



##### 第六世代 1999-2004

代表机型：DreamCast、PS2、NGC、Xbox

家用游戏主机子辉煌的年代，随着主机性能大幅飞跃，游戏类型再一次得以扩充。出现了众多注重流畅体验和华丽演出的3D动作游戏--《鬼泣》《战神》等。

索尼依然是本世代最大的赢家，但微软的加入一举改变了业界格局并影响至今。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/watermark,image_d2F0ZXJtYXJrLnBuZw,g_se,x_10,y_10-20210304164805012.jpeg)



##### 第七世代 2005-2013

代表机型：Xbox360、PS3、Wii

本世代形成了任天堂、索尼和微软三足鼎立的格局，三台主机的销量非常接近。

高清画面输出与网络服务是第七世代电视游戏主机的两大标志性元素，这是技术进步所带来的必然结果。

本世代的另一个火热的关键词--体感，相信是很多人都不曾预料的。



##### 第八世代 2012至今

代表机型：Wii U、PS4、Xbox One

随着移动游戏的崛起和PC性能上的巨大飞跃，再如以往那样投入巨资研发自主芯片并不明智。

索尼和微软不约而同都选择与主流PC相同的x86架构。对于国内玩家而言，本世代具有里程碑式的重大意义--PS4和Xbox One斗争史在国内推出了行货。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/quality,q_90-20210304164026220.jpeg)





##### 当前 2016至今

代表机型：PS4 Pro、Xbox One X、Nintendo Switch

技术创新与硬件升级的快速迭代，意味着家用游戏主机的更新周期也将随之缩短。

索尼和微软的做法都是通过对已有硬件的小幅升级，搭配最新的软件技术，让主机不至于落后于时代，不过任天堂一如既往地追求创新。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/watermark,image_d2F0ZXJtYXJrLnBuZw,g_se,x_10,y_10.jpeg)







### 游戏是如何开发出来的

#### 游戏开发团队角色划分



#### 经典游戏开发流程





#### 工具和资产



### 游戏引擎

#### 什么是游戏引擎





#### 游戏引擎的发展历程





#### 游戏引擎架构







### 如何成为一个游戏开发者

#### 游戏从业者的两个方向

+ 商业游戏开发者
+ 独立游戏开发者

GDC在2019年做的游戏开发者从业年龄数据统计调查来看，从业年龄在2年以内的年轻人占到整体的20%；有50%的人有3到10年的工作经验；10到20年从业经历的有20%；而超过20年经验的不到10%。

另外一个值得关注的数据是游戏开发者所在公司规模调查，有1/3的人是在百人以上中大型的游戏公司，而还有超过1/3的人是在5人以下的中小型团队做独立游戏。

国际游戏开发者协会IGDA（Developer Satisfaction Survey）在2017年做了一个调查得到的结论：大部分游戏从业者都是拥有大学文凭的，所以学习成绩是非常重要的，必须要有一个好的大学文凭，这里给各位一些建议：

+ 最好有个大学文凭
+ 即便你不喜欢你的专业，也应该努力拿下来
+ 热情很重要，但更重要的是证明你有完成任务的能力
+ 成绩会是对你能力最好的证明



#### 大学应该学什么

那在大学里面应该学哪些东西是能够跟游戏相关的呢？

+ 综合性大学：计算机科学、软件工程
+ 艺术类院校：插画、概念设计、3D建模



#### 入行建议

+ 找到合适自己的方向
+ 打磨手艺 精益求精
+ 坚持学习 拓展视野
+ 持之以恒

入行的方向很多，有程序、美术甚至策划，但是要找到自己合适的方向，打磨手艺精益求精，坚持学习拓展视野，最重要的就是持之以恒。



#### 独立游戏开发者

##### 什么是独立游戏

“独立游戏源”（The Independent Gaming Source）为“独立游戏”所定下的两条定义：

1. “独立发行”，即不通过发行商
2. 开发规模小（不超过20人左右）

##### 建议

+ 不要想太多，早动手
+ 尽早在屏幕上呈现出能动起来的“精灵”
+ 建立一个适合你的健康的工作环境
+ 每时每刻把功夫花在自己的游戏上
+ 不要烂尾，把自己的游戏做完
+ 不要在美术上偷工减料
+ “独立游戏”并不代表一种游戏类型或美学风格
+ 你就是你的作品，理解并开发你自己



#### 大团队中的独立游戏人精神

在一个大的团队里面，我们也是需要一种独立游戏人的精神。

#### 主人公精神

##### 多学

+ 多学如何处理好人际关系
+ 多学专业和非专业技能
+ 多学他人的经验和方法



##### 多想

+ 多想如何做最正确的事情
+ 多想如何用正确的方法做事情
+ 多想是否已经把事情做好
+ 多想自己是入额把事情做好的



##### 多做

+ 多做些力所能及的事情
+ 多做些边界模糊的事情
+ 多做些帮助别人的事情



##### 多管

+ 多管项目进度
+ 多管产品质量



#### 匠人精神

+ 匠人文化的本质：敬业、认真
+ 匠人最典型的气质：对自己的手艺拥有一种近乎自负的自尊心
+ 对手艺要求苛刻，力求做到精益求精，完美再完美



著名的独立游戏《FEZ》的制作人Phil Fish就曾为了追求完美而不惜三次重头来过。

> “......我在FEZ之前没做过点绘，所以我得去学。三年来不断学习，那结果就是你比以前更擅长做这些事，然后所有三年前所画的图，没办法达到你现在所画的相同水准，差距太明显了，所以我得重改一堆旧东西，我整整重做了三次......”

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/ss_c433accea78008474b03f027bc4aacec765f968f.600x338.jpg)



对于独立游戏制作者们来说，游戏已经不单单只是一款摆在货架的商品了，游戏更像是用来展示人生的艺术品，开发者们往往更像是艺术家一样在追求艺术的最高境界。