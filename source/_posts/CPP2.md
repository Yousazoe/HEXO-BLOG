---
title: C++语法基础
comment: false
tags: Cpp
categories: Cherno的C++笔记 (Cherno C++)
abbrlink: b6350aab
date: 2021-03-22 15:59:50
type:
banner_img:
index_img:
translate_title:
top:
mathjax: ture
---





![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/749d2b61408483.5a6df91d1ecfa.jpg)

<div align=center>
  <font size="3">
    <i>
      <a href="https://www.behance.net/gallery/61408483/Memories">Memories</a> by 
      <a href="https://www.behance.net/MChahin">Mohamed Chahin</a>
    </i>
  </font>
</div>





### 引言

这个系列将讲解C++需知道的一切内容，涵盖这门语言的基础知识。本节将开始讲解C++的语法内容。

<!--more-->





### 变量

今天我们来讨论一下C++中的变量。一个C++程序中我们希望使用数据，而编程的大部分内容实际上都是在使用数据，我们操作任何类型的数据；我们在程序中使用任何数据，包括我们想要改变的、我们想修改的、我们想要读和写的......我们需要把这个数据存储进这个叫“变量”的东西。

变量允许我们命名我们存储在内存中的数据继续使用它。举个例子，假设你正在制作一款游戏，你有一个球员，在你的游戏中球员角色在地图有一个位置而角色可以移动，我们需要你能够存储球员的位置，位置在我们的内存中是一个变量。当需要把球员放在屏幕上或与关卡的其他部分互动时我们才能看到球员到底在哪里，我们想要用一个变量存储球员位置。

无论什么编程语言，变量是所有程序中最基本的。我们需要能够利用数据将数据存储在某个地方，当我们创建一个变量时，它被存储在内存中（具体是两个地方：堆和栈）。在之后的章节会介绍内存的深度解释，不过现在我们只要知道变量确实会占用内存，那是我们实际存储数据的地方。

在C++中我们有许多定义好的数据类型，这些基本的数据类型构成了我们在程序中存储的任何数据。每种数据类型都有特定的用途，虽然它有特定的用途，实际上你也不一定就是用于这个目的。C++是一种非常强大的语言，这意味着实际上对我们有很少的约束，当我解释变量时，我喜欢这么说：**不同变量类型之间唯一的区别在C++中是大小**，也就是这个变量会占用多少内存。

#### 整数

来看一个例子，在`main()`前我们已经有了一个变量类型`int`，它让我们在特定条件下存储一个整数：

```c++
#include <iostream>

int main(){
  std::cout << "Hello World!" << std::endl;
  std::cin.get();
}
```



如果我们想声明一个全新的变量，我们可以输入这个变量的类型，给它起个名字例如`variable`，然后给它起一个值，最后一部分是可选的，你不需要马上给它赋值，但现在我们把它的值设为8：

```c++
int variable = 8;//-2b -> 2b
```



整数是传统上为4个字节的数据类型，数据类型的实际大小取决于编译器，不同的编译器会有不同的大小，由编译器确定类型的大小。`int`数据类型的意思是在一定范围内存储整数，因为它是4个字节大小。所以存储的数字被限制在一定范围内，具体来说这是一个有符号的数字，存储的值从负20亿到20亿，任何在这个范围之外的数字都需要比`int`类型更大的数据类型来存储。

改变一下源码，将这个`variable`变量打印到控制台：

```c++
#include <iostream>

int main(){
	int variable = 8;
	std::cout << variable << std::endl;
	std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210322182208177.png)

我们可以继续修改变量，例如将它重新分配到20这样的值，让我们再打印一次看看会发生什么：

```c++
#include <iostream>

int main(){
	int variable = 8;
	std::cout << variable << std::endl;
	variable = 20;
	std::cout << variable << std::endl;
	std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210322182447422.png)



就像我说的，`int`数据类型可以存储介于负20亿到正20亿的值（准确的说是20亿多一点）。所以你可能会说为什么是负20亿到正20亿，这些限制从何而来？它们有意义吗？

答案是肯定的，它们是有意义的。变量的类型大小与它能存储多大的数字直接相关，一个整数是4个字节，那么我们可以在这4个字节的数据范围存储值。让我们分析一下，一个字节是8比特的数据，那么4字节是32位的数据。因为这个变量有符号，这意味着它可以是负的，包含一个像负号一样的符号，因此这32位中的一个表示符号，这样我们就是知道它是正的还是负的。实际数字只剩下31位，一个比特可以是0或1，那么现在我们有31个比特，每个比特有两个可能的值，$2^{31}$是多少？掏出内置的计算器算一算：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210322184347943.png)

我们得到大约21亿，而这就是我们得到的整数存储的最大值，最小值加上负号即可。但我听见你说你不想要负值，有没有什么方法把这个符号位去掉，然后把它作为我数字的一部分？

是的，有的，这就是我们所说的无符号数，这意味着它是一个没有符号的数并且它总是正值。在C++中我们可以在`int`前面输入`unsigned`：

```c++
#include <iostream>

int main(){
	unsigned int variable = 8;
	std::cout << variable << std::endl;
	variable = 20;
	std::cout << variable << std::endl;
	std::cin.get();
}
```



现在我们有32位比特，也就是$2^{32}$：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210322184933999.png)

这就是`unsigned`关键字在C++中的作用，它让我们定义了一个没有符号位的数据类型。

我们还有什么其他数据类型可用呢？如果我不想要四个字节的整数呢？还有其他类型吗？

我们实际上有不少。我们有`char`，它是1字节的数据；我们有`short`，它是2字节的数据；我们有`int`，4个字节的数据；我们有`long`，这通常也是4字节的数据，具体取决于编译器；然后是`long long`，通常是8字节的数据。还有其他类型，比如`long int`等等，但最基础的是这五个，我们也可以将`unsigned`添加到其中任意一个，它会移除符号位可以让你设置一个更大的数字。

`char`通常用于存储字符而不仅仅是数字，除了给它分配数字比如50，你也可以给它分配字符比如`A`:

```c++
char a = 50;
a = 'A';
```



这并不是说你不能给其他整数类型分配字符，例如刚才的字母`A`实际上只是一个与该字符相关联的数值，具体来讲字符`A`是65。如果数字可以是字符，字符也可以是数字，那为什么会有这种区别呢？为什么我说`char`是专门用来代表字符的？其实不是这样，这是因为我们经常当程序员对某些数据类型做出假设时，如果我传入一个`char`，我通常希望你真的分配一个字符：

```c++
#include <iostream>

int main(){
	char a = 'A';
	std::cout << a << std::endl;
	std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210322190436231.png)



如果我用数字65代替字符`A`，再次打印我们还是会把`A`打印出来：

```c++
#include <iostream>

int main(){
    char a = 65;
    std::cout << a << std::endl;
    std::cin.get();
}
```



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210322190629657.png)



传入一个`char`到`cout`，`cout`会把65（`A`）看作一个字符而不是一个数字。如果我把它变成其他类型例如`short`，`cout`不再把它当作一个字符，它会打印出数值：

```c++
#include <iostream>

int main(){
    short a = 65;
    std::cout << a << std::endl;
    std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210322191003894.png)



即使我在这里赋值的是一个字符，它也只是把值赋值给65：

```c++
#include <iostream>

int main(){
    short a = 'A';
    std::cout << a << std::endl;
    std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210322195402236.png)



通过上面这几个例子想必可以更深入的理解数据类型。数据类型的使用取决于程序员，我们有一些既定的约定，但是没有什么具体的东西需要你去遵循，C++中没有太多的规则限制你，正因如此我希望你们能意识到，这是这些数据类型之间唯一的区别：创建变量时通过数据类型将分配不同的内存。



#### 浮点数

有了这些整数类型，如果我想存储一个含小数点的值例如5.5，我该怎么做呢？我们有两种数据类型：`float`和`double`，也可以在此基础上进行修改：`long double`。

`float`基本上是一个小数，占用4字节数据的存储。我们在这里定义一个变量，例如5.5，我们怎么做呢？我们把变量`a`替换成浮点变量：

```c++
#include <iostream>

int main(){
	float variable = 5.5;
	
	std::cout << variable << std::endl;
	std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210322201316973.png)



现在你可能认为你已经定义了一个`float`数，但你实际上你没有，你实际上定义了一个双精度`double`。

我们有两个变量可以用来存储小数`float`和`double`，那么我们如何区分哪些是`double`，哪些是`float`，区别的方式是在数字的后面追加`f`/`F`，并且浮点数基本上是4字节大，双精度数是8个字节。：

```c++
#include <iostream>

int main(){
	float variable = 5.5f;
  double var = 5.2;
	
	std::cout << variable << std::endl;
	std::cin.get();
}
```



#### 布尔值

最后我们还有一种更原始的数据类型，那就是`bool`。它的意思是`boolean`，代表`true`或`false`，如果我们尝试打印到控制台，你会得到1：

```c++
#include <iostream>

int main(){
    bool variable = true;

    std::cout << variable << std::endl;
    std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210322204607838.png)



为啥？很显然计算机不懂什么真假，只知道0和1这些数字。所以基本上0意味着`false`，除了0之外任何数字，都是`true`。在这个例子中，我们会打印1到控制台表明它是`true`的，如果我们改变成`false`并运行程序，我们会得到0：

```c++
#include <iostream>

int main(){
    bool variable = false;

    std::cout << variable << std::endl;
    std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210322205000741.png)



`bool`数据类型占用一个字节的内存。现在你可能会问了，为什么是一个比特？`bool`不是`ture`就是`false`，当然这只需要一比特来表示就行了。然而当我们处理寻址内存时我们需要从内存中找到我们`bool`变量的值，我们没有办法去寻址只有一个比特位的内容，因此我们不能创建只有一个比特的变量，我们需要能访问它。







好了，我们说了那么多的`size`大小和`bytes`大小以及每个类型多大，占据多少内存，我们如何知道一个数据究竟多大？毕竟它依赖于编译器，有什么地方可以查一下吗？是的，我们有个操作符，在C++中调用`sizeof`操作符：

```c++
#include <iostream>

int main(){
    bool variable = false;

    std::cout << sizeof(bool) << std::endl;
    std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210324163711382.png)





这就是变量所需要讲的东西了，已经涵盖了所有的基本数据类型，你也可以实际创建许多不同的类型，有些C++已经为你创建了。自定义类型都是基于这些基本的类型创建的，在这些基本类型的基础上我们可以创建任何类型并存储我们的任何数据。现在有了这些原始数据类型，我们还可以将它们转换为指针或引用，其中指针可以通过写一个`*`来声明，引用则是一个`&`。指针和引用是如此庞大和复杂，在之后的章节我们会详细解释。

变量是几乎所有东西的基础，它们真的很重要，请务必保证自己能够理解和掌握。





### 函数

今天我们来讨论C++中的函数，那么函数到底是什么呢？函数就是我们写的被设计用来执行特定任务的代码块，之后我们学习`class`类的时候这些块称为方法。但是当我说到函数时，我明确地说的是不属于C++类里面的东西，对我们来说使用函数避免代码重复是很常见的，我们不想写重复相同的代码，当然我们也可以复制和粘贴很多代码，但那会带来巨大混乱与不确定，这也意味着如果我们决定改变一些代码，我们必须在所有这些地方改变它，维护这些代码简直是灾难。

所以我们把我们要做的事情写成一个函数，然后如果我们需要我们可以多次调用它。我们可以为函数提供一定的参数，函数可以为我们返回值。假设我们想写一个把两个数相乘的函数，首先是写出这个函数所谓的返回类型`int`，然后给函数命名为`Mutiply`，它有两个参数`a`、`b`：

```c++
#include <iostream>

int Multiply(int a,int b){
  return a * b;
}

int main(){
	std::cout << "Hello World!" << std::endl;
	std::cin.get();
}
```



函数的参数不是必要的，我们也可以变为这样：

```c++
int Multiply(){
  return 5 * 8;
}
```



我们也可以通过`void`作为返回类型，让函数不返回任何东西：

```c++
void Multiply(){
  std::cout << 5 * 8 << std::endl;
}
```



回到最初的例子，我们该如何调用函数呢？在本例中我用一个`result`变量保存`a*b`乘法结果：

```c++
#include <iostream>

int Multiply(int a,int b){
  return a * b;
}

int main(){
  int result = Multiply(3,2);
  
	std::cout << "Hello World!" << std::endl;
	std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210324175123514.png)







让我们把情况说的更详细些，假设我要做一堆的乘法并把它们都记录到控制台，在没有函数的情况下会看起来很乱：

```c++
#include <iostream>

int Multiply(int a,int b){
    return a * b;
}

int main(){
    int result1 = Multiply(3,2);
    std::cout << result1 << std::endl;

    int result2 = Multiply(8,5);
    std::cout << result2 << std::endl;

    int result3 = Multiply(90,45);
    std::cout << result3 << std::endl;
    std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210324175948419.png)



所以我们尝试写一个包含打印与乘法功能的函数`MultiplyAndLog`：

```c++
void MultiplyAndLog(int a,int b){
    int result = Multiply(a,b);
    std::cout << result << std::endl;
}
```



调用时就不用写许多重复的部分，得到的效果是一样的，最后我们会得到漂亮干净并且易读的代码：

```c++
#include <iostream>

int Multiply(int a,int b){
    return a * b;
}

void MultiplyAndLog(int a,int b){
    int result = Multiply(a,b);
    std::cout << result << std::endl;
}

int main(){
    MultiplyAndLog(3,2);
    MultiplyAndLog(8,5);
    MultiplyAndLog(90,45);
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-03-25%20%E4%B8%8A%E5%8D%8810.41.54.png)



这是一个很简单的例子，但我认为它很有效的证明了函数是非常重要的，你的目标应该是讲你的代码分为很多函数。然而有一件事我想强调，也不要把你的代码每一行都拆成函数，那是对任何人都没好处的代码：它很难维护并且看起来凌乱不堪，它会让你的程序变慢。

每次我们调用函数时，编译器生成一个`call`指令，这意味着在一个运行程序中为了调用一个函数我们需要创建一个堆栈结构，这意味着我们必须把像参数这样的定西推进堆栈。我们还需要将一个叫做返回地址的东西压入堆栈，然后我们要做的是跳到二进制文件的不同部分，以便开始执行我们的函数指令。为了将`push`进去的结果返回，我们得回到最初调用函数之前，就像在内存中跳跃来执行函数，跳跃和执行这些都需要时间，所以它会减慢我们的程序。我说这个的原因是因为这些都是编译器假设的决定我们的函数作为一个实际的函数而不是内联`inline`，在未来的章节我们会深入讨论内联。

函数的主要目的是防止代码重复，我们不希望到处复制粘贴代码。回到我们的代码，`main`函数的返回类型是`int`，但我们并没有任何返回的数据。事实上只有主函数可以豁免，其他指定了返回类型的函数必须要返回值，它会自动假设你返回0：

```c++
#include <iostream>

int Multiply(int a,int b){
    return a * b;
}

void MultiplyAndLog(int a,int b){
    int result = Multiply(a,b);
    std::cout << result << std::endl;
}

int main(){
    MultiplyAndLog(3,2);
    MultiplyAndLog(8,5);
    MultiplyAndLog(90,45);
  
    return 0;
}
```







### 头文件

头文件是什么？我们为什么需要它们？为什么它们存在于C++中？你可能学过很多其他语言比如Java或C#，它们实际上并没有头文件，我们有两种不同文件类型的概念，一种就是像C++一样编译的翻译单元，这种就会有头文件概念。

头文件是一种很奇怪的文件，我们总是把它包含在某些地方，为什么要这样呢？它们的用途远不止只是声明一些你想要的声明然后在C++文件中使用。就C++的基础而言，头文件通常用于声明某些类型的函数以便它们能够被使用在你的程序中，如果你回想一下C++编译器和链接器部分，我讲了我们需要某些声明存在以便我们知道我们的功能和类型可供我们使用。例如如果我们在一个文件中创建函数，我们想在另一个文件中使用它，当我们尝试编译另一个文件的时候C++不会知道这个函数存在，所以我们需要一个公共的地方来存放东西，只是声明，没有定义（因为我们只能定义函数一次）。我们需要一个公共的地方来存储函数声明，没有实际的定义或函数体，只是一个地方说这个函数是存在的。



#### include

让我们举一个简单的例子，假设这里有一个叫做`log`的函数接收一个`const char* message`参数然后输出：

```c++
#include <iostream>

void Log(const char* message){
    std::cout << message << std::endl;
}

int main(){
    std::cout << "Hello World!" << std::endl;
    std::cin.get();
}
```



新建一个`Log.cpp`，创建一个`InitLog`函数，里面调用`Log`函数：

```c++
void InitLog(){
    Log("Initializing Log");
}
```



我们会得到一个错误，因为`Log`函数在此文件中并不存在，这个文件不知道`Log`函数是什么东西。`Log.cpp`到底需要什么才能不出错？我们怎么知道`Log`函数是确实存在的，它只是在别处定义呢？也就是说，需要函数声明。

回到代码，我只需要声明`Log`确实存在：

```c++
void Log(const char* message);

void InitLog(){
    Log("Initializing Log");
}
```



这个函数实际上没有实体表示它是函数的声明，我们还没有定义这个函数。我们只是说，有个函数叫`Log`返回`void`并接受一个`const char*`指针，这个函数确实存在。修改之后可以看到错误已经消失了：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202021-03-25%20%E4%B8%8B%E5%8D%8812.32.12.png)



我们找到了一种方法可以告诉`Log.cpp`这个函数存在，但如果我们创建另一个文件呢？其他的文件也需要用到`Log`函数吗？这是否意味着我还需要复制和粘贴把这个`void Log()`函数声明粘贴到其他地方？

答案是肯定的，你确实需要这样做，但是有一种更简单的方法：头文件。什么是头文件？我应该怎样看待头文件？头文件通常会被包含在CPP文件中，我们做的就是复制粘贴将头文件的内容放入CPP文件，通过`#include`预处理器指令来实现复制粘贴把文件放入另一个文件。

回到项目新建一个头文件`Log.h`，在该文件中放置我的`Log()`函数的声明：

```c++
void Log(const char* message);
```



这个头文件`Log.h`可以包含在任何我希望使用`Log()`函数的地方。对我们来说，我不想自己手动地复制并粘贴到每一个需要它的文件，所以我找到了这一种看起来整洁和自动化的方法。

回到`Log.cpp`，可以看到我们得到一个因没有声明函数导致的错误：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210401205838241.png)



但如果加入之前包含函数声明的头文件`Log.h`，报错消失并且文件可以编译：

```diff
+ #include "Log.h"

void InitLog(){
    Log("Initializing Log");
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210401210048322.png)



回到`main.cpp`，如果我们想调用`InitLog()`，那么就在`Log.h`中添加`InitLog()`函数的声明，再在`main.cpp`中调用`Log.h`头文件即可：

```diff
#include <iostream>
+#include "Log.h"

void Log(const char* message){
    std::cout << message << std::endl;
}

int main(){
+   InitLog();
    Log("Hello World!");
    std::cin.get();
}
```



回到`Log.h`添加函数`InitLog()`的声明：

```diff
#pragma once

void Log(const char* message);
+void InitLog();
```



现在运行我们的程序，可以看到我们初始化了Log，然后将Hello World输出到控制台。

![](https://tva1.sinaimg.cn/large/008i3skNgy1gqd8ubks8xj310q0h83zg.jpg)



#### pragma

好的，让我们回到头文件看看那个`#pragma`声明到底是什么。它看上去是为我们自动插入的，首先任何以`#`开头的东西被称为预处理器命令或预处理器指令，这意味着它在实际编译此文件之前被处理。

`pragma`本质上是一个被发送到编译器或预处理器的预处理指令，它想要只包括这个文件一次。`#pragma once`监督着这个头文件，组织我们单个头文件多次被包含并转换为单个翻译单元。现在我非常谨慎地选择我的措辞，因为你要明白这并不妨碍我们将头文件放在程序的多个位置，而只是说放在一个翻译单元，一个CPP文件。

原因是如果我们不小心多次包含了一个文件并转换成一个翻译单元，我们会得到duplicate复制错误，因为我们会复制粘贴整个头文件多次，演示这一点最好方法是我们创建一个结构体。例如我在`Log.h`创建了一个名为`player`的结构体，我可以让它空着，这不重要。

```diff
-#pragma once

void Log(const char* message);
void InitLog();

+struct player {};
```



如果我将这个文件包含两次并转换成一个翻译单元，放弃这个`#pragma once`监督，它实际上会包含该文件两次，这意味着我将有两个相同名字的`player`结构体。回到`Log.cpp`包含`Log.h`两次：

```diff
#include <iostream>
+#include "Log.h"
+#include "Log.h"

void Log(const char* message){
    std::cout << message << std::endl;
}

int main(){
    InitLog();
    std::cout << "Hello World!" << std::endl;
    std::cin.get();
}
```



此时如果尝试编译文件，它会说我们重新定义了`player`结构体，结构体名字必须是唯一的，我们只能定义一个名为`player`的结构体：

![](https://tva1.sinaimg.cn/large/008i3skNgy1gqdemrpq1dj310o0h9jua.jpg)





也许有人会说自己不是一个愚蠢的程序员，我不像你想的那么笨，为什么我要包含一个文件两次？好吧，年轻人，现在回到`include`是如何工作的，记住`include`的工作原理是复制和粘贴文件到其他文件，这意味着你可以创建一链条的头文件。所以我们有一个名叫`Log.h`的头文件，里面有`player`结构体、`log`函数等等，而这些东西也被包含进了其他头文件，然后第三个头文件包含了所有，如果我们创建另一个头文件`common.h`包含其他的头文件：

```c++
#pragma once

#include "Log.h"
```



​	回到`Log.cpp`将其中一个`Log.h`改为`common.h`，编译文件：

![](https://tva1.sinaimg.cn/large/008i3skNgy1gqdf241q7aj310n0h9dj6.jpg)



我们仍然得到那个错误，因为`player`结构体被重新定义了。如果我们想知道预处理器到底做了什么，你可以看到它实际上包含了两次`log`，而如果我们在`Log.h`重新加入`#pragma once`编译：

![](https://tva1.sinaimg.cn/large/008i3skNgy1gqdf68zcnlj311y0lc77u.jpg)



我们不会得到错误，因为它识别了那个`log.h`已经被包含，没有必要包含两次。





#### ifdef

还有另一种方法来做头文件的监督，虽然`pragma`看起来更简洁，但它比`pragma`更有意义，它就是`ifndef`。

首先，在`Log.h`中输入`#ifndef`，然后输入需要检查的符号比如`_Log_H`，然后我们`#define _LOG_H`，在文件的最后我们输入`#endif`：

```diff
-#pragma once
+#ifdef _LOG_H
+#define _LOG_H

void Log(const char* message);
void InitLog();

struct player {};

+#endif
```



这里的过程是首先检查是否有一个叫做`_Log_H`的符号被定义：如果它没有被定义，将继续在编译中包含下面的代码；如果这个被定义了，那么所有这些都不会被包含进来。一旦我们通过这个初始检查，我们定义`_Log_H`，也就是说下次我们再用到这些代码的时候它将被定义，因此不会重复。



#### header file

最后我想展示的是头文件在`include`语句中的差异，有些`include`语句使用引号，有些`include`语句使用尖括号，到底是怎么回事？

```c++
#include <iostream>
#include "Log.h"
```

​	

其实很简单，当我们编译程序时，它们有两种不同的含义。我们有能力告诉编译器包含文件的路径是什么，如果我们要包含的文件是在其中一个文件夹里，我们可以使用尖括号来告诉编译器搜索包含路径文件夹；而引号则通常用于包含相对于当前文件的文件。

例如，我有一个名为`log.h`的文件，它如果在`log.cpp`文件所在目录的上层目录下，我可以使用`../`返回当前文件的上级目录，而`iostream`只需在其中一个包含目录里面就行了。我们将在未来讨论更多关于设置包含目录，我不想把事情复杂化，但这就是头文件工作的基本要点。



最后一件事是这个`iostream`实际上看起来不像一个文件，因为它不包含任何扩展只叫做`iostream`，这是怎么回事？它实际上是一个文件，只是它没有扩展名，这是写C++标准库的家伙决定要这么做的，这样可以将C++标准库与C标准库进行划分，C标准库通常会有`.h`拓展但C++文件没有，这是一种区分C标准库和C++标准库的方法。

```c++
#include <stdlib.h>
#include <iostream>
```





### 调试

今天我们来学习如何调试代码。调试是非常重要的，它是编程的一部分，如果你知道如何调试你的代码，你会明白这个程序是如何工作的，计算机是如何实际运行你的代码。我们会用中断来将东西分成两部分，断点是调试和在内存中查找的重要部分。断点和读取内存是调试的两大部分，当然你会同时使用它们，换句话说，你要设置断点就是为了读取内存。

那么调试的意义是什么呢？debug的意思是de bug，从代码中清除错误。要从我们的代码中删除一个bug，我们必须诊断出我们的代码错在哪儿，这部分实际上是很棘手的即使你在这门语言上很有经验。最终你要记住，电脑永远是对的，极少情况才会是你做了正确的事情但电脑却工作不了，通常情况是你烦了错误而不是计算机，意识到这点非常重要，所以这一切都是为了找出你的错误。

我们使用上一节的项目工程，主函数`main`对`Log`函数进行调用：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210511093316644.png)

```c++
#include <iostream>
#include "Log.h"


int main(){
    Log("Hello World");
    std::cin.get();
}
```



`Log.cpp`包含`Log()`函数的具体实现：

```c++
#include <iostream>
#include "Log.h"

void Log(const char* message){
    std::cout << message << std::endl;
}
```



而`Log.h`则是对`Log()`函数声明：

```c++
#pragma once

void Log(const char* message);
```



我们首先要做的是设置一个断点，然后逐步执行我们的程序。那么什么是断点呢？断点是程序中调试器将中断的点，这里break的意思是暂停。我们可以在程序中的任何代码行上设置断点，当程序执行到这里时它将暂停。

在我们这个例子的整个项目中，它会挂起执行线程，让我们来看看这个程序的state（状态），这里指的是内存，我们可以暂停我们的程序看看在它内存中发生了什么。记住，一个运行中的程序所需的内存是相当大的，包括你设置的每个变量、要调用的函数等等，当你将程序中断后，内存数据实际上还在，查看内存对诊断程序问题非常有帮助。通过查看内存，你可以看到每一个变量的值，这个变量不应该设置为这个值。

你还可以单步逐行运行你的代码，我可以放一个断点在第5行代码，然后点击按钮，程序将只前进一行到第6行。你还可以step into（步入）函数内看看函数会运行到哪里，可以用断点做很多事情。

回到我们的项目，VisualStudio直接点击`F9`在当前代码行设置断点，或者你可以点击侧栏的任意地方，这里CLion也是点击侧栏设置断点：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210511220115175.png)



点击debug按键，我们程序的焦点实际上回到CLion上：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210511220515644.png)



这里有一堆按钮，让我们进入（`Step Into`），要么跨过（`Step Over`），要么走出去（`Step Out`）。这三个按钮会控制什么？



#### Step into

`Step Into`的意思是进入到这行代码的函数里（如果这一行有一个函数的话）。在这种情况下，如果我点击`Step Into`，在`Log`这一行我们将步入进`Log`函数，我们可以看到它到底干了什么。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210511220830764.png)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210511220906112.png)

#### Step Over

`Step Over`就是从当前函数跳到下一行代码。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210511220739489.png)



#### Step Out

`Step Out`的意思是跳出当前函数，回到调用这个函数的位置。在这个例子中，回到`main`函数的调用位置，也就是C++标准库函数的位置。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210511221006379.png)



让我们来`step into`来看看`Log`函数。在stack栈的最开始，我们没有执行任何代码，可以将鼠标悬停在这个`message`变量上，它告诉我们它被设置为`Hello World`。这是调试的第二个部分，我们现在在读内存：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210512000627711.png)



此时高光表明它还没有实际执行那代码，如果我们现在查看控制台可以看到`Hello World`消息没有被打印出来：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210512001001149.png)



这时我们再继续执行，控制台才会打印消息：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210512001127067.png)



通过在我们的程序中设置断点，我们可以逐行运行整个程序。我们再来做一些变量使事情变得有趣，我将取一个整数`a`设它等于8并让它递增，换句话说`a`被设为9，然后加一个循环：

```diff
#include <iostream>
#include "Log.h"

int main(){
+    int a = 8;
+    a++;
+    const char* string = "Hello";

+    for (int i = 0; i < 5; ++i) {
+        const char c = string[i];
+        std::cout << c << std::endl;
+    }
    
    Log("Hello World");
    std::cin.get();
}
```



此时如果我们不设断点直接运行程序，我们得到了`Hello`和`Hello World`：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210513112006882.png)



好的，现在让我们单执行看看，在`int a = 8`设置断点：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210513112256094.png)



可以看到`a`为7亿多，这里的高光并不意味着我们已经运行了这行代码而是我们正要运行它，所以这行创建并设置`a`变量的值并没有运行。这里显示的是`a`将要被设置的内存位置的数字，因为我们没有设置这个变量，它只是未初始化的内存，这意味着这个值是内存中实际包含的内容。

调试模式会减慢我们的程序，这是因为编译器会让我们的程序做一些额外的事情让我们的调试更轻松。编译器知道我们准备做一个变量，但我们还没有初始化它，所以我们要做的就是把它填满：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210513114832030.png)



我们继续前进运行程序，观察Debugger窗口的变化：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210513115332997.png)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210513115456856.png)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210513115611192.png)



可以看到`a`随着程序的运行递增为9，而循环变量`i`被设为0，它会取出这个`string`字符串中索引0对应的字符，也就是字符串的第一个字符`H`，以此类推。

这就是一个非常简单、基本的调试过程，这里面还有很多其他的东西，但这节展示的内容可以作为我们实际调试代码的基础。记住，一个程序就是由内存组成的，指针、我们实际执行的代码所有这些都存储在内存中，所以能看到我们的内存是最重要的，这是我们所需要的。

通过设置断点，我们可以暂停程序，在给点时间的给定代码行检查我们的变量，这对我们运行代码非常有用。





### 条件与分支

今天我们来看看条件语句，换句话说`if`、`if else`和`else if`等等。那么条件语句、`if`语句、分治语句都是什么意思呢？基本上，我们写程序的时候需要一个特定的条件进行评估，然后根据评估的结果决定我们想要执行什么代码。举个例子，假设我们有一个变量x等于5，我们希望能够编写确定这个变量的值是否确定等于5这样的代码，这就是condition（条件语句）的本质，这里的条件就是x等于5。

在此基础上，我们可以进行适当的分支，当我们运行我们写的`if`语句时有两种情况会发生，先是对实际condition（条件语句）的评估，然后时给予这个条件语句评估后的分支语句。换句话说如果条件为真，我们需要跳到我们源代码的某一部分；如果值为假，我们需要跳到我们源码的另一部分。

当我们开始一个应用程序时，整个应用程序及其所有模块加载到内存中，基本上所有的这些指令组成了我们的程序。当我们有了条件语句所产生的分支，我们基本上是告诉电脑：嘿，跳到我们的这部分内存开始吧，在那里执行我们的指令。

正因为如此，在内存和分支之间跳跃，实际上过程比我说的更复杂一点。这里有相当多的东西值得探索，例如我们必须检查条件，然后跳转到内存的不同地方并从这里开始执行指令，意味着`if`语句和分支通常有比较大的开销。如果你想写快速的代码，你可能要考虑根本不使用`if`语句，事实上许多优化的代码将特别避免分支，避免使用`if`语句，因为这样做会最终使程序慢下来。在这个系列中，我们将看看一些优化的例子，比如删除分支，但现在还为时尚早。

我们来看一个上节课用到的例子：

```c++
#include <iostream>
#include "Log.h"

int main(){
    int x = 5;
    bool comparisonResult = x == 5;


    Log("Hello World");
    std::cin.get();
}
```



我们要检查一下x是不是等于5，为此我们需要执行一个叫做比较的操作，换句话说我们要比较一个值与另外一个值，比较的结果是一个`bool`类型：`true`或`false`。创建一个`comparisonResult`的变量用于存储比较的结果。而`==`则被称为等于（equality）运算符。

```c++
#include <iostream>
#include "Log.h"

int main(){
    int x = 5;
    bool comparisonResult = x == 5;

    if (comparisonResult) {
        Log("Hello World");
    }

    
    std::cin.get();
}
```



我们在第6行设置一个断点来看看会发生什么：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210525211503893.png)



而当`x`换为6时可以看到`comparisonResult`已经变成了`false`，并且下面的`if`语句并没有执行直接跳转到最后，中间代码从未被调用：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210525211646918.png)





如果我们想检验指针是否为空，我们可以把那个指针放到一个`if`语句的条件中，看看它是不是`null`：

```c++
#include <iostream>
#include "Log.h"

int main(){
    const char* ptr = "Hello";
    if (ptr)
        Log("Hello World");
    
    std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210525212937211.png)



运行这段代码，我们可以看到指针实际上是被设置了某值而不是`null`，因此我们可以把它打印到控制台。如果指针等于`null`，它可以是`0`或`nullptr`，代码不会执行：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210525213321128.png)



让我们再加入`else`语句：

```c++
#include <iostream>
#include "Log.h"

int main(){
    const char* ptr = nullptr;
    if (ptr)
        Log("Hello World");
    else
        Log("Ptr is null!");

    std::cin.get();
}
```



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210525213547730.png)



关于条件语句、分支跳转基本上就是这样。编程实际上分成两种，一种是数学编程，另一种是逻辑编程，一部分的编程就像是在做数学运算，实际上大多数快速的代码本质上都是在做数学运算；编程的第二类逻辑编程有些无聊，在未来当我们学会写更好的代码的时候，你会在很多情况下需要用到`if`语句，但我们需要尝试用一些数学计算代替而不是分支语句来处理。







### VisualStudio的最佳设置

今天我们要讲的是建立C++项目的方法，这些对于每一个人来说不一定是最好的设置，然而这是我所使用的。老实说，每一个C++项目/解决方案都会使用这些设置，让我们先来看看吧。

我们创建一个全新的项目和解决方案，点击`File`-`New Project`，把名称命名为`New Project`。关于位置，我喜欢把项目存储在C:/目录中而不是在user文件夹中，这样当我切换电脑或类似的东西时它不会破坏任何部分；项目在某个中央目录下也更容易存储你的开发项目，我喜欢用dev。

一旦我们有了这个新的空项目，你可以看到我们这里完全没有文件或者类似的东西，如果我右键点击该项目，选择在文件资源管理器中打开文件夹（Open Folder in File Explorer），可以看到VisualStudio已经为我们创建了`New Project`项目并且有一个同名的解决方案文件在旁边：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210527110651225.png)



我们有一个专门用于项目的文件夹，里面有`.vcxproj`以及`.vcxproj.filters`文件，其中`.vcxproj`文件是一个XML文件。解决方案看上去是一种奇怪的格式，实际上它是一个文本文件夹就像某种目录。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210527110733791.png)

回到IDE我们注意到这里得到的是一堆不同的文件夹。这些不是文件夹，这些东西叫做过滤器，如果我右键项目点击添加，我们会看到没有new folder而是new filter，如果我添加一个过滤器`cherno`磁盘上什么都不会改变：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210527110607460.png)



这个过滤器文件包含了我们创建的这类虚拟文件夹，这些过滤器组织了你的代码，但是这些目录在磁盘上并不存在，它们确实存在于这个解决方案资源管理器视图。例如我要进入`source files`添加一个新东西（new item），`source files`不是一个文件夹，如果我添加一个`main.cpp`它实际上创建在我的项目文件的旁边：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210527110805200.png)



这有点太乱了，所以我喜欢做的是创建一个名为`Source`或`src`的文件夹，其中包含所有源代码、头文件等等东西，这使得我的项目文件和可能使用的任何其他资源实际上被很好地分开在文件夹中。这是VisualStudio没有为你自动设置的，所以你要自己设置，点击我们的项目的Show All Files展示出来的实际上是硬盘里面的目录结构：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210527110837928.png)

如果我现在右键点击项目，点击Add可以看到过滤器被替换为新文件夹，我可以创建一个名为`src`的文件夹，`alt`+`tab`回到文件管理器我们就有了一个`src`文件夹，在Windows或者VisualStudio中将`main.cpp`文件移到`src`目录：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210527111116130.png)



VisualStudio表现比我期望的更好，这种“显示所有文件”按钮非常好用。回到我们的过滤器，你可以看到`main.cpp`仍然在`source files`中，这只是一种虚拟组织的方案，我可以把它拖到`header files`，它在哪儿并不重要，也可以不放在过滤器中，也就是说它可以在这里。实际上我可以把这些都删掉，这些都不重要，过滤视图就是这样，都是假的：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210527111634077.png)



这些过滤器就是让你把东西分好组就行了，它和磁盘上实际的目录结构没有关系。让我们来快速写一个`Hello World`程序：

```c++
#include <iostream>

int main(){
    std::cout << "Hello World" << std::endl;
}
```



点击`build`，你可以看到所有东西都将构建成功。所以VisualStudio把`.exe`执行文件放在哪里了呢？如果我们看输出，你可以看到这个目录`New Project\Debug`，`.exe`文件在这里，再次打开文件资源管理器可以看到这里有一个`Debug`文件夹，与`.vcxproj`文件在同一个目录：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210527111709321.png)



但是如果我们打开它，我看不到`New Project.exe`文件，这是怎么回事？让我们回到上级目录，再进到这个`Debug`目录，`.exe`文件在这里：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210527111723589.png)



实际上，它把中间文件放进到我们项目目录中的一个名为`debug`的文件夹中，而我们实际的最终可执行二进制文件放入一个名为`Debug`的文件夹中。实际上我还没见过任何专业的开发人员会用这个配置，每个人都会改变它们，因为它们真的很奇怪，对于刚刚起步的人一旦你`build`好了之后，真的很难找到那该死的`.exe`可执行文件。

改变这些并不是什么大问题，你可以创建模板之类的东西。右键点击我们的项目-属性，在活动配置和活动平台下有一个输出目录和一个中间目录，这就是文件的生成目录。首先我要改成所有配置（All Configurations），平台选择All Platforms，现在要做的就是修改这个输出目录，我喜欢写成：

```
$(SolutionDir)\bin\$(Platform)\$(Configurations)\
```



在我们的例子中，把它们放入到解决方案目录下面。最后这部分我们为每个配置放到一个单独的文件夹，对于`debug`模式加一个`debug`的名字后缀；在`release`模式下加一个`release`后缀，这取决于我如何处理我的项目，但在这个例子中我只是把它们放进去，放入一个单独的文件夹。

中间目录将非常相似，我们从输出目录复制所有东西放入中间目录，唯一的区别是加一个`intermediates`文件：

```
$(SolutionDir)\bin\intermediates\$(Platform)\$(Configurations)\
```



ok，现在看起来干净多了。就项目组织而言，设置你的目录非常重要，会让你的生活更轻松。



### 循环

今天我们讨论循环loops。当我说循环的时候，通常指的是`for`循环和`while`循环，简单来说循环是我们写代码需要多次执行同样的操作，因此如果我想打印Hello World 5次，我可以复制粘贴这些代码5次或者可以将这些代码放入一个函数内，然后调用这个函数5次，我们应该这么做吗？或者我们可以使用循环，让代码连续运行5次。

循环在显示图片方面也是非常重要的，可以用来显示游戏。如果你写了一个游戏，你可能想让游戏继续下去；你不想运行游戏，渲染一帧然后退出。其实你是希望游戏保持运行的，要做到这一点，你需要的是游戏循环，意思是说当游戏在运行的时候，只要用户玩家还没有决定退出游戏，就需要对游戏状态更新，渲染游戏，让所有的角色持续保持移动状态，一遍又一遍一帧接一帧持续做所有的事情。

因此，循环对于程序非常重要，它们被用在每一个程序中，就像条件语句一样。



#### for循环

我的例子是之前的打印Hello World，然后打印5次，我们可以通过复制粘贴调用这个`Log`函数5次做到：

```c++
#include <iostream>
#include "Log.h"

int main(){
    
    Log("Hello World");
    Log("Hello World");
    Log("Hello World");
    Log("Hello World");
    Log("Hello World");
    std::cin.get();
}
```



运行代码，你会看到我们把Hello World打印到控制台5次：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210526092345531.png)



然而，为了让我们更加舒服点我们可以写一个`for`循环：

```c++
#include <iostream>
#include "Log.h"

int main(){
    for (int i = 0; i < 5; ++i) {
        Log("Hello World");
    }
    
    std::cin.get();
}
```



循环体就是将要被循环的部分，也就是会被多次执行的代码。当然，这些条件决定了这些代码是否会被执行，有可能循环1次，也有可能循环100次，这都取决于条件。



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210526092636459.png)



当指令指针到`for`这一行时，首先要做的就是申明这个变量`i`，然后接下来看这个条件是否满足：如果条件为真我们会跳到`for`循环里面，执行`for`循环内部的代码，当我们完成了`for`循环体到达大括号时回到`i++`这里，再次查看条件是否为真，这个过程持续到`i`等于4，此时`i++`变成5不满足条件跳出循环，这就是`for`循环重复运行5次的实质。

现在我只想强调`for`循环的三段申明，第一段时开始`for`循环时会运行一次；第二段是一个比较后的`bool`类型，它将在`for`循环一次结束后进行评估；第三段看上去要在`for`循环最后被运行，我们可以把变量`i`的声明放在`for`之前，然后让`for`里面的第一段完全空着，`i++`放在函数体内效果也是完全一样：

```c++
#include <iostream>
#include "Log.h"

int main(){
    int i = 0;
    for (; i < 5; ) {
        Log("Hello World");
        ++i;
    }

    std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210607224642246.png)



同样的我们替换中间的条件也可以得到同样的效果：

```c++
#include <iostream>
#include "Log.h"

int main(){
    int i = 0;
    bool condition = true;
    for (; condition; ) {
        Log("Hello World");
        ++i;
        if (!(i < 5))
            condition = false;
    }

    std::cin.get();
}
```









#### while循环

`while`循环和`for`循环一样，它只是没有开头的申明以及后面的语句，仅有条件语句。

我们写`while`循环时，先输入`while`关键字，然后在里面输入条件例如`i < 5`。如果我们运行，它会运行这里面的代码：

```c++
#include <iostream>
#include "Log.h"

int main(){
    for (int i = 0; i < 5; ++i) {
        Log("Hello World");
    }
    
    Log("===============");
    
    int i = 0;
    while (i < 5){
        Log("Hello World");
        i++;
    }
    
    std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210607225522737.png)



可以看到两种循环得到的结果完全一样，都是将`Hello World`打印五次。

那为什么我们用一个循环而不用另外一个循环？这就看你是否需要变化，因为循环的内容都是一样的，你都可以交换使用，它更像一种习惯或者风格，而不是规矩，这两种循环没有什么实质性的区别，它们可以做完全一样的事情。

但是有一种习惯约定是如果你有一个已经存在的确定的条件，你只是想做一些比较（例如前面提到的游戏循环，那里有一个变量叫做`running`），你可能想让这个游戏持续循环，只要这个`running`变量设置为`true`即可。如果要做类似于这样的事情的时候，我可能会用`while`循环，因为条件是不变的，我不需要在每次循环之后改变这个条件，我们不需要在循环前先声明这个条件变量，我们可以将之前的变量或函数调用后的结果拿来用，不需要保持更新或者初始化某些东西。

然而当我们处理数组的时候，我会使用`for`循环。当我们的迭代进行的时候，这和数组的索引完全一致，非常适合，我们之后会深入学习。





### 控制流语句

控制流语句与循环语句一起工作，换句话说它让我们可以更好地控制这些循环的实际运行。我们有三个主要的控制流语句，我们可以使用`continue`、`break`和`return`，它们做不同的事情：

+ `continue`只能在循环中使用，表示进入这个循环的下一个迭代（如果还有下一次迭代的话），如果没有循环就会结束
+ `break`主要用于循环中，然而它也出现在`switch`语句中，表示跳出/终止循环
+ `return`会完全脱离你的函数。如果你在一个函数中，碰到了一个`return`关键字，你会退出这个函数。函数可能需要一个返回值，如果只有`return`就只能返回`return`本身；如果你的函数需要返回值的话，你需要为它提供一个值



#### continue

`continue`将跳到`for`循环的下一个迭代：

```c++
#include <iostream>
#include "Log.h"

int main(){
    for (int i = 0; i < 5; ++i) {
        if (i % 2 == 0)
            continue;
        Log("Hello World");
        std::cout << i <<std::endl;
    }

    std::cin.get();
}
```



可以看到，从第一个开始，每两个迭代就会跳过一个，只在奇数行迭代：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210607232146805.png)



让我们换个简单点的看看，条件改为`i > 2`：

```c++
#include <iostream>
#include "Log.h"

int main(){
    for (int i = 0; i < 5; ++i) {
        if (i > 2)
            continue;
        Log("Hello World");
        std::cout << i <<std::endl;
    }

    std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210607232516061.png)

好了，这就是`continue`的大致内容：被执行时跳到`for`循环的下一个迭代。





#### break

如果我们把`break`替换`continue`，它会打印第一个：

```c++
#include <iostream>
#include "Log.h"

int main(){
    for (int i = 0; i < 5; ++i) {
        if ((i + 1) % 2 == 0)
            break;
        Log("Hello World");
        std::cout << i <<std::endl;
    }

    std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210608081415202.png)



一旦程序到达`break`语句，循环结束了，游戏结束了。这就是`break`，完全跳出`for`循环，当然，这些控制流语句可以用在所有的循环语句中，因此`for`循环、`while`循环、`do while`循环工作方式是一样的。





#### return

这是一个需要返回`int`的函数，我们不能只写`return`，而需要写`return XXX`：

```c++
#include <iostream>
#include "Log.h"

int main(){
    for (int i = 0; i < 5; ++i) {
        if ((i + 1) % 2 == 0)
            return 0;
        Log("Hello World");
        std::cout << i <<std::endl;
    }

    std::cin.get();
}
```



就控制流语句而言，`return`可以在任何地方使用，它会退出这个函数。当然，如果你的函数要返回一个值，`return`必须给它一个值来返回。这些控制流语句就是控制你代码如何流动的，循环语句和`if`语句以及这些控制流语句构成了编程的基本逻辑，你可以使用这些工具来控制程序的流程。





### 指针

指针可能是本系列最重要的一节，但也是很多人都痛苦的领域，今天我们讨论的是原始的指针，不是智能指针。对于计算机来说，内存就是一切，如果要我说出编程中最重要的一件事，可能就是内存。

当你编写一个应用程序并启动它时，所有的程序都被载入到内存中，所有的指令高速计算机在你写的代码中需要做什么，所有这些都被加载到内存中，CPU就是这样访问你的程序并开始执行它的指令。当你创建一个变量从磁盘加载数据时，所有的东西都存储在内存中，如果没有内存就什么也做不了，而指针对于管理和操纵内存非常重要。

指针是一个整数，一种存储内存地址的数字。我不想深入讨论内存在计算机中是如何工作的，只要把你的内存放在电脑里面，就像一个大直线，描述一条你居住城市的街道，有开始也有结束，线上就是一排房子。这就是计算机中的内存，它只是一条线性的线，在这条街上的每一所房子都有一个号码和地址，把这个比喻用在电脑上想象一下，这条直线上的每一栋房子都有一个地址，是一个字节数据。

我们显然需要一种方法来寻址所有的byte（我们这条街上所有的房子），例如某人在网上订了东西，想要送货上门，它需要被送到正确的房子里，或者可能有人把东西从他们的房子里送出去，无论哪种方式你都需要能够从这些房子的内存字节中读写。

因此指针就是这些地址，这些地址告诉我们房子在哪里，这是非常重要的，因为我们在代码中做的几乎所有事情都是从内存中读写。当然你完全可能写一个不使用指针的C++程序，然而它是非常有用的工具，正如我之前提到的内存可能是你拥有的最重要的东西，能够对内存有更多的控制是至关重要的。

让我们来看看一些例子：

```c++
#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main(){

    std::cin.get();
}
```



我们要创建最纯粹的指针，是一个空的指针。`void`的意思是无类型，记住，一个指针就是一个地址，它只是一个在内存中保存地址的整数，它不需要类型。如果我们给指针一个类型，只是说这个地址的数据被假设为我们给的类型，除此之外它没有任何意义，它只是一些我们在实际的源代码可以编写的东西，使我们的生活在语法层面上更容易，为了让我们的生活更轻松，我们可以使用指针类型。

但是再一次声明，类型不会改变一个指针的性质，实质就是指针只是一个内存的地址，它是一个整数，所以`void`指针意味着我们现在不关心我们的代码中这个指针是什么类型的，我们只想保存一个地址：

```c++
#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main(){
    void* ptr = 0;

    std::cin.get();
}
```



我们把刚声明的指针称为`ptr`，pointer的简写。我们将它设为0，相当于我们给这个指针的内存地址是0，0实际上不是一个有效的内存地址，内存地址不会一直到零，这意味着这个指针是无效的。无效指针是完全可以接受的状态，但我要说0不是一个有效的内存地址，我们不能从内存地址0种读取或写入，如果我们尝试这样做的话我们的程序会崩溃。

我们也可以写成`NULL`，因为`#define NULL 0`：

```c++
#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main(){
    void* ptr = NULL;

    std::cin.get();
}
```



C++提供了关键字`nullptr`，效果也是一样的，这个会在C++11介绍。太棒了，我们做了第一个指针，它是无类型的，它的内存地址是0，这可能是你能写的最简单的指针。

让我们做一些更有用的事情，让我们创造一个整数变量`var`，只是一个普通的整数。当然，我们创建的每个变量都有一个内存地址，我们需要一个地方来存储这个变量。如果我想知道这个变量的内存地址，我可以通过使用`&`运算符来做到这一点，如果我在一个已经存在的变量前面加上一个`&`号，我们实际上是在问这个变量：“嘿，你的内存地址是什么？”，然后我们取这个变量的内存地址把它赋给一个新的变量`ptr`：

```c++
#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main(){
    int var = 8;
    void* ptr = &var;
    std::cin.get();
}
```



就是这样，我们现在有了变量的内存地址，我们把它存储在另一个变量中。放置一个断点调试我们的程序：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210608091531054.png)



指针的格式以十六进制格式呈现给我们，这个指针变量现在保存的是`var`变量的内存地址，这就是指针的工作方式：一个保存地址的变量。

指针就像其他变量一样，它不是保存变量这样的值本身，它的内存地址也是值，也是一个整数。这个整数有多大，这个指针有多大取决于很多东西，可能是32位整数，也可能是64位，也可能是16位，关键是它是一个整数。

回到我的代码，把这个变成一个整数指针，实际上我没有改变任何东西：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210608092354392.png)



类型无关紧要，但类型对该内存的操作很有用，所以如果我想对它进行读写，类型可以帮助我，因为编译器会知道一个整数应该是四个字节，所以我要在那儿设置一个值，它会设置四个字节的内存，但最终类型是完全没有意义的，在之后我们会更深入地研究它，但现在，不用担心类型。

假设我想使用我的数据，我有一个指针指向那个数据，然而现在我想要写入或读取这些数据。我知道数据在哪里，但是我怎么才能访问它呢？这就是靠逆向引用了（指针的`*`运算符通常被称为`dereference`运算符），我们有`var`变量，指针`ptr`指向`var`，但我怎么才能回到这个`var`呢？

可以通过在指针前面插入一个`*`来实现这一点：

```c++
#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main(){
    int var = 8;
    void* ptr = &var;
    *ptr = 10;
    std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210608093418187.png)

我实际上是在逆向引用那个指针，这意味着我现在正在访问我可以读取或写入数据的数据。然而我试着这么做，你会看到我实际得到了一个错误，因为这个指针是一个空指针，计算机不知道那是什么：这个10是`short`两个字节的整数？`int`四个字节的整数？`long long`八个字节的整数？我们不知道这需要多少字节的数据，我们说是10，但是10可以代表任何东西，我们需要告诉编译器这是一个整数：

```c++
#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main(){
    int var = 8;
    int* ptr = &var;
    *ptr = 10;
    std::cin.get();
}
```



此时我们打印`var`，你会看到我得到的值是10：

```c++
#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main(){
    int var = 8;
    int* ptr = &var;
    *ptr = 10;
    LOG(var);
    std::cin.get();
}
```



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210608094123580.png)



所以我们成功地把它从8改成了10，通过逆向引用（`*`）一个指针我可以访问这个数据。所以现在你应该知道指针是如何工作的，这就是它的全部：指向内存中的一个位置。

有人说它指向一个内存块，这不是很准确，因为我们不知道这块内存是多大。在这个例子中它是4个字节，因为我们创建了一个整数，一个整数是4字节的内存，所以我们知道这个指针指向的内存是4个字节，然而在实际的指针中，我们并不知道内存多大。



我能做的是在堆上创建一个变量，或者问我们的电脑：“嘿，我想让你给我分配一些内存，我想有一定的尺寸”。所以我现在能做的就是使用`char*`，我们知道`char`是一个字节，我真正要求的是8字节的内存：

```c++
#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main(){
    char* buffer = new char[8];
    
    std::cin.get();
}
```



这给我们分配了8个字节的内存，并返回一个指向那块内存开始的指针。然后我可以使用一个叫做`memset`的函数，它用我们指定的数据填充一个内存块，它接收一个指针，这个指针将会是内存块开始的指针：

```c++
#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main(){
    char* buffer = new char[8];
    memset(buffer,0,8);
  
    delete[] buffer;
    std::cin.get();
}
```



还有一点我想说的是指针本身是变量，这些变量也存储在内存中，这就是我们可以得到双指针或三指针，意思是指向指针的指针：

```c++
#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main(){
    char* buffer = new char[8];
    memset(buffer,0,8);

    char** ptr = &buffer;
    std::cin.get();
}
```



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210608100027775.png)



### 引用

今天我们要讲的是引用，引用实际上只是指针的扩展，所以你需要能够理解指针是如何工作的。

指针和引用是在C++中被大量翻来覆去提及的两个关键字，计算机现在用它们做的事情几乎是一样的。从语义上来说，我们如何使用和书写它们有一些细微的区别，但根本上引用通常只是指针的伪装，它们只是指针的语法糖，让它更容易阅读，更容易理解。

引用基本上就是它听起来的名字，这是一种我们引用现有变量的方式。不像指针你可以创建一个新的指针变量，然后设置它等于空指针或类似的东西，引用必须“引用”已经存在的变量，引用本身并不是新的变量，它们不像典型的变量并不占用内存，没有真正的存储空间。

回到代码，假设我有一个变量`a`，然后我想给这个变量创建一个引用，我可以输入变量的类型后面跟进一个`&`符号。注意`&`符号实际上是变量声明的一部分，之前讲指针时我们可以使用`&`运算符来实际获取现有变量的内存地址，这里不同，因为`&`符号实际上是类型的一部分。

```c++
#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main(){
    int a = 5;
    int& ref = a;

    std::cin.get();
}
```



所以现在我们所做的就是创造了一个叫别名的东西，因为这个`ref`“变量”（它不是一个真正的变量）实际上不存在，它只存在于我们的源代码中。如果你现在编译这段代码，你不会得到两个变量`a`和`ref`，你只会得到`a`。

我们现在能做的是，我们可以使用`ref`就像它是`a`。如果我们设`ref`为2然后打印`a`：

```c++
#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main(){
    int a = 5;
    int& ref = a;
    
    ref = 2;
    LOG(a);
    std::cin.get();
}
```



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210608105508074.png)



运行程序`a`等于2，我们通过`ref`改变了`a`的值，无论发生什么，`ref`都是`a`，我们给`a`记了个别名。在这种情况下，我们的引用不是一个指针或类似的东西，编辑器不需要实际创建一个新变量，编译时这个代码相当于你设置了`a = 2`。

让我们尝试一些更复杂的东西。假设我们想写一个整数变量递增的函数`Increment()`：

```c++
#include <iostream>

#define LOG(x) std::cout << x << std::endl

void Increment(int value){
    value++;
}

int main(){
    int a = 5;
    Increment(a);
    LOG(a);
    std::cin.get();
}
```



可以看到调用`Increment`函数只通过值传递它，它会考呗这个值5复制到函数中，复制会创建一个全新的变量`value`，运行代码：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210608110227651.png)



我需要做的是通过引用来传递变量，这样它才会递增，因为我真正想做的是影响这个变量。如何通过将这个变量传递到函数中来修改它呢？我们可以把`a`变量的内存地址传递过去，写入该内存地址：

```c++
#include <iostream>

#define LOG(x) std::cout << x << std::endl

void Increment(int* value){
    (*value)++;
}

int main(){
    int a = 5;
    Increment(&a);
    LOG(a);
    std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210608110824612.png)



我们成功地通过引用将变量传递到一个函数中。然而我们同样可以用引用更简单、用更少的代码和更少的修饰语法：

```c++
#include <iostream>

#define LOG(x) std::cout << x << std::endl

void Increment(int& value){
    value++;
}

int main(){
    int a = 5;
    Increment(a);
    LOG(a);
    std::cin.get();
}
```



我们基本上重写了代码，但做了完全相同的事情，这一次我们的代码看起来漂亮，这也是唯一的区别了。这就是引用的全部真相了，它们只是语法糖，对于引用没有什么是指针不能做的。

关于引用另一件重要的事情是一旦你声明了一个引用，你不能改变它引用的东西：

```c++
#include <iostream>

#define LOG(x) std::cout << x << std::endl

void Increment(int& value){
    value++;
}

int main(){
    int a = 5;
    int b = 8;
    
    int& ref = a;
    ref = 8;
  
  //a = 8, b = 8
  
    Increment(a);
    LOG(a);
    std::cin.get();
}
```





同样的，当你声明一个引用时你需要把它进行赋值，你不能不赋值，编译器不会让你这样做，它需要一个初始化。当你声明一个引用时，你必须马上给它赋值，因为它必须引用一些东西，记住它不是一个真正的变量，只是一个引用。
