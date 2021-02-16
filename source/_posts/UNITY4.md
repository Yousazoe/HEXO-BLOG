---
title: Unity基本编译环境设置
banner_img: 'https://tva1.sinaimg.cn/large/008eGmZEly1gmidafmpnfj31400u0wmh.jpg'
abbrlink: 87cbf473
date: 2021-01-10 09:51:25
tags:
- Unity
- Game Develop
categories: Unity 游戏引擎 (Unity Game Engine)
index_img:
comment:
sticky:
---



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/23b2522533cb0ccc023245cef36a75e64b7d2b0a.jpg@860w_482h-20210211170138902.webp)

### 引言

有非常多的朋友加入到Unity游戏开发中，但是同时也有非常多的朋友卡在了一开始的配置环境部分。直接导致 MonoBehavior 白色，代码无法自动补全等问题。为了一次性解决新人都可能面对的问题，我决定写下这个指南希望你们都能顺利开始学习Unity游戏开发！



<!--more-->

> 作者：M_Studio
> https://www.bilibili.com/read/cv9764864#reply4100644546
> 出处： bilibili



**基本说明：**

+ 中国 Unity 官网下载地址：https://unity.cn/releases

+ 请下载 **Unity HUB** 来管理和安装你的 Unity 各种版本

### 场景一：

Windows系统 ｜Unity 2020之前的版本 ｜Visual Studio Community编辑器

+ 电脑中**没有任何代码编辑器**的情况下，请使用 Unity HUB 安装 Unity 的时候勾选 Visual Studio Community

  这样 HUB 会帮你自动下载安装并配置好 Visual Studio 作为你的代码编辑器（强烈推荐）

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/bd387563be5ee2a0b9aa3e52c45da58c480beffe.png@1320w_746h.webp)

进入 Unity 后找到 Preferences (Windows在Edit菜单下/Mac在Unity菜单下) 找到 External Tools 将 External Script Editor 设置为 Visual Studio 或其他你想使用的编辑器

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/50e55f20b596109ea9a7f22693b6a1b147a48eba.png@1320w_1024h.webp)

这是最简单也最方便的方法，希望刚入门的小伙伴选择这种方法。Mac平台直接在 HUB 中安装 VS 即可




电脑中由于自己曾经学习过其他变成语言安装过 Visual Studio 不想删除重新安装怎么办？

1. 打开你的 Visual Studio 找到 工具 - 获取工具和功能 （如图）

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/85e13d4d94f2a2d63f48d19c624f18b05fd8689b.png@1320w_1232h.webp)

2. 在打开的窗口中点击 单个组件 然后搜索 Unity 安装所有跟 Unity 相关的组件

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/bf58ed851b9100a8fd2be90e02cca171e8b60335.png@1320w_736h.webp)

3. 重复上一个情况中设置编辑器的界面点击 Regenerate project files 只会卡一帧不需要额外的其他确定操作就可以使用了

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/bf58ed851b9100a8fd2be90e02cca171e8b60335.png@1320w_736h-20210211102457785.webp)

### 场景二：

Windows系统 ｜Unity 2020.x版本 ｜Visual Studio Community编辑器

+ 如果你按照场景一的步骤已经实现在 Unity2019.x 中正常编辑代码有补全，那么理论上你正常升级到 2020.x 也是可以自动补全的。

+ 如果你发现不能补全，请去到 **Window - Package Manager** 在 **In Project** 中找到 **Visual Studio Editor** 选择 **Remove** 移除即可实现**代码补全｜双击代码打开VS**




### 场景三：

Windows & MacOS 系统 ｜Unity 任何版本 ｜Visual Studio Code编辑器

+ 首先请**确保**你能正常使用 VS 进行代码编辑

+ **不建议新人折腾** Visual Studio Code 特别是 Windows 的小伙伴（外貌协会除外）

+ 详细步骤跟随 **微软官方指南** ：https://code.visualstudio.com/docs/other/unity

**注意事项：**

1. 重复场景一中的步骤将 **Visual Studio Code** 设置为默认编辑器后，点击 **Regenerate project files**

2. 找到 **Package Manger** 确保 **Visual Studio Code Editor** 为最新版本

3. 视频介绍内容参考我曾经出过的教程：BV19741167zU

**需要安装的 Visual Studio Code 插件参考：（基本必装）**

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/495125e4b3785afb4ab2635348e7180ff5856eb7.png@1320w_3046h.webp)

希望你能成功配置好你的编译环境跟着我一起学习Unity。


