---
title: 欢迎来到C++
comment: false
tags: Cpp
categories: Cherno的C++笔记 (Cherno C++)
abbrlink: e5bd4d2
date: 2021-03-07 10:44:09
type:
banner_img:
index_img:
translate_title:
top:
mathjax:
---





![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/49ff1661408483.5a6df91d1e93d.png)

<div align=center>
  <font size="3">
    <i>
      <a href="https://www.behance.net/gallery/61408483/Memories">Memories</a> by 
      <a href="https://www.behance.net/MChahin">Mohamed Chahin</a>
    </i>
  </font>
</div>


### 引言

这个系列将讲解C++需知道的一切内容，涵盖这门语言的基础知识。本节将会简单介绍C++这门语言并学会在不同平台（Windows、MacOS、Linux）安装以及C++是如何工作的。



<!--more-->



学习C++对游戏开发大有裨益，然而C++不仅仅适用于游戏。

### 为什么学习C++

我为什么要学习C++？这是不是一种过时的语言？现在学习C++有什么好处？

当你需要编写性能良好的代码时，C++仍然是最常用的语言；或者你正在为一个奇怪的架构或平台编写原生代码并且想获取对硬件的进程控制，C++也是不二选择；在游戏行业中，例如Unity、Unreal、Frostbite等游戏引擎都是用C++写的......

问题在于问什么我们想要直接访问硬件？为什么所有这些游戏引擎都是用C++编写的，为什么不用另一种语言？

#### 底层

使用C++最大的原因是直接控制硬件。我们来讨论一下C++的工作原理：你用C++写的代码被送去编译器编译，这些编译器将代码输出为目标平台的机器码（设备在CPU实际执行的指令），使用C++我们完全可以控制CPU执行的每一条指令。

#### 平台

如果你问C++可以运行在什么平台，答案是几乎所有平台，你只需要找到为该平台输出机器码的编译器，例如x64编译器将输出x64机器码从而在64位CPU上运行。举个例子，一些平台通常被用于开发C++程序：Windows、Mac、Linux和其它几乎所有桌面操作系统以及移动操作系统IOS、Android......我们同样可以在所有游戏主机上编写C++程序，包括Xbox、PS以及任天堂的3DS、WiiU、Switch等等。当你需要广泛的平台支持时，C++非常棒因为只要有一个编译器你就可以让C++编译成在该平台运行的本地代码。

当然还有其他的本地计算机语言，但C++是自80年代初以来就广泛使用并广受欢迎，每个人都知道，每个人都在使用它。其他诸如C#或Java的语言之所以不同是因为它们是在虚拟机上运行的，这意味着你的代码首先被编译成一种中间语言，当你在目标平台上运行你的应用程序时虚拟机运行程序再转换为机器码。

想象一下，假设你用英语写了一本书，但你想让一个只会说德语的德国人读你的书，所以你决定要做的就是在德国书店里卖英文版的书。然而当你买这本书时，你还会有一个真人翻译陪你回家。当这个德国人回到家想读这本书的时候，翻译用英文朗读了这本书，然后再开始用德语为这个人翻译整本书。这有点像在虚拟机上运行的代码，当然你把书本身翻译成德语然后在德国的书店出售效率会更高，也是C++与C#、Java之类的语言的区别：C++是本地语言，C++编译器为目标平台和目标架构生成机器码，不需要翻译只要把机器代码指令放入CPU运行它们，CPU就会执行这些指令。



### 学习内容

当然本地语言不意味着它会很快，如果你写垃圾代码的话它会很慢，事实上它甚至可能比虚拟机语言比如C#和Java更慢，因为它们倾向于运行时做系统优化，所以如果你C++代码写的不好，C++肯定会比C#或Java更慢。正因为如此，我喜欢使用这类语言，当我只是需要合适的工具或不需要我压榨每一点性能的时候C#是一种非常好的语言，但是当我们真正需要性能的时候我们就需要C++。

我们将学习如何正确书写的简单技巧、如何写好代码、如何写出快速的代码。

你可能会问我们要讲些什么呢？一开始我们将从C++基础开始，如果我们关心性能之后将讨论使用C++库的好处，我们会讲到C++如何运行，会谈到内存与指针、池、自定义构造函数、移动语义、模板等如何正确的使用。我们还会讨论宏，以及如何在多个平台上编程，编写我们自己的数据结构使它们比C++库的更快更安全，我们甚至会涉及底层优化，通过编译器内联、汇编，写自己的Maps和SSE指令集。



### 配置安装

今天让我们把工具准备好，为了让我们用C++写程序我们需要一台计算机和一套工具，而这些工具将取决于你使用的操作系统：

#### Windows

Windows是非常好的选择，因为Windows是游戏行业中使用最广泛的操作系统。现在要写C++代码，你真正需要的只是一些文本编辑器，比如记事本就会做的很好。然而如果你在一个`.txt`文件中写C++代码我们需要通过编译器来生成一些可执行的二进制文件，这样我们才能运行我们的程序，所以我们需要至少有一个编译器：我们会把那个`.txt`文件转换成一个程序。

然而我们可以做得更好，因为写C++程序并不简单。如果你用的是notepad这对你一点帮助也没有，所以你需要做的是找到一个开发环境也就是所谓的集成开发环境，它会帮助我们编写和调试代码。既然我们是Windows，我们将使用Microsoft VisualStudio，这几乎是现在最好的IDE，它远非完美，但这是我们所能拥有的最好。我用过很多不同的IDE，到目前为止它是我最喜欢的。VisualStudio还有许多插件，可以在任何平台帮助你比如：PC、移动终端、游戏主机等。这就是为什么它是游戏行业中最受欢迎的IDE。

言归正传，让我们把它安装好。这里我们是Windows10，不管你用的是什么版本的Windows我们先看看[https://visualstudio.microsoft.com/zh-hans/](https://visualstudio.microsoft.com/zh-hans/)：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210307232108262.png)

我们有Community社区版，它是完全免费的：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210308221028430.png)



下载完成后我们要安装它并花费大量时间，新版本VisualStudio速度快得多，还有一些非常不错的新特性，也是我们在整个系列中用到的IDE。之后的安装和往常一样，我们选择需要的组件：

+ C++桌面开发
+ .NET桌面开发

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210307232212373.png)

点击安装，现在它会开始下载和安装我们需要的所有东西。安装完成后启动，可能需要登陆账户，注册一个新的微软账户或直接登录即可。

我很喜欢自定义设置之类的东西，例如在工具的设置选项中，我们可以改成dark黑暗模式：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210308221120765.png)



现在我已经按我喜欢的方式设置了VisualStudio，包括语法高亮之类的东西。如果你们想使用和我一样的配置可以直接去访问我的[https://thecherno.com/vs](https://thecherno.com/vs)网站，网址有下载链接下载这个`.vssettings`。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/2781615129427_.pic_hd.jpg)

进入VisualStudio，在工具的选项中选择导入和导出设置，选择导入选定的环境设置：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210308221740460.png)

保存当前设置时导入新配置，覆盖当前配置：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210308221958762.png)



导入刚才的设置，在我的电脑的文档中：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210308222354509.png)



这样配置就导入VisualStudio了，现在让我们新建一个C++空项目：



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210308233144000.png)



我不喜欢把工程放在默认的文件目录的原因是首先这个路径太长了，第二点这个路径中很可能包含空格符的，这将导致一些插件出现兼容问题，例如安卓插件如果路径中有空格就无法工作。

我们命名为`HelloWorld`，将`HelloWorld`打印到控制台并测试整个环境。下面还有一个叫做解决方案的东西，Solution就是一组相互关联的项目（Project），它们可以是各种项目类型，基本上解决方案就像是工作台，每个项目本质上就是一组文件，不管它是一个库还是一个实际的可执行文件都会被编译成某种目标二进制文件

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210309000357551.png)



鼠标右键点击源文件（Source），点击Add添加新项目（New Item）选择C++文件取名为`main.cpp`，编写以下程序：

```c++
#include <iostream>

int main(){
  std::cout << "Hello World" << std::endl;
  std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210309000330433.png)

控制台输出`HelloWorld`，说明环境配置成功。



#### MacOS

你可以使用很多不同的工具在Mac上构建C++应用程序，但我要推荐的是XCode。Xcode是苹果公司开发的IDE，它还不算太糟，在大型项目上可能会很慢，例如EA公司用Xcode为IOS开发游戏时某些程序的编译时间会超过20分钟，比如《极品飞车：无极限》。实际上对于写代码也是一场噩梦，因为当你做一个大型项目时所有的东西都被延迟，但像学习C++这样的小项目，我仍然认为XCode是最好的IDE，让我们来安装它。



进入Appstore，搜索栏输入XCode：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-03-07%20%E4%B8%8B%E5%8D%881.29.39.png)



XCode安装好后让我们打开它，接受所有的条款和条件，XCode将继续为我们安装一些组件：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-03-07%20%E4%B8%8B%E5%8D%881.35.08.png)



完成后我们将创建一个新的XCode项目，选择模板时点击MacOS，然后选择命令行项目：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-03-07%20%E4%B8%8B%E5%8D%881.36.47.png)



我们给这个项目起个名字`HelloWorld`，然后在语言下面选择`C++`。你必须输入你的组织标识，比如com.你的公司名，这是某种唯一标识符但并不重要：



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-03-07%20%E4%B8%8B%E5%8D%881.39.37.png)



选择好项目的存储位置后基本OK了，这就是XCode项目的样子：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-03-07%20%E4%B8%8B%E5%8D%881.44.57.png)

<br/>

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-03-07%20%E4%B8%8B%E5%8D%881.47.11-20210307135152889.png)

可以看到，我们已经有了一个`main.cpp`文件，它已经有了一些默认的代码，但我们还是重写已匹配其他平台：

```c++
#include <iostram>

int main(){
    std::cout << "Hello World" << std::endl;
    std::cin.get();
}
```



如果这是你第一次运行XCode，则必须启用`Developer Mode`。编译成功后应该在底部弹出一个控制台显示我们的编译输出，按下回车键程序成功终止：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-03-07%20%E4%B8%8B%E5%8D%881.53.37.png)



这样我们已经启动了XCode并运行了它，终于准备好学习C++了。



#### Linux

您正在使用Linux开发C++代码，让我们介绍一下如何在Linux上设置所需的工具以便制作C++程序示例。当然有很多不同的工具很多不同的方法来编写和构建你的代码，我将介绍其中一种方法。

我希望你已经准备好一堆设置了，我的意思是既然你选择了Linux显然要一些准备工作。基本上我们将使用CMake在CodeLite编译器上生成工程文件，CodeLite是一个很好的轻量级IDE，它基本上可以做你所期望的所有事情，让我们用它轻松编写代码。

这里我们有一个虚拟机，虚拟机里面安装的是Linux Mint 18.1版本，桌面是KDE。我们要做的第一件事就是打开终端建立一个`Dev`目录：

```bash
mkdir Dev
cd Dev
mkdir HelloWorld
cd HelloWorld
```

这个目录放我们开发的东西，在这个目录内部每个项目都有一个文件夹。我们实际需要安装的应用程序是一个编译器、CMake以及CodeLite。首先我们要做的就是`sudo apt-get update`输入root账号的密码，然后会更新安装包及安装包仓库：

```bash
sudo apt-get update
[sudo] password for root:password
```

这些完成之后我们可以安装我们需要的软件包：

+ vim作为我们的终端文本编辑器
+ g++作为编译器
+ codelite作为IDE
+ CMake

```bash
sudo apt-get install vim g++ codelit cmake
```

在完成下载之后我们来创建一个名为`src`的目录放我们所有的源文件，在里面新建一个`Main.cpp`：

```bash
ls
mkdir src
touch src/Main.cpp
```



我们需要CMakefile来构建脚本，这样我们就有一个简单的方法来生成项目。用vim来写CMake，这个文件命名为`CMakeLists.txt`，这个文件告诉CMake我们将如何构建项目文件。

首先我们要指定一个最低版本的CMake，根据经验用3.5版本即可。然后是项目名称`HelloWorld`，同时设置一些变量比如我们用于编译的标记和我们使用的标准库。我们在设置一个源文件目录的变量`source_dir`指向这个项目的源文件`src`目录，这个`PROJECT_SOURCE_DIR`就是当前目录

```cmake
cmake_minimum_required (VERSION 3.5)
project (HelloWorld)
set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Werror -std=c++14")
set (source_dir "${PROJECT_SOURCE_DIR}/src/")
```



我们已经设置了编译标志和源文件目录，现在我们需要告诉编译器哪些文件要编译。所以在CMake中用`GLOB`来制定在`src`目录中的源文件，这个目录下后缀为`.cpp`的文件都需要编译。

如果你还有`include`目录，你同样需要设置它但现在我们不打算那样做。`add_excutable`是我们的目标可执行文件设定，`HelloWorld`是项目名，然后是我们想要传入该项目中的文件，它们将是我们的源文件，如果你需要`include`目录之类的这里也是支持的。

```cmake
file (GLOB source_files "${source_dir}/*.cpp")
add_excutable (HelloWorld ${source_files})
```



ok，CMakeLists文件写完了，写入并推出（`:wq`）然后要写一个脚本来运行CMake，脚本命名为`build.sh`。这并不是编译代码，它只会生成项目。

```bash
vim build.sh
```



我们要做的第一件事就是确保批处理脚本能够运行，因此我们添加一句`#!bin/sh`，每个批处理脚本都有这句。关于目标我们使用`CodeLite - Unix Makefiles`，对于编译类型我们设置为`Debug`模式，毕竟大部分我们都是在`Debug`模式下：

```sh
#!bin/sh
cmake -G "CodeLite - Unix Makefiles" -DCMAKE_BUILD_TYOE=Debug
```



现在我们已经准备好运行我们的脚本，在Linux中运行脚本你必须把脚本标记为可执行的，所以我们就用`chmod +x build.sh`，就给了这个脚本可执行权限：

```bash
chmod +x build.sh
./build.sh
```



现在我们可以运行它，你可以看到它为我们写了一些构建文件，如果我们`ls`看一下目录，你将看到有许多新文件。现在我们用CodeLite打开（如果你想在后台打开它，在后面加上`&`就行了）：

```bash
ls
build.sh CMakeFiles cmake_install.cmake CMakeLists.txt HelloWorld.project HelloWorld.workspace MakeFile src
codelite HelloWorld.workspace
```



在CodeLite中编写代码：

```c++
#include <iostram>

int main(){
    std::cout << "Hello World" << std::endl;
    std::cin.get();
}
```





### C++是如何工作的

写C++程序的基本流程是你有一些C++源文件，然后将这些源文件给到编译器，编译器将其转变成二进制的东西（可能是某种库或者是可执行文件），本节我们将主要讲可执行程序。

打开VisualStudio，我们在Windows如何安装C++中已经有了`HelloWorld`程序，它非常基础但包含不少知识点。

首先我们有`#include <iostream>`语句，这个叫预处理，在`#`符号之后都是预处理语句。编译器收到源文件后，一看到这条语句就先处理这些预处理语句，这也是为什么叫做预处理了，因为它在实际编译之前就被处理了。

`include`的含义是它需要找到一个文件（本例中需要找到`iostream`的文件）然后将该文件所有内容拷贝到现在的文件内，这些包含文件通常称为“头文件”。我们之所以要包含`iostream`这个头文件是因为我们需要一个被调用的函数声明，`std::cout`可以让我们在终端打印东西

```c++
#include <iostram>
```



接下来是`main`函数。`main`函数非常重要，因为任何一个C++程序都有`main`函数。它是程序的入口，这意味着当我们运行程序时计算机就从这个函数开始执行代码，当程序还是运行时计算机会逐行执行我们的代码。当然，程序也可以中断或者改变执行的顺序（控制语句或函数调用），但最重要的还是一行一行执行。

```c++
int main(){
		......
}
```

因此，我们的程序首选被执行的是：

```c++
std::cout << "Hello World" << std::endl;
```

然后才是：

```c++
std::cin.get();
```

运行完`main`中的所有东西后我们的程序结束了。现在对于那些了解函数的人会发现`main`函数的返回类型是`int`，然而我们并没有返回`int`，这是因为`main`函数比较特殊，它不一定需要返回值，如果你不返回值的话它会默认你返回了0。

好了，我们继续讨论更多细节。这两个左箭头`<<`符号看上去很奇怪，其实它们只是写成这个样子并没有更多实际的意义。这些看起来像左移运算符的东西实际叫做重载运算符，你可以把它理解为一个函数将字符串`Hello World`推送到`cout`流中然后打印到终端，然后推送一个行结束符`endl`告诉终端跳到下一行：

```c++
std::cout << "Hello World" << std::endl;
std::cout.print("Hello World").print(std::endl);
```

`cin.get`函数是等待我们按下`enter`键，在前往下一句代码之前等待，这个时候程序暂停执行直到我们按下回车键后，程序继续运行下一行，但程序已经没有下一行了所以返回0，意味着代码执行完毕。

现在我们写完了`main.cpp`的源文件，下一步该怎么把它转换成可运行的二进制文件？首先编译器先处理诸如`#include <iostream>`的预处理语句，拷贝黏贴把`iostream`文件内容全部包含进来，这样我们就可以用`cout`、`cin`这些函数了。当预处理语句处理完之后，我们的文件将被编译，这个阶段编译器将所有C++代码转化为实际机器代码，而VisualStudio中有些非常重要的设置决定我们怎么转化代码。

在视图左上角你可以看到一个叫解决方案配置，另一个叫解决方案平台，默认是`Debug`和`x86`/`win32`。下拉解决方案配置我们可以看到两个选项`Debug`和`Release`，所有的VisualStudio项目都默认有这两个选项。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210314155825468.png)

在解决方案平台这里，可以看到`x86`和`x64`两个选项。强调一下这些配置只是默认的，配置只是构建项目的时候的一系列规则而已，解决方案平台是指你编译的代码的目标平台。`x86`的意思就是目标平台是windows32位，也就是会生成32位的windows应用程序。其他复杂的项目的目标平台也不相同，你可能在下拉菜单中看到Android平台，如果你想构建、部署、调试Android，解决方案配置这里需设置一系列针对目标平台的规则。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210314155842461.png)

右键项目进入设置，打开VisualStudio的属性页面，这里定义规则用来构建解决方案配置及解决方案平台。首先需要注意到的是`Configuration`和`Platform`，设置成你实际想要的配置与目标平台。你在`Release`的设置对`Debug`没有任何影响，如果你忘了这一点，你会奇怪为什么改了设置没起到一点作用。

回到属性页面我们看到的是常规属性，包括SDK版本、输出目录、中间目录等等。这里的配置类型`Configuration Type`比较重要，设置为应用程序`Application`，编译器会生成二进制文件。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210314155902895.png)



编译器方面的设置在`C/C++`这里，附加包含目录、代码生成设置、预处理定义等配置项都很重要，VisualStudio默认的配置就很好，其实我们啥也不需要做。这些规则控制我们的文件如何被编译，如果你进入到`Optimization`你可以看到`Debug`和`Release`的区别：

+ `Debug-Optimization: Disabled`
+ `Release-Optimization: Maximize Speed `

这就是为什么默认的`Debug`模式会更慢的原因，优化都被关闭掉了，但关掉优化的好处是可以让我们调试代码。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210314161352718.png)

接着我们编译这个文件，在VisualStudio中可以按`ctrl`+`F7`快捷键。输出窗口显示`main.cpp`编译成功：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210314160007906.png)

如果我们故意搞点语法错误例如忘记一个分号：

```diff
#include <iostram>

int main(){
    std::cout << "Hello World" << std::endl;
-   std::cin.get();
+   std::cin.get()
}
```



再次编译我们将看到报错。VisualStudio有很多不同的方法显示错误信息，一种是错误列表，另一种在输出窗口里面，事实上这个错误列表就是个垃圾，看起来也许可以从里面读到一些信息但你绝对不能依赖它，而它经常缺失一些信息。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210314160344987.png)



错误列表的工作原理是分析输出窗口，然后找到`error`这个单词，并抓取这部分信息展示出来然后放进错误列表中，所以这个只能用来作参考。它就是个大概，如果你需要细节需要所有的出错信息，那就看输出窗口，本例中输出窗口提示我们`main.cpp`中出现语法错误，也就是我们的缺失分号`;`，它告诉你出错行。

当我们单独编译的时候链接还没发生，很明显我们编译单独一个文件不会进行链接，让我们看看编译器编译后都生成了什么：



默认情况下，VisualStudio会输出构建文件到`Debug`文件夹，在该文件夹下我们会看到`main.obj`。这是我们的编译器生成的目标文件，对于项目中的每一个C++文件都会生成一个`.obj`文件。我们回到VisualStudio选择`Build`项目，这次就不是编译单个文件了，而是构建整个项目，实际上你会看到生成了`.exe`文件：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210314233855008.png)

我们回到源文件中，在解决方案目录下找到我们的`HelloWorld.exe`，我们可以运行它并打印`Hello World!`：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210314233912669.png)

总的来说很简单，但如果是多个C++文件呢？我们看个简单的例子，假设我们仍然要打印`Hello World!`，但我不想用`cout`函数，我想用自己的`logging`函数包裹`cout`函数，因此我们建立一个函数`Log()`，参数是`message`，作用是打印这个`message`到终端：

```c++
#include <iostram>

void Log(const char* message){
    std::cout << message << endl;
}

int main(){
    Log("Hello World!");
    std::cin.get();
}
```



现在我们把这个函数放在另外一个文件中，我不喜欢一个`main`文件包含所有东西，我希望把我的代码分到很多文件当中这样可以保证代码干净整洁。在源文件新建一个`.cpp`文件并命名为`Log`，把刚才的`Log()`函数裁剪到`Log.cpp`：

```c++
#include <iostream>

void Log(const char* message){
   std::cout << message << endl;
}
```





再回到`main.cpp`，我们将一个函数移动到另一个地方，然后我们对每个文件进行单独的编译。`main.cpp`文件并不知道还有一个叫`log`的函数，因为不认识所以报错。我们可以通过调用申明来修复该错误，申明就像我们宣布有个叫`Log()`的函数是存在的，这就像是一个承诺告诉编译器这里有个名叫`Log`的函数，编译器只需要相信我们就好了，它并不关心这个函数是在哪儿定义的。

```c++
#include <iostram>

void Log(const char* message);

int main(){
    Log("Hello World!");
    std::cin.get();
}
```



可能有人会好奇编译器是怎么知道`Log()`函数会在另一个文件中呢？答案就是编译器会相信我们。又有人会问它怎么实际运行到正确的代码，这里就需要链接了。当我们构建整个工程而不是单个文件时，如果我右键点击`Build`，我的所有文件都会被编译，链接器会找到正确的`Log()`函数定义在哪里，将函数定义导入到`Log()`函数中。如果我们找不到定义将会出现链接错误。

链接错误看起来比较吓人，我们来看个例子。假如我们把函数的名字改成`Logr()`单独编译这个文件，你会发现没有问题。然而当我们点击项目`Build`，我们在错误列表中看到了非常吓人的错误信息，在输出窗口也有这些错误信息：

```diff
#include <iostream>

- void Log(const char* message){
+ void Logr(const char* message){		
    std::cout << message << endl;
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210314233816143.png)



之所以看上去吓人是因为有一些我们自定义函数的额外信息，例如根据惯例会显示调用函数的系统内部命名，其实也就是告诉我们这个无法解析的外部函数`Log`它的返回值和参数都是什么。相对于`mian.cpp`来说，无法解析的外部符号是指链接器无法解析这个符号。

链接器的工作是连接函数，但它找不到`Log`函数连接到哪儿，因为我们并没有一个叫`Log`的函数，所以修复此问题只需要把`Logr`改回`Log`即可。编译成功后回到源文件你会看到两个`.obj`文件，因为编译器会为每一个源文件生成一个`obj`文件，链接器会将它们合并成一个`.exe`文件。



#### 编译器

让我们来思考片刻大的思路：C++编译器实际上负责什么？我们把C++代码写成文本，然后我们需要一些将文本转换为实际应用程序的方法让我们的计算机可以运行。从文本形式到实际可执行的二进制文件，我们基本上有两个主要的操作需要进行：一个叫做编译，另一个被称为链接。所以说编译器实际上需要做的唯一一件事是将我们的文本拿来，转换它们为一种称为目标文件的中间格式，这些`.obj`文件可以传递到链接。

编译器在生成这些`.obj`时实际上做了几件事。首先它需要预处理我们的代码，这意味着所有的预处理器语句都会先处理，一旦我们的代码被预处理，接下来我们将或多或少地进行记号化和解析，基本上把C++整理成编译器能够真正理解和推理的格式，这基本上就是创建所谓的抽象语法树，它是我们代码的一种基本表示。编译器每天的工作是转换我们所有的代码为常量数据或指令。一旦编译器创建了这个抽象语法树它可以开始实际生成代码，这段代码就是实际的机器执行代码。我们还得到了其他各种数据，比如一个存储所有常量、变量的地方，这基本上就是编译器所做的一切。

这并不复杂，当然，随着代码复杂的增长，它会变得非常复杂。

这里我们有一个简单的`HelloWorld`程序，在解决方案的目录可以找到`main.obj`和`Log.obj`，所以编译器所做的就是为我们的每个`.cpp`文件生成`.obj`文件。现在我们的项目包含的每个`.cpp`文件都告诉编译器要生成一个`.obj`目标文件，这些`.cpp`文件被称为翻译单元。

本质上我们需要意识到C++并不关心文件，文件不是存在于C++中的东西。例如在Java中类名必须是和你的文件名称一样，你的文件夹层次需要和package一样，这是因为Java的要求。C++不是这样，它没有所谓的文件，文件只是提供给编译器源代码的一种方式，你负责告诉编译器你输入的是什么类型的文件以及编译器应该如何处理它。

当然，如果你创建一个文件`.cpp`，编译器会把它当作C++文件；类似的，如果我创建一个扩展名为`.c`或者`.h`文件编译器会将`.c`文件当成C语言文件而不是C++文件；而编译器对待`.h`文件会当成头文件处理，这些基本上都是默认的约定。你也可以更改它，如果你不告诉如何处理，我可以制作`.cherno`文件，只要我告诉编译器这个文件是一个`.cpp`文件，请像编译C++文件一样编译它。请记住，文件没有意义。

我们提供给编译器的每个C++文件，编译器都将把文件变成一个翻译单元，翻译单元会生成一个`.obj`文件。实际上有时在C++文件中包含其他的C++文件变成一个大的C++文件是很常见的，如果你做了这样的事你会得到一个翻译单元，然后得到一个`.obj`文件。这就是为什么术语上有区别，什么是翻译单元，什么是`.cpp`文件，一个`.cpp`文件不一定要等价于一个翻译单元，然而如果你只是做一个C++个人项目你永远不会把它们放在一起，每个C++文件都是一个翻译单元，每个C++文件都会生成一个目标文件。

你可以看到这些生产的`.obj`文件实际上是相当大的，原因是包含了`iostream`。正因如此，这些`.obj`文件实际上相当复杂。我们点击源文件新建一个`math.cpp`写一个非常基本的乘法函数：

```c++
int Multiply(int a,int b){
  int result = a * b;
  return result;
}
```

编译文件，我们可以看到成功了。我们回到输出目录再看一下`math.obj`的大小明显比`main.obj`和`Log.obj`小：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210314233937315.png)



##### include

在我们看`.obj`文件中到底有什么之前，我们来谈谈编译的第一阶段。在预处理阶段，编译器基本上会遍历我们所有的预处理语句并进行处理。我们常用的预处理语句是`include`、`if`、`ifdef`还有`pragma`语句，它告诉编译器到底要做什么，让我们来看看其中一个常用的预处理语句`#include <iostream>`。



`#include`实际上很简单，它指定了你想要包含的文件，预处理器打开那个文件，阅读它的所有内容，然后把它粘贴到你写的文件中。回到VisualStudio新建一个头文件命名为`EndBrace.h`，清除所有的内容仅输入一个右花括号：

```diff
- #pragma once
+ }
```

转到之前写的乘法函数`Math.cpp`，把最后的右花括号去掉：

```diff
int Multiply(int a,int b){
  int result = a * b;
  return result;
-}
```

现在编译该乘法函数，编译器会报错文件末尾不匹配。现在我们来修复代码，只要接上我们的结束括号即可：

```diff
int Multiply(int a,int b){
  int result = a * b;
  return result;
+ #include "EndBrace.h"
```

`ctrl`+`F7`编译成功：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210314234020379.png)

当然成功了，因为编译器做的是打开这个文件复制所有内容，将右括号复制过来，头文件的问题解决了。现在你应该确切地知道它们是如何工作和使用它们。



##### define

实际上有一种方法我们可以告诉编译器输出一个文件，其中包含所有的结果和预处理器的评估情况。回到文件，在C++预处理器属性页将预处理设置到文件，确保正在编辑的配置是所有配置。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210314234113301.png)

再次编译此文件，打开输出目录我们会看到新的`math.i`文件，这是我们预处理后的C++代码。让我们在文本编辑器中打开它：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210314234129730.png)

```
#line 1 "E:\\Dev\\CppSeries\\ChernoCpp\\HelloWorld\\HelloWorld\\math.cpp"
int Multiply(int a, int b) {
 int result = a * b;
 return result;
    #line 1 "E:\\Dev\\CppSeries\\ChernoCpp\\HelloWorld\\HelloWorld\\EndBrace.h"
}
#line 5 "E:\\Dev\\CppSeries\\ChernoCpp\\HelloWorld\\HelloWorld\\math.cpp"
```



这里你可以看到预处理器实际上生成了什么，你可以看到我们的源代码包含了`EndBrace.h`，预处理器代码刚把我们的`EndBrace.h`文件插在这里。让我们添加更多的预处理器语句，看看发生什么：

```c++
#define INTEGER int

INTEGER Multiply(int a,int b){
  INTEGER result = a * b;
  return result;
}
```

`define`预处理语句基本上只进行搜索`INTEGER`并将其替换为后面的内容，所以虽然我们没有使用`int`，但最终效果还是`int`。再次返回`math.i`：

```
#line 1 "E:\\Dev\\CppSeries\\ChernoCpp\\HelloWorld\\HelloWorld\\math.cpp"


int Multiply(int a, int b) {
 int result = a * b;
 return result;
}
```



如果我们做了蠢事比如把`int`写成了`Cherno`，那么回到文件我们会发现`INTEGER`都换成了`Cherno`。



##### if

`if`预处理器语句可以让我们包含或排除基于给定条件的代码。这里我只写`#if 1`，这句话的意思是`if`为真，在函数末尾写上`endif`：

```c++
#if 1
int Multiply(int a,int b){
  int result = a * b;
  return result;
}
#endif
```

编译后查看`math.i`文件：

```
#line 1 "E:\\Dev\\CppSeries\\ChernoCpp\\HelloWorld\\HelloWorld\\math.cpp"

int Multiply(int a, int b) {
 int result = a * b;
 return result;
}
#line 7 "E:\\Dev\\CppSeries\\ChernoCpp\\HelloWorld\\HelloWorld\\math.cpp"
```



可以看到它和源代码函数没有区别。如果我回到源代码这里把`#if 1`改为`#if 0`，VisualStudio将淡出下面的函数显示它是被禁用的代码，再次编译后查看`math.i`文件：

```
#line 1 "E:\\Dev\\CppSeries\\ChernoCpp\\HelloWorld\\HelloWorld\\math.cpp"





#line 7 "E:\\Dev\\CppSeries\\ChernoCpp\\HelloWorld\\HelloWorld\\math.cpp"
```



没有看到代码，这是一个预处理语句很好的例子。我们把`#if`去掉，然后重新加入`#includ <iostream>`并编译，查看`math.i`有将近5万行，最底部是我们自己的函数。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210315120606299.png)

这就是`#include <iostream>`所做的全部工作，它包含了许多其他文件，这也是为什么这些目标文件这么大：因为它们包含了`iostream`，而它包含了大量的代码。

预处理阶段结束我们可以继续实际编译C++代码成机器代码。我们把`#include <iostream>`去除，并在`HelloWorld`项目中禁用预处理输出到文件使之恢复默认设置（不勾选不会生成`.obj`文件）。配置妥当后让我们来看看`.obj`文件的内部是什么，如果用文本编辑器直接打开你会看到它是不可读的二进制，但实际上它是当我们调用这个乘法函数时我们的CPU将运行的机器代码。

让我们转换成对我们来说可能更容易读懂的方式。进入VisualStudio在属性中的`C/C++`项下的输出文件中汇编程序输出由无列表改为仅有程序集的列表，再次编译，目录下会看到一个`math.asm`文件，用文本编辑器打开：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210315120733770.png)

```
; Listing generated by Microsoft (R) Optimizing Compiler Version 19.28.29335.0 

include listing.inc

INCLUDELIB MSVCRTD
INCLUDELIB OLDNAMES

msvcjmc SEGMENT
__85A6F400_math@cpp DB 01H
msvcjmc ENDS
PUBLIC ?Multiply@@YAHHH@Z    ; Multiply
PUBLIC __JustMyCode_Default
EXTRN _RTC_InitBase:PROC
EXTRN _RTC_Shutdown:PROC
EXTRN __CheckForDebuggerJustMyCode:PROC
; COMDAT pdata
pdata SEGMENT
$pdata$?Multiply@@YAHHH@Z DD imagerel $LN3
 DD imagerel $LN3+85
 DD imagerel $unwind$?Multiply@@YAHHH@Z
pdata ENDS
; COMDAT rtc$TMZ
rtc$TMZ SEGMENT
_RTC_Shutdown.rtc$TMZ DQ FLAT:_RTC_Shutdown
rtc$TMZ ENDS
; COMDAT rtc$IMZ
rtc$IMZ SEGMENT
_RTC_InitBase.rtc$IMZ DQ FLAT:_RTC_InitBase
rtc$IMZ ENDS
; COMDAT xdata
xdata SEGMENT
$unwind$?Multiply@@YAHHH@Z DD 025052c01H
 DD 01112316H
 DD 0700a0021H
 DD 05009H
xdata ENDS
; Function compile flags: /Odt
; COMDAT __JustMyCode_Default
_TEXT SEGMENT
__JustMyCode_Default PROC    ; COMDAT
 ret 0
__JustMyCode_Default ENDP
_TEXT ENDS
; Function compile flags: /Odtp /RTCsu /ZI
; COMDAT ?Multiply@@YAHHH@Z
_TEXT SEGMENT
result$ = 4
a$ = 256
b$ = 264
?Multiply@@YAHHH@Z PROC     ; Multiply, COMDAT
; File E:\Dev\CppSeries\ChernoCpp\HelloWorld\HelloWorld\math.cpp
; Line 1
$LN3:
 mov DWORD PTR [rsp+16], edx
 mov DWORD PTR [rsp+8], ecx
 push rbp
 push rdi
 sub rsp, 264    ; 00000108H
 lea rbp, QWORD PTR [rsp+32]
 mov rdi, rsp
 mov ecx, 66     ; 00000042H
 mov eax, -858993460    ; ccccccccH
 rep stosd
 mov ecx, DWORD PTR [rsp+296]
 lea rcx, OFFSET FLAT:__85A6F400_math@cpp
 call __CheckForDebuggerJustMyCode
; Line 2
 mov eax, DWORD PTR a$[rbp]
 imul eax, DWORD PTR b$[rbp]
 mov DWORD PTR result$[rbp], eax
; Line 3
 mov eax, DWORD PTR result$[rbp]
; Line 4
 lea rsp, QWORD PTR [rbp+232]
 pop rdi
 pop rbp
 ret 0
?Multiply@@YAHHH@Z ENDP     ; Multiply
_TEXT ENDS
END
```

这基本上是一个可读的结果，可以看到`.obj`文件里面。如果我们往下翻看还会看到我们调用了这个乘法函数，然后我们有一堆汇编指令，当我们运行函数时这些是CPU执行的实际指令。我们的乘法操作实际发生在这里，加载变量`a`进入`eax`寄存器，然后执行`imul`指令将`b`与`a`相乘，`result`变量存储结果然后把`result`返回给`eax`：

```
; Line 2
 mov eax, DWORD PTR a$[rbp]
 imul eax, DWORD PTR b$[rbp]
 mov DWORD PTR result$[rbp], eax
```



很显然这两次`mov`是多余的，如果不把编译器优化设置代码会很慢，因为会做一些无缘无故的事情。所以我们回到`math.cpp`去掉`result`变量，直接返回`a*b`：

```diff
int Multiply(int a,int b){
-  int result = a * b;
-  return result;
+  return a * b;
}
```

再次编译并来到`math.asm`，我们可以观察到指令的变化：`imul`指令直接将`b`与`eax`相乘，而`eax`实际上包含了我们的返回值。

我们在调试模式中编译会使代码看起来很多，它没有做任何优化并且做了很多额外的事情使得我们的代码尽量的丰富多彩，尽可能更容易调试。回到我们的项目，在属性中`C/C++`的优化属性页选择最大优化（优先速度）。如果此时尝试编译代码它会给你一个错误，显示`O2`和`RTC1`是不相容的：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210315144809094.png)

所以我们需要回到代码生成选项确保我们基本运行时检查选项为默认。再次编译，进入汇编文件`math.asm`，哇，看起来小多了：我们只是把变量`a`加载到了寄存器中，然后是乘法，非常简单。所以当我们告诉编译器优化时，编译器实际上会去做这件事。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210315144847566.png)

```
; Listing generated by Microsoft (R) Optimizing Compiler Version 19.28.29335.0 

include listing.inc

INCLUDELIB MSVCRTD
INCLUDELIB OLDNAMES

msvcjmc SEGMENT
__85A6F400_math@cpp DB 01H
msvcjmc ENDS
PUBLIC ?Multiply@@YAHHH@Z    ; Multiply
PUBLIC __JustMyCode_Default
EXTRN __CheckForDebuggerJustMyCode:PROC
; COMDAT pdata
pdata SEGMENT
$pdata$?Multiply@@YAHHH@Z DD imagerel $LN4
 DD imagerel $LN4+42
 DD imagerel $unwind$?Multiply@@YAHHH@Z
pdata ENDS
; COMDAT xdata
xdata SEGMENT
$unwind$?Multiply@@YAHHH@Z DD 040a01H
 DD 06340aH
 DD 07006320aH
xdata ENDS
; Function compile flags: /Odt
; COMDAT __JustMyCode_Default
_TEXT SEGMENT
__JustMyCode_Default PROC    ; COMDAT
 ret 0
__JustMyCode_Default ENDP
_TEXT ENDS
; Function compile flags: /Ogtpy
; COMDAT ?Multiply@@YAHHH@Z
_TEXT SEGMENT
a$ = 48
b$ = 56
?Multiply@@YAHHH@Z PROC     ; Multiply, COMDAT
; File E:\Dev\CppSeries\ChernoCpp\HelloWorld\HelloWorld\math.cpp
; Line 1
$LN4:
 mov QWORD PTR [rsp+8], rbx
 push rdi
 sub rsp, 32     ; 00000020H
 mov edi, ecx
 mov ebx, edx
 lea rcx, OFFSET FLAT:__85A6F400_math@cpp
 call __CheckForDebuggerJustMyCode
 imul edi, ebx
 mov rbx, QWORD PTR [rsp+48]
 mov eax, edi
; Line 3
 add rsp, 32     ; 00000020H
 pop rdi
 ret 0
?Multiply@@YAHHH@Z ENDP     ; Multiply
_TEXT ENDS
END
```



我们来看一个稍微不同的例子，在`math.cpp`这种情况下我们实际上不需要放函数参数，可以直接`5 * 2`：

```c++
int Multiply() {
 return 5 * 2;
}
```

保存该文件，进入属性确保禁用优化。编译并进入汇编文件，你可以看到所做的实际非常简单，只需将`10`移到寄存器`eax`，这个寄存器会存储我们的返回值。`5 * 2 = 10`这种运算两个常数值事情其实没有必要，这被称为常数折叠，任何常数都可以在编译时算出来。

让我们通过引入另一个函数来让事情变得更有趣。举个例子，我要在`math.cpp`写一个`Log()`记录特定消息的函数，当然我并不想真的把它写成记录打印任何东西，因为那就意味着我必须包括`iostream`文件，而这将使事情变得非常复杂。所以我让它返回接收到的信息`message`，而下面的`Multiply()`来调用`Log()`，参数是`Multiply`：

```diff
+const char* Log(const char* message){
+   return message
+}

-int Multiply() {
+int Multiply(int a,int b){
- return 10;
+  Log("Multiply");
+  return a * b;
}
```



回到汇编文件，我们看到了这个`Log`函数，它返回了我们的`message`。你可以看到它把我们的`message`指针移动到`eax`，这是我们用来返回值的寄存器。

```
; Listing generated by Microsoft (R) Optimizing Compiler Version 19.28.29335.0 

include listing.inc

INCLUDELIB MSVCRTD
INCLUDELIB OLDNAMES

msvcjmc SEGMENT
__85A6F400_math@cpp DB 01H
msvcjmc ENDS
PUBLIC ?Log@@YAPEBDPEBD@Z    ; Log
PUBLIC ?Multiply@@YAHHH@Z    ; Multiply
PUBLIC __JustMyCode_Default
PUBLIC ??_C@_08EOBDLMOI@Multiply@   ; `string'
EXTRN __CheckForDebuggerJustMyCode:PROC
; COMDAT pdata
pdata SEGMENT
$pdata$?Log@@YAPEBDPEBD@Z DD imagerel $LN3
 DD imagerel $LN3+37
 DD imagerel $unwind$?Log@@YAPEBDPEBD@Z
pdata ENDS
; COMDAT pdata
pdata SEGMENT
$pdata$?Multiply@@YAHHH@Z DD imagerel $LN3
 DD imagerel $LN3+55
 DD imagerel $unwind$?Multiply@@YAHHH@Z
pdata ENDS
; COMDAT ??_C@_08EOBDLMOI@Multiply@
CONST SEGMENT
??_C@_08EOBDLMOI@Multiply@ DB 'Multiply', 00H  ; `string'
CONST ENDS
; COMDAT xdata
xdata SEGMENT
$unwind$?Multiply@@YAHHH@Z DD 025031201H
 DD 0b20d2312H
 DD 05009H
xdata ENDS
; COMDAT xdata
xdata SEGMENT
$unwind$?Log@@YAPEBDPEBD@Z DD 025030f01H
 DD 0b20a230fH
 DD 05006H
xdata ENDS
; Function compile flags: /Odt
; COMDAT __JustMyCode_Default
_TEXT SEGMENT
__JustMyCode_Default PROC    ; COMDAT
 ret 0
__JustMyCode_Default ENDP
_TEXT ENDS
; Function compile flags: /Odtp /ZI
; COMDAT ?Multiply@@YAHHH@Z
_TEXT SEGMENT
a$ = 80
b$ = 88
?Multiply@@YAHHH@Z PROC     ; Multiply, COMDAT
; File E:\Dev\CppSeries\ChernoCpp\HelloWorld\HelloWorld\math.cpp
; Line 5
$LN3:
 mov DWORD PTR [rsp+16], edx
 mov DWORD PTR [rsp+8], ecx
 push rbp
 sub rsp, 96     ; 00000060H
 lea rbp, QWORD PTR [rsp+32]
 lea rcx, OFFSET FLAT:__85A6F400_math@cpp
 call __CheckForDebuggerJustMyCode
; Line 6
 lea rcx, OFFSET FLAT:??_C@_08EOBDLMOI@Multiply@
 call ?Log@@YAPEBDPEBD@Z   ; Log
; Line 7
 mov eax, DWORD PTR a$[rbp]
 imul eax, DWORD PTR b$[rbp]
; Line 8
 lea rsp, QWORD PTR [rbp+64]
 pop rbp
 ret 0
?Multiply@@YAHHH@Z ENDP     ; Multiply
_TEXT ENDS
; Function compile flags: /Odtp /ZI
; COMDAT ?Log@@YAPEBDPEBD@Z
_TEXT SEGMENT
message$ = 80
?Log@@YAPEBDPEBD@Z PROC     ; Log, COMDAT
; File E:\Dev\CppSeries\ChernoCpp\HelloWorld\HelloWorld\math.cpp
```



你可能想问`Log`函数名称像是被一堆随机字符装饰了，这实际上是函数的签名，这需要唯一地定义你的函数。本质上当我们有多个`.obj`时函数也被定义在多个`.obj`中，链接的工作就是把所有的函数链接在一起，这样做是为了查找这个函数的签名，所以你只需要知道我们调用这个`Log`函数，这就是编译器在你调用函数时实际做的事情，它将生成`call`指令。

回到属性页再次打开优化选择最大优化（优先速度），编译回到汇编文件，你会看到它完全消失了。是的，编译器决定什么都不做，我要删除那段代码。

现在你应该基本上了解了编译器的工作原理，它将获取源文件并输出一个`.obj`文件，`.obj`文件是包含机器代码以及其他我们定义的常数数据的文件。现在我们有了这些`.obj`文件，我们可以将它们链接成一个包含所有内容的可执行文件中，可执行文件包含了需要运行的机器代码，这就是我们如何让C++程序跑起来，非常简单。



#### 链接器

什么是链接？C++链接实际上做什么？链接是一个过程，当我们从源C++文件转到实际的可执行二进制文件，第一阶段是编译源文件。一旦我们把文件编译好，我们需要通过一个叫做链接的过程，现在链接的主要焦点是找到每个符号和函数在哪里并把它们连接起来。记住，每个文件被编译成一个单独的目标文件/翻译单元，它们彼此之间没有关系，这些文件不能交互，所以如果我们决定把我们的程序分割成多个C++文件，我们需要一种方法把这些文件连接在一起成一个项目，而这就是链接器的主要目的和要做的事情。

即使你在外部文件中没有函数，比如你就在一个文件中写完整个程序，应用程序仍然需要知道入口点在哪里，换句话说`main`函数在哪里。当你实际运行你的应用程序时，C++运行库时会说：嘿这是`main`函数，我要跳到这里然后开始执行代码，这实际上是你的应用的起始位置，所以它仍然需要把`main`函数链接起来。

我们来举一个没有其他所有的文件的例子。在VisualStudio中我们有一个非常简单的项目，只包含一个源文件`math.cpp`，其中有两个函数`Log()`和`Multiply()`，而`Multiply()`实际上调用了`Log()`函数，打印`Multiply`单词到控制台，最后返回`a*b`：

```c++
#include <iostream>

void Log(const char* message){
  std::cout << message << std::endl;
}

int Multiply(int a,int b){
  Log("Multiply");
  return a * b;
}
```



非常简单，但这并不是一个实际的应用程序，因为它没有包含主函数`main`。你首先要意识到的是编译有两个阶段：编译、链接，实际上有有一种方法可以在VisualStudio区分这两个阶段：按`ctrl`+`F7`或者只按下编译按钮，只有编译才会发生，链接将永远不会发生。但是如果你`Build`你的项目或者点击`F5`运行你的项目，它会编译，然后链接。

所以我们首先`ctrl`+`F7`编译，一切正常，因为编译生成了`.obj`目标文件：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210315165922851.png)

但是如果我右键单击我的项目并点击`Build`，你会看到我实际上得到了一个链接错误：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210315165958099.png)

入口点必须再次定义。很显然我们错过了入口点`main`函数，通过编译和链接，我们实际上得到了不同类型的错误，与每个阶段相关联的信息。如果我犯了语法错误比如`return a * b`没有加分号`;`编译代码会得到如下报错：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210315170056840.png)

它告诉我我实际上得到一个叫`C2143`的错误，当然这是语法错误，你会注意到实际上它以字母`C`开头，这告诉我们是编译阶段。

如果我们修复该错误然后构建整个项目，我们会看到这里列出的错误代码以单词`LNK`开头，它代表链接并告诉我们错误发生在链接阶段。在这种情况下它告诉我们入口点必须被重新定义，这是因为我们将其编译为一个应用程序，如果我们到项目属性看到配置类型为`.exe`：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210315183139138.png)

每个`.exe`文件必须有某种入口点，如果我们到链接器设置找到高级设置，我们可以指定一个自定义的入口点。入口点不一定是`main`函数，它可以是任何东西，只要有一个入口点就行了，但通常它是`main`函数：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210315183220903.png)

我们回到这里把`main`函数写出来：

```diff
#include <iostream>

void Log(const char* message){
  std::cout << message << std::endl;
}

int Multiply(int a,int b){
  Log("Multiply");
  return a * b;
}

+int main(){

+}
```



再次构建项目我们不再得到那个链接错误，并且成功地生成了`.exe`文件。现在我们把`Multiply()`函数打印出来：

```diff
#include <iostream>

void Log(const char* message){
  std::cout << message << std::endl;
}

int Multiply(int a,int b){
  Log("Multiply");
  return a * b;
}

int main(){
+  std::cout << Multiply(5,8) << endl;
+  std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210315183116700.png)



好了，现在假设这个`Log`实际上并不需要在这个`math.cpp`文件内，用一个单独的文件包含我所有的日志相关函数：

```c++
#include <iostream>

void Log(const char* message){
  std::cout << message << std::endl;
}
```



回到`main.cpp`对这个函数进行声明：

```c++
#include <iostream>

void Log(const char* message);

int Multiply(int a,int b){
  Log("Multiply");
  return a * b;
}

int main(){
  std::cout << Multiply(5,8) << endl;
  std::cin.get();
}
```



##### 未解决的外部符号

让我们来看看一种链接错误类型，我们可能会遇到未解决的外部符号（unresolved external symbol），一般是当链接器找不到它需要的东西时发生。比如现在我将`Log.cpp`的函数名更改为`Logr`：

```diff
#include <iostream>

-void Log(const char* message){
+void Logr(const char* message){
  std::cout << message << std::endl;
}
```



重新编译`math.cpp`，编译成功，因为这个环节不包含链接，而编译器认为在某个地方存在这样一个`Log`函数，这是链接的工作。所以当我们构建整个项目得到一个以`LNK`为首的错误，表示未解决的外部符号。幸运的是它告诉我们我们在哪里引用了它，这里是在`Multiply`函数中，所以如果我们在该函数中不调用`Log()`则没有错误。发生这种情况的原因是我从来没有调用过`Log`函数，所以链接器不需要去链接这个`Log`函数。

```c++
#include <iostream>

void Log(const char* message);

int Multiply(int a,int b){
  //Log("Multiply");
  return a * b;
}

int main(){
  std::cout << Multiply(5,8) << endl;
  std::cin.get();
}
```



另一个比较有趣的一点是如果我注销掉`Multiply`函数，也就不会调用`Log`函数。现在构建项目仍会出现链接报错：

```c++
#include <iostream>

void Log(const char* message);

int Multiply(int a,int b){
  Log("Multiply");
  return a * b;
}

int main(){
  //std::cout << Multiply(5,8) << endl;
  std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210315202859380.png)







为什么会这样呢？我们没有在任何地方调用`Multiply`函数，为什么它会抱怨链接错误？我们可不可以说这些没用的死代码一点意义都没有呢？大错特错，因为在这个文件这里我们虽然用不到`Multiply`函数，但从技术上讲我们在另一个文件中可能会使用它，所以链接器缺失需要链接它。如果我们能告诉编译器这个`Multiply`函数我只会在这个文件中使用它，那么我们可以去掉这个链接必要性，因为`Multiply`从未被调用，也就是不需要调用`Log`函数。

有一个方法我们可以做到，如果我们在`Multiply`之前写下`static`静态这个词，意味着这个函数只被声明在这个翻译单元中，也就是我们的`math.cpp`文件：

```c++
#include <iostream>

void Log(const char* message);

static int Multiply(int a,int b){
  Log("Multiply");
  return a * b;
}

int main(){
  //std::cout << Multiply(5,8) << endl;
  std::cin.get();
}
```



在本例中，我们实际上修改了函数的名字，然而这不仅仅是函数的名字很重要，如果我把函数名字改回来但返回类型改为`int`，然后返回0或者类似的值：

```c++
#include <iostream>

int Log(const char* message){
  std::cout << message << std::endl;
  return 0;
}
```

构建项目我得到一个错误，因为我们在`math.cpp`中声明`Log()`是一个返回值为`void`的函数。正因如此我们需要找到一个名为`Log`并返回`void`的函数，修改返回类型恢复正常。同样的如果我们更改参数例如增加一个`level`，构建项目依然会得到一个链接错误，因为它期望的`Log`函数没有另一个参数。

```c++
#include <iostream>

void Log(const char* message,int level){
  std::cout << message << std::endl;
}
```



就是这样，如果它找不到确切的函数定义你会得到一个链接错误。





##### 重复符号

另一种常见的链接错误是我们有重复的符号，换句话说我们有函数或变量有着相同的名字或声明。如果发生两个名字相同的函数有相同的返回值和相同的参数，我们就有麻烦了。我们陷入困境的原因是因为链接不知道该链接到哪一个函数，它是模棱两可的。

回到我们的代码，编写`Log()`函数的另一个版本：

```c++
#include <iostream>

void Log(const char* message){
  std::cout << message << std::endl;
}

void Log(const char* message){
  std::cout << message << std::endl;
}
```





我们会得到一个编译错误，这个函数已有主体，这个代码是无效的。编译器可以直接帮助我们解决这些问题，因为这一切都发生在一个文件中，发生错误的时候还没开始链接。但是如果我把它移到一个不同的地方例如`main.cpp`：

```c++
#include <iostream>

void Log(const char* message);

void Log(const char* message){
  std::cout << message << std::endl;
}

static int Multiply(int a,int b){
  Log("Multiply");
  return a * b;
}

int main(){
  std::cout << Multiply(5,8) << endl;
  std::cin.get();
}
```



在`math.cpp`中我们只有一个`Log`的定义，所以它不会给我们一个编译错误。但如果构建项目我们会得到一个链接错误，它告诉我们已经有了这个`Log`函数定义在`Log.obj`文件中。在这种情况下链接不知道`Log`函数链接到哪一个，是链接`math.cpp`里面的呢还是`Log.cpp`里面的呢，链接器它不知道。

你可能认为这种类型的错误不是经常会发生的事情，你会做的聪明些。然而这很可能会悄悄发生在你身上，下面来展示几种情况。首先去掉`math.cpp`中重复定义的`Log()`函数，成功构建项目。现在让我们创建一个名为`Log.h`的头文件，将之前`Log.cpp`的定义剪切过来：

```c++
#pragma once

void Log(const char* message){
  std::cout << message << std::endl;
}
```

返回`Log.cpp`定义一个`InitLog`函数调用`Log`函数：

```c++
#include <iostream>
#include "Log.h"

void InitLog(){
  Log("Initialized Log");
}
```



再次构建项目我们得到一个或多个符号被多重定义的错误：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210315203054134.png)

这个重复符号的错误信息很奇怪，事实上我只有一个`Log`函数的定义，它为什么会说多重符号呢？这就回到了`include`语句的工作原理，当我们包含头文件时我们取头文件的内容，把它放在`include`语句的地方。所以实际发生的是因为`#include "Log.h"`这个`Log`函数被定义在`math.cpp`和`Log.cpp`中，这样我们有了2个相同的函数定义。

那么我们该如何解决这个问题呢？我们有几个选择，如果我们撤销刚才的复制操作我们可以将这个`Log`函数标记为静态，这意味着在链接到`Log`函数时`Log`函数只能是内部函数，也就是说`Log.cpp`和`math.cpp`文件中的`Log`函数只能是文件的内部函数，就像`Multiply`函数一样。所以`Log.cpp`和`math.cpp`都会有自己的`Log`函数，它对任何其他的`.obj`文件都不可见：

```c++
#pragma once

static void Log(const char* message){
  std::cout << message << std::endl;
}
```



如果我们编译这个文件，我们不会得到任何报错：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210315202959948.png)





还有另外一个办法是`inline`：

```c++
#pragma once

inline void Log(const char* message){
  std::cout << message << std::endl;
}
```

`inline`的意思是获取我们实际的函数体并将函数调用替换为函数体，在这种情况下`InitLog`函数变成了这样：

```c++
#include <iostream>
#include "Log.h"

void InitLog(){
  std::cout << "Initialized Log" << std::endl;
}
```

如果我们构建项目，依然没有错误。



还有另一种方法可以解决这个问题，在这种情况下我会把它的定义转移到一个翻译单元。因为现在的情况是这个`Log`函数的定义列入了两个翻译单元（`Log.cpp`和`math.cpp`），这是导致错误的首要原因。我们可以把它搬到第三个翻译单元或者把`Log`的定义放进现有的这些翻译单元。由于`Log.cpp`与该功能有关，所以我们把定义放入`Log.cpp`：

```c++
#include <iostream>
#include "Log.h"

void Log(const char* message){
  std::cout << message << std::endl;
}s

void InitLog(){
  Log("Initialized Log");
}
```



而`Log.h`仅仅保留函数的声明即可：

```c++
#pragma once

void Log(const char* message);
```



现在`Log`函数的链接被放进了`Log.cpp`中，在我们项目的一个翻译单元中，然后`main`函数会调用到它。构建项目，我们没有链接错误，我们的项目能够成功链接：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210315202938517.png)

记住，在工作结束的时候链接器需要带走我们所有的目标文件并将它们链接到一起，它也链接我们可能用到的任何其他库，例如C运行时的库、C++的标准库、平台的API等等......从不同的地方链接是很常见的。还有不同类型的链接，我们有静态链接和动态链接，在以后的部分会提到。

