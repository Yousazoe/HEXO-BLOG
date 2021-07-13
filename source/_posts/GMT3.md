---
title: 《空洞骑士》的关卡设计
comment: false
tags: Hollow Knight
categories: 游戏制作工具箱 (Game Maker Toolkit)
abbrlink: d313cddc
date: 2021-07-12 22:50:05
type:
banner_img:
index_img:
translate_title:
top:
mathjax:
---

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210712225336463.png)

<div align=center>
  <font size="3">
    <i>
      <a href="https://www.pixiv.net/artworks/67023394">0129</a> by 
      <a href="https://www.pixiv.net/users/9713408">IIIIIIInari!</a>
    </i>
  </font>
</div>






### 引言

《空洞骑士》的故事发生在地域庞大的“圣巢”：一个有森林、矿井、盆地和污水系统的地下昆虫王国。本期文章中，马克·布朗将从地图结构、探索顺序等方面考察这款也许是史上最出色的“银河恶魔城”作品。

<!--more-->



<br/>

> 本文是观看完 [Game Maker's Toolkit](https://www.youtube.com/channel/UCqJ-Xo29CKyLTjn6z2XwYAw) 的 [The World Design of Hollow Knight | Boss Keys](https://www.youtube.com/watch?v=7ITtPPE-pXE) 后深受触动，决定整理一份文字版以供大家参考，中文制译可以移步 [卡姐Cara](https://space.bilibili.com/180052141) 的 [【Boss Keys】《空洞骑士》的关卡设计 The World Design of Hollow Knight | Boss Keys](https://www.bilibili.com/video/BV11J411Q7Zp?from=search&seid=13712551978212770642)，欢迎赞助作者：https://www.patreon.com/GameMakersToolkit 和译者。

<br/>



如果你是银河恶魔城游戏的粉丝，那你肯定记得难熬的2010年。一方面，《银河战士：另一个M》推出：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210712230624631.png)

这款游戏对“孤独与探索”并不上心，却更钟情于激烈的战斗、令人尴尬的过场和泛滥的提示。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210712231114332.png)



另一方面，继六款出色的“恶魔城”掌机游戏后，我们迎来了《恶魔城：暗影之王》。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210712231304470.png)



这款华丽的动作游戏深受“战神”的影响，却鲜有探索元素，看起来像“银河恶魔城”已死......

然而并非如此，因为任天堂和科乐美正要让他们的经典IP去沉睡十年之时，一些开发者，尤其是小型独立工作室开始涉足“迎合恶魔城”领域。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210712231629042.png)



《洞窟物语》（2004）、《安琪拉之歌》（2007）和《暗影帝国》（2009）：



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210712231950795.png)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210712231905517.png)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210712232042037.png)



这些早期作品都继承了解锁区域、获取技能、网状地图和搜集物品的传统。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210712232400363.png)

之后，类似的游戏纷呈迭出，《出击飞龙》（2014）、《公理边缘》（2015）、“桑塔”系列、《小鸡快跑2》（2012）、《墨西哥大混战》（2013）、《首席登陆舱》（2016）以及《奥里与黑暗森林》（2015）：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210712233438426.png)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210712233247830.png)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210712233825326.png)



但这些作品都不及2017年的一款作品。这是款神作，因为爽快而富有想象力的Boss战、匹配“魂系”游戏的超高难度，还有丰富深邃的剧情供玩家取材。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210712234241350.png)

最重要的是，它地图设计精巧、错综复杂，令人流连忘返，今天我将深入探究这款游戏的关卡设计。



### Hallownest's layout

《空洞骑士》的故事发生于庞大的王国“圣巢”。游戏始于“德特茅斯”，这座破败的小镇只有寥寥几个商店和探险者。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210712235419363.png)

它的下方是“遗忘十字路”，从名字就能猜到，它连结着游戏许多区域，比如葱葱郁郁的“苍绿之径”、死气沉沉的“水晶山峰”、布满酸液的“雾之峡谷”以及有毒洞穴“真菌荒地”。

在圣巢最深处，你会发现漆黑的迷宫“深邃巢穴”，以及神秘的“古老盆地”。地图最遥远的角落有座坟墓，名为“安息之地”，还有“呼啸山庄”和苍翠茂密的温室“王后花园”。在王国的边缘，你会找到“王国边境”，它也毗邻“蜂巢”。

所有这些区域都围绕圣巢宏伟的首都：阴雨连绵的“泪水之城”和污水系统“皇家下水道”。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210712235532117.png)



所以，这15个不同区域像拼图般镶嵌在一起。每个区域都有不同的观感，你绝不会混淆“水晶山峰”的粉红宝石、“苍绿之径”的墨绿高墙、“遗忘十字路”的昏暗幽蓝、“古老盆地”的凝重墨灰......而且各区域主题色一致，看着一目了然。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/WechatIMG4.jpeg)

这些设计让你在脑海里能分别记忆每个区域，极大地帮助你寻路和空间推理。你还会发现不同区域玩法各异，让游戏保持新鲜多样，比如你要在“真菌荒地”跳蘑菇蹦床、在“水晶山峰”躲避光阵、在“深邃巢穴”抹黑前行。

某些区域如“王国边境”，地形天然垂直。而其他区域，如“皇家下水道”则像公路延伸。每个区域也都有独特敌人，如“苍绿之径”的爆炸虫、“雾之峡谷”的自杀水母、“深邃巢穴”的粘人蜘蛛、“蜂巢”的可爱小蜜蜂，每个区域都充满新鲜感。



### Exploring Hallownest

当我们初次踏入“圣巢”，眼前没有任何具体目标与方向，开场动画里的孤独漫游者，那个神秘骑士，悄然抵达王国，然后一跃而下。但我们还是会得到些含糊的方向提示，比如“德特茅斯”的虫长者要你往下走：



而“遗忘十字路”最西边的路牌指向“王国的中心城”，据说那是个“希望会成真，真相会显露”的地方：

