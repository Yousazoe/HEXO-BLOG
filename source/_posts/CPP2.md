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



#### step into

`Step Into`的意思是进入到这行代码的函数里（如果这一行有一个函数的话）。在这种情况下，如果我点击`Step Into`，在`Log`这一行我们将步入进`Log`函数，我们可以看到它到底干了什么。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210511220830764.png)

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210511220906112.png)

#### step Over

`Step Over`就是从当前函数跳到下一行代码。

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210511220739489.png)



#### step Out

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



#### for

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









#### while

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







### 数组

今天我们谈论 C++ 数组。

首先什么是数组？数组基本上是元素的集合，按特定的顺序排列的一堆东西。在我们的例子中，C++ 数组就是表示一堆变量组成的集合，一般是一行相同类型的变量。

数组如此重要和有用的原因，是因为我们经常想要表示一大堆数据的数据集合。对我们来说，创建一大堆变量是没有意义的，这些数据应该放在一个数据集中。因为变量需要手动创建，我们需要进入代码中，指定变量并给它们命名，然而有时我们只是想要能够存储50个整数，代表某种数据。我们不想去详细说明整数1号、整数2号......一直到整数50号，这太恐怖了，根本不可行，无法维护，想象一下要设置所有这些变量等于0，你要写50行代码。

处理这么多变量真的很难，在这种情况下，我们想做的是使用一个数组来包含所有50个相同类型的元素，处理起来会轻松很多。记住，数组基本上就像在一个变量中有多个变量，我们给一个数组起一个名字，通过这样我们可以创建数组引用尽可能多的变量。



#### 数组

让我们到代码中看一看。定义数组非常简单，假设我想要一个有5个整数的数组，我写上我想要的数组类型，然后给它一个名字，在中括号中放入个数：

```c++
int example[5];
```

现在我们有一个有5个整数的数组，并且分配了足够的空间来存储这5个整数。

现在我们要设置和访问这些整数，我可以写数组的名字，然后在方括号内写一种叫 index（索引）的东西。索引是我在数组中指向的那一个变量或者元素。第一个元素要写上0，因为在 C++ 中下标是从0开始的，一些语言比如 lua 是从1开始的，通常数组都是从0开始的，这意味着下标0代表第一个元素：

```c++
example[0] = 2;
example[4] = 4;
```

当我们在一个特定的索引上访问这些元素之一时，我们得到这个元素的类型就是数组的类型，在这里就是整型 `int`。第一个索引是0还意味着最后一个索引应该是4而不是5，我们分配了5个整数的空间。



读取这些元素很简单，如果我们想打印一个，我们只需要指明索引就行了。如果你想打印这个数组，你需要打印这个数组的地址（实际上这是一个指针类型）：

```c++
std::cout << example[0] << std::endl;
std::cout << example << std::endl;
```



如果我试图访问一个不存在的索引，例如-1或5，会发生 Memory access violation（内存访问违规）：

```c++
example[-1] = 5;
example[5] = 2;
```



我在试图访问不属于我的内存。在 `Debug` 模式下，你会得到一个程序崩溃的错误消息，来帮助你调试这些问题。然而在 `Release` 模式下，你可能不会得到报错信息，这意味着你已经写入了不属于你的内存。

这一点非常重要，你要注意确保总是在数组的边界内写东西，否则会导致一些很难挑事的问题。因为我们修改了内存，而这些内存不是这个数组的一部分，很有可能是源码中另一个变量的一部分，我们在没有意识的情况下将代码中其他变量改掉了。



数组与 `for` 循环经常在一起，因为 `for` 可以通过索引在一个特定的范围内遍历。如果我们想设置 `example[]` 数组中的每一个值，可以通过 `for` 循环实现：

```c++
#include <iostream>

int main(){
    int example[5];
    for (int i = 0; i < 5; ++i) {
        example[i] = 2;
    }

    std::cin.get();
}
```



正如之前所提到的，数组实际上只是一个指针。我可以在这里创建一个整型指针，并把它赋值为 `example`：

```diff
#include <iostream>

int main(){
    int example[5];
+   int* ptr = example;
    
    for (int i = 0; i < 5; ++i) {
        example[i] = 2;
    }

    std::cin.get();
}
```



访问2号元素设置等于5或类似的东西，相当于写入从指针开始8个字节的偏移量的地址。所以这部分实际上可以用指针简单地重写：

```c++
example[2] = 5;
*(ptr + 2) = 6;
```



注意我这里的 `+2` 并不是指字节。当你处理指针运算时，在指针加上像2这样的值计算实际要加的字节数（偏移）取决于类型。这里我们是整数 `int` 指针，将会增加 2 * 4 的偏移（4 时每个整型 `int` 的大小）。 

我们可以将这个 `ptr` 指针转换为一个字节的类型，例如一个 `char*`。如果这样我还得加上刚才提到的8个字节：

```c++
example[2] = 5;
*(int*)((char*)ptr + 8) = 6;
```

因为我想写的是一个四字节的整数，不仅仅只是一个字节大小的 `char`，所以我们需要把类型转换为 `int` 指针类型，这样指向就是整型了，但这是相当奇怪的代码。



#### 堆栈

我们还可以在堆上创建一个数组，虽然还没讨论过栈和堆以及它们的内存是如何运作的，但我们先来看看。首先通过 `new` 关键字来创造一个数组：

```c++
#include <iostream>

int main(){
    int example[5];
    int* another = new int[5];

    std::cin.get();
}
```



这代码和之前的代码是一个意思，然而生存期是不同的：前者是在栈上创建的，当我们到达最后花括号跳出作用域范围时，它会被销毁；后者是在堆上创建，直到我们程序把它销毁之前都是处于活动状态，所以你需要用 `delete` 关键字来删除。

因为这是一个数组，我们在这里使用数组的操作符 `[]` 来分配内存，所以我们还需要像这样使用方括号删除它：

```c++
#include <iostream>

int main(){
    int example[5];
    int* another = new int[5];
    delete[] another;
    
    std::cin.get();
}
```



所以为什么要动态地使用 `new` 来分配而不是在栈上创建呢？最大的原因是生存周期，用 `new` 来分配内存它将一直存在，知道你删除它。如果你有一个函数返回一个数组，你必须使用一个 `new` 关键字来分配它，除非你传入一个数组的地址参数。如果你想返回一个数组，这个数组是在函数中创建的，你需要使用 `new` 关键字。

此外另外一件事也需要考虑：间接寻址。我们实际上有一个指针，那个指针会指向另一个内存块，这个内存块保存了我们实际的数组，这将会产生某种内存碎片（memory fragmentation）、缓存丢失（cache miss）以及所有这些复杂的东西，这些会在之后讲到。

让我们来看一个实际的例子：

```c++
#include <iostream>

class Entity {
public:
    int* example = new int[5];

    Entity() {
        for (int i = 0; i < 5; ++i) {
            example[i] = 2;
        }
    }
};

int main(){
    Entity e;

    std::cin.get();
}
```



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210709165427688.png)



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210709165525823.png)



这就是所谓的内存间接寻址，我们实际得到 `e` 的内存地址，它包含另一个地址（我们数组的实际内存地址），这意味着当我们想要访问这个数组时要在代码周围跳来跳去：首先找到 `Entity`，接着找到数组，然后所有这些东西。

 所以只要有可能你应该在栈上创建数组避免这种情况，因为这样在内存中跳跃肯定会影响性能。



#### 标准数组

我还想提一下 C++11 里面的数组。在 C++11 我们有标准数组 `std::array`，这是一个库中内置的数据结构。很多人喜欢用它来代替我在这里展示的原始数组，因为它有很多优点比如边界检查、记录数组大小（我没有提到的一点是，实际上没有办法计算出原始数组的大小）。

虽然我说不可能，但其实是有一些方法，因为当你删除这个数组的时候，编译器需要知道实际要释放多少内存。方法就是通过编译器相关的东西，它可能有时存储在数组的一个负索引里面，这取决于很多因素。因此，你永远不应该在数组内存中访问数组的大小，这是危险的。

如果你在栈上分配一个数组 ，你不知道它的实际大小。所以如果你写 `sizeof(a)`，得到的是数组占了多少个字节，这里 `int` 是4个字节而我们有五个数组元素，所以有20个字节：

```c++
int a[5];
int count = sizeof(a) / sizeof(int);
```



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210709172149360.png)



所以如果你想知道里面有多少元素，你可以把它们除以数据类型的大小，这行代码会给出元素的计数，也就是我们已经分配的元素的数量。然而你真的不能相信这个方法，如果它变成了 `int` 指针就完蛋了。所以你要做的是自己维护自己的数组大小，从这个意义上说糟糕透了，但它就是这样运作的，你必须自己维护它。

我个人写这种代码的方式是声明一个常量 `size`，大小为5：

```c++
static const int size = 5;
int* example = new int[size];

for (int i = 0; i < size; ++i) {
  	example[i] = 2;
}
```



如果你决定使用 C++11 的数组，你可以这样做：

```c++
std::array<int, 5> another;

for (int i = 0; i < another.size(); ++i) {
  	example[i] = 2;
}
```



这是一种很简单的处理方式，当然它也有开销，通常都是值得的。

就我个人而言，我总是使用原始数组，大多数人可能用它会更快一点，我个人使用它们的时候，并没有遇到什么问题。说实话，使用 `std::array` 会被使用原始数组安全得多，但我喜欢过危险的生活。



### 字符串

首先什么是字符串？一般来说，字符串本质上是一个接一个字符的一组字符（字母、数字、符号）。所以它对我们来说很常见，作为人类当然想要在我们的电脑上以某种方式表示文本，当我编程时想要能够表示文本或一组文本，它可以是一个单个的字符，可以是一整个段落，可以是一个单词，也可以是一堆单词，所有这些被称为字符串的东西都是一个文本字符串。我们需要一些方法能够在我们的程序中表现出来，这就是 C++ 字符串。对于我们来说，这是一种能够表示和处理文本的方法。



#### 字符

为了理解 C++ 中的字符串是如何工作的，你首先需要理解字符是如何运作的，以及字符到底是什么。字符就像字母符号、数字等以不同的形式呈现。现在你可能已经注意到在 C++ 中，有一种数据类型叫做 `char`，是 Character 的缩写。到目前为止，我们已经用过了，这是一个字节的内存，它很有用，因为它能把指针转换成 `char` 型指针这样你就可以用字节来做指针运算。

它对于分配内存缓冲区也很有用，因为如果你想分配 1k 的内存，你可以分配1024个 `char`。它对字符串和文本也很有用，因为 C++ 对待字符的默认方式是通过 ASCII 字符进行文本编码，在这里不多赘述，但是我们在 C++ 中处理字符是一个字符是一个字节，这就是 ASCII。ASCII 可以扩展成很多，比如 utf-8、utf-16、utf-32......我们有宽字符（wide string），当然字符是可以大于一个字节的，我们有两个或四个字节的字符。其他语言比如日文、中文或其他语言有一些不同的字符，和我们在英文中看到的不同，我们需要能够使用这些，因为我们需要有足够多的字符。

如果我们只有一个字节来表示一个字符，八个比特，这意味着我们有2的8次方可能的结果，也就是265种可能性，而它们远远超过了265个字符，如果你把英文字母算进去、数字、符号、日文字母、韩国字母......所有这些，所以我们不能兼顾所有语言，你知道，8个比特根本不够，所以有16位字符编码，这意味着我们有2的16次方种不同的可能性。

我们还有很多其他的编码，但在 C++ 中只是基础语言，不使用任何库，只是原始数据类型。`char` 是一个字节，这就是为什么当你在 C++ 中使用一个字符串，而不是2个字节的宽字符串。普通的字符串使用普通的字符，我们说的是一个字节的字符，我们主要说英文。如果你需要学习其他语言比如俄罗斯，那就做不到使用一个字节的编码，你将不得不使用某种不同的字符编码，我们可以在未来讨论这些。



#### 字符串

介绍了这么多，我们来讨论一下字符串是如何在 C++ 中工作的。字符，就是 `char` 数据类型；而字符串实际上是字符数组，而数组又是一组元素的集合，所以一组字符组成了字符串或文本。你可能已经注意到，在本系列中我们经常把字符串称为 `const char*`，让我们来看看它是如何工作的：

```c++
#include <iostream>

int main(){
    const char* name = "YOUSAZOE";

    std::cin.get();
}
```



这是 C 语言风格定义字符串的方式。因为我们 C++ 有一个库，这使得字符串操作对我们来说要简单得多，但了解它是如何工作的仍然很重要。

你其实不需要把它声明为 `const`，但人们通常这样做的原因是不想去改变这些的值，因为字符串是不可变的：

```c++
char* name = "YOUSAZOE";
```

意思是说，你不能扩展字符串并使它变大，因为这是一个固定分配的内存块。如果你想要一个最大的字符串，它需要执行一个全新的分配并删除旧的字符串。



现在这里的 `char*` 并不意味着它是在堆上分配的，你不能通过 `delete` 删除这些东西，也不能通过 `delete[]` 之类的（经验法则是没有 `new` 就不要有 `delete`）。

如果你声明成 `const`，这意味着你不能再改变它的内容，这会导致错误。所以如果你知道你不会修改字符串，就可以加上 `const`；否则去掉 `const`。



#### 工作原理

下一个问题是一个字符串在内存中是什么样的呢？它究竟是如何工作的呢？设置断点运行我们的程序：

```c++
#include <iostream>

int main(){
    char* name = "YOUSAZOE";
    name[2] = 'N';
    
    std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210710032639656.png)



可以看到内存视图一边是 ASCII 码表示，可以通过码表转义。`YOUSAZOE` 就是由这八个字符组成，然后我们可以看到有一个被设为0的字节，这被称为空终止字符，这样我们就知道那时字符串结束的地方。

你会注意的我们从来不知道 `YOUSAZOE` 有多大，它只是一个指针，那么我们怎么知道它的大小呢？空终止字符就是这样来的，字符串从指针的内存地址开始，然后继续下去直到它碰到0，意识到这是空终止字符，在字符串的结尾。

我创建了另一个名为 `name1` 的 `char` 数组，有八个字符并初始化。我把它设为单个字符（C++ 的字符是单引号，不是双引号，双引号默认是 `char*`）：

```diff
#include <iostream>

int main(){
    char* name = "YOUSAZOE";
+   char name1[8] = {'Y','O','U','S','A','Z','O','E'};
    
+   std::cout << name1 << std::endl;    
    name[2] = 'N';

    std::cin.get();
}
```



这是一个数组，不是字符串。你可以看到一个包含八个字符的数组，这里没有空终止字符。如果我试着把 `name1` 打印到控制台：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210710034338514.png)



因为这里没有0，`std::cout` 就不知道打印到哪里结束，这就是这个 `w` 出现的原因。然而如果我们扩展一个 `0` 或 `\0`，它会被正确的打印：

```diff
#include <iostream>

int main(){
    char* name = "YOUSAZOE";
+   char name1[9] = {'Y','o','u','s','a','z','o','e','\0'};

    std::cout << name1 << std::endl;
    name[2] = 'N';

    std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210710035229863.png)



这就是字符数组的工作原理，字符串就是这样工作的。

那么我们应该如何在 C++ 中使用字符串？在 C++ 中的标准库中有一个名为 `string` 的类，实际上有一个类叫 `basicString`，它是一个模板类。`std::string` 基本上是 `basicString` 类的模板版本，模板参数是 `char`，这叫模版特化（template specialization），就是将 `basicString` 模板类中的模板参数设为 `char`，意为 `char` 是每个字符背后的实际类型。有一种叫 `wString` 的东西，也就是宽字符串 `wide string`，我们可以用一个简单的例子，在 C++ 中使用的字符串，你应该用 `std::stirng`。

`std::string` 怎么工作的？他只是一个 `char` 数组和一些操作这个字符数组函数，我们之后会在数据结构里重新实现自己的版本，以及如何优化，但现在它只是一个数组和一些函数。

那么让我们来谈谈如何使用 `std::string`。回到我们的代码，改用 `std::string`：

```diff
#include <iostream>
+#include <string>

int main(){
+   std::string name = "YOUSAZOE";
    char name1[9] = {'Y','o','u','s','a','z','o','e','\0'};

    std::cout << name1 << std::endl;
    name[2] = 'N';

    std::cin.get();
}
```



`string` 有一个构造函数，它接受 `char*` 或 `const char*` 参数。如果你把鼠标悬停在这个上面，你会看到它实际上是一个 `const char` 数组：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210710123435907.png)



为什么你通常会把它赋值给 `const char*` 而不是 `char*`？因为本质上当你定义字符串时，用双引号引起来的一个单词或者多个单词在 C++ 中是 `const char` 数组，而不是 `char` 数组。

如果我们没有把这个 `string` 头文件包括进去，会得到一个错误。输出流会告诉我们，不能把字符串发送到 `cout` 流中，因为这个操作符允许我们发送字符串到流中的重载版本在 `string` 头文件内部。

当然，因为 `std::string` 是一个有很多功能的类，我们实际上有所有这些方法：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210710135455259.png)



我们可以找出它的尺寸：

```c++
name.size()
```



如果我们是 `const char*` 或 `char*`，我们就需要用到 C 函数比如 `strlen()`：

```c++
char* s;
strlen(s);
```



另外一个常见的事是追加字符串，我想在 `YOUSAZOE` 加上 `hello`会出现错误：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210710141541127.png)



发生这种情况的原因是你实际上是想将两个 `const char` 的数组相加。这个双引号里面的东西是 `const char` 数组，它不是真正的字符串，不能把两个指针相加，不能把两个数组直接相加。

所以如果你想做这样的事，一个很简单的方法是把它分开多行，用 `+=` 操作符重载：

```c++
std::string name = "YOUSAZOE";
name += "hello";
```



或者将两个相加的字符数组中的其中一个，显式调用一个 `string` 构造函数：

```c++
std::string name = std::string("YOUSAZOE") + "hello";
```



如果你想找到字符串中的文本，你可以使用 `name.find()` 查找文本字符串：

```c++
bool contains = name.find("ZOE") != std::string::npos;
```





我想快速提一下的另一件事，是把这些字符串传递给其他函数。如果我写了一个叫 `printString()` 的函数，我想要传递一个字符串，我不会简单地写 `std::string`：

```c++
void printString(std::string str) {
		std::cout << str << std::endl;
}
```



我不会这样做的原因是这实际上是一个副本，我们之前没有过多讨论过这个问题，但当你这样把类（对象）传递给一个函数时，你实际上在复制这个类（对象）。如果我要做诸如 `string += "h"` 这样的事情，它不会影响到传递的原始字符串。

这显然是一个只读函数，我们不修改任何东西，我们只是想把它打印出来，为什么我们要复制整个字符串呢？这意味着我们必须动态地在堆上分配一个全新的 `char` 数组来存储我们已经得到的完全相同的文本。

这可不快，字符串复制实际上相当慢。因此当你传递一个这样的字符串而且是只读的情况下，确保通过常量引用传递它：

```c++
void printString(const std::string& str) {
		std::cout << str << std::endl;
}
```



`&` 引用意味着它不会被复制；而 `const` 意味着我们承诺不会在这里修改它。





#### 字面量

今天我们讨论字符串字面量，这是一种基于字符串的东西，会讲的更深一点。

字符串字面量，是在双引号之间的一串字符。我可以定义一个字符串字面量，然后通过双引号在之间写点东西：

```c++
#include <iostream>
#include <string>

int main(){
    "YOUSAZOE";

    std::cin.get();
}
```



好了，现在是一个字符串字面量。它会变成什么，取决于很多因素，最基本的情况下它是一个 `const char` 数组，长度为9。接着你可能注意到了，这里实际上只有8个字符，那为什么数组长度是9呢？原因是在这种情况下，字符串的最后有一个额外的字符：空终止字符，字符串的结束位置是0，代表 null 字符的意思而不是字符的 `0`。

所以如果我们想做一些事情比如在字符串中间搞个 `\0`，在许多情况下实际上会破坏这个字符串的行为：

```c++
#include <iostream>
#include <string>

#include <stdlib.h>

int main(){
    const char name[9] = "YOU\0ZOE";

    std::cin.get();
}
```



如果我想看到我的字符串是什么，我可以运行 C 函数 `strlen()` 计算字符串长度的函数：

```diff
#include <iostream>
#include <string>

#include <stdlib.h>

int main(){
    const char name[9] = "YOU\0ZOE";

+   std::cout << strlen(name) << std::endl;
    std::cin.get();
}
```



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210711005436382.png)



查看结果是3，然而很显然它的长度超过了三个字符。得到这个结果的原因是它只计算到 `\0` 之前的字符数，碰到0就认为是字符串的结尾了。如果我们移除 `\0`，重新运行，得到的就会是6：

```c++
#include <iostream>
#include <string>

#include <stdlib.h>

int main(){
    const char name[9] = "YOUZOE";

    std::cout << strlen(name) << std::endl;
    std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210711011259660.png)





### 常量

今天我们来讲 C++ 的 `const` 关键字。

`const` 是被我称之为伪关键字的东西，因为它在改变生产代码方面做不了什么。它有点像类和结构的可见性，这是一个机制，让我们的代码更加干净，并对开发人员写代码强制特定的规则。

`const` 基本上就像你做出的承诺，它承诺某些东西将是不变的，也就是说它不会改变。然而它只是一个你可以绕过的承诺，你可以打破你的承诺，就像你在现实生活中一样。这里关键是承诺，它承诺一些东西是不变的，你是否遵守诺言取决于你自己。

但话又说回来，这是一个承诺，你应当遵守承诺。我们要保持 `const` 的原因是这个承诺实际上可以简化很多代码，有很多好处，让我们来看看代码：

```c++
#include <iostream>

int main(){
    int a = 5;
    a = 2;

    std::cin.get();
}
```



按照上面的声明为可以把 `a` 改成任何我喜欢的数，然而如果我声明这是一个 `const`，我无法改变它：

```diff
#include <iostream>

int main(){
+   const int a = 5;
    a = 2;

    std::cin.get();
}
```



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210707173833105.png)



这里可以看到，通过 `const` 首先我们从语法上指定了这个整数是一个常数，我不打算修改它，它只是一个需要在程序中保持不变的数字。



#### 指针

现在常量还有其他几种用法，让我们聊聊，首先是指针：

```c++
int* a = new int;
```



因为这个声明没有使用 `const`，这里我可以做两件事，我可以逆向引用 `a`，然后将它设为一个值比如2：

```c++
#include <iostream>

int main(){
    const int MAX_AGE = 90;
    
    int* a = new int;
    *a = 2;
    std::cout << *a << std::endl;
    
    std::cin.get();
}
```



然后我可以做的另一个事情就是重新分配实际的指针，这样它就会指向别的东西，比如 `MAX_AGE`。为了绕开这个 `const` 限制，我把它强制转换成 `int*` 类型：

```c++
#include <iostream>

int main(){
    const int MAX_AGE = 90;

    int* a = new int;
    *a = 2;
    a = (int*)&MAX_AGE;

    std::cout << *a << std::endl;
    std::cin.get();
}
```



这不是你通常应该做的事，记得我说过你可以违背 `const` 承诺，上面说的就是一种违背承诺的方法。然而如果你在这种情况下尝试这么做，你可以看到我们声明 `MAX_AGE` 是一个常量，很有可能编译器会把它当做一个可读的常量。如果你试着做逆向引用 `dereference`，然后写入，你可能会程序崩溃，但硬要这样搞，也是可以工作的：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210707225513300.png)



可以看到打印了90，因为我们在这里做的是重新分配了指针指向。我们可以改变指针的内容，也就是指针指向的内存的内容；另外我们也可以改变指针指向的地址。

现在我们开始添加 `const` 变成 `const int*`，这意味着您不能修改该指针指向的内容：

```diff
#include <iostream>

int main(){
    const int MAX_AGE = 90;

+   const int* a = new int;
    *a = 2;
    a = (int*)&MAX_AGE;

    std::cout << *a << std::endl;
    std::cin.get();
}
```

 ![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210707230301833.png)



当我想逆向引用（指针的 `*` 运算符通常被称为 derefere nce 运算符，某些翻译叫做逆向引用）这个指针改变 `a` 值的时候，你可以看到这是不行的，`a` 的值是实际内存地址上的内容。

我们也可以注意到当我尝试改变 `a` 本身时，我没有得到任何错误，所以如果我让 `a` 指向其他比如 `MAX_AGE` 时是没有问题的，我只是不能改变那个指针指向的内容，也就是指针指向的内存中的数据。



使用 `const` 的第二种方法是把它放在 `*` 号之后：

```c++
int* const a = new int; 
```



它的作用正好相反，我可以改变指针指向的内容，但我不能把实际的指针本身重新赋值，指向别的东西。如果你把 `const` 放在这里，让指针本身成为常量，不能重新分配指针指向。

确保你记住这个，因为有时你会看到不同编程风格的人使用 `int const*`，但要知道它和 `const int*` 是完全一样的，但如果你搞成 `int* const`，那就完成不同了：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210707232301503.png)



我不能重新给 `a` 赋值，但我可以改变指针指向的内容。



最后我可以写2个 `const`，像这样：

```c++
const int* const a = new int;
```



这意味着我不能改变指针指向的内容，也不能改变这个指针本身。

这是 `const` 的第二个用法，当你处理指针时，可以是指针本身，或者指针指向的内容，当你把 `const` 放在声明的某处，不管它是在 `*` 号的左边或是前面，还是在 `*` 号之后，它有不同的含义。



#### 类与方法

最后我要讲的关于 `const` 的含义，是在类中以及方法中使用 `const`，让我快速写个类：

```c++
class Entity {
private:
    int m_X, m_Y;

public:
    int getX() const { return m_X; }
};
```



这个类有两个变量，我们通过 `getter` 和 `setter` 的方式初始化。我把 `const` 放在方法名的右边，参数列表之后，这就是第三种用法，它与变量无关，而是在方法名之后，顺便一说，这只在类中有效。

这意味着这个方法不会修改任何实际的类，因此你可以看到我不能修改类成员变量。如果我尝试让 `m_X = 2`，可以看到是做不到的 ：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210708161240526.png)



我已经承诺，这个方法不会修改实际的类，只能读不能写。所以在 `getter` 方法之后写 `const` 是有意义的，然而如果是 `setter` 方法，我不能在这里声明 `const`，因为显然我要写这个类：

```c++
void setX(int x) const {
		m_X = x;
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210708161619698.png)





当然，如果 `m_X` 是一个指针，你想让它保持不变，你可以写成这样：

```diff
class Entity {
private:
+   int* m_X, m_Y;

public:
+   const int* const getX() const {
        return m_X;
    }
};
```



我们一行写了三个 `const`，这意味着我们返回了一个不能被修改的指针（第一个 `const`），指针的内容也不能被修改（第二个 `const`），这个方法承诺不修改实际的 `Entity` 类（第三个 `const`）。

让我们回到普通不是指针的情况，问题是为什么我要声明这个东西是常量？是的，我得到一种承诺不要修改这个函数里的东西，然而这是否真的强制了什么东西吗？

答案是是的。如果我们在主函数中有 `Entity` 实例，然后我有一个 `printEntity()` 函数可访问我的 `getter` 方法：

```c++
#include <iostream>

class Entity {
private:
    int m_X, m_Y;

public:
    int getX() const {
        return m_X;
    }
};

void printEntity(Entity e) {
    std::cout << e.getX() << std::endl;
}

int main(){
    Entity e;
    
    std::cin.get();
}
```



现在我们有一个很合理的函数，但我希望能够通过常量引用传递这个，因为我不想再次复制 `Entity` 类，这需要分配空间。所以我要通过常量引用的方式：

```diff
+void printEntity(const Entity& e) {
    std::cout << e.getX() << std::endl;
}
```



现在有件事，如果我通过常量引用来传递参数，这意味着这个 `e` 是常量，我不能修改 `e`，不能将它重新赋值，这与指针的工作方式不同。如果你重新分配这个引用，你实际是在改变这个对象，而不是其他对象。

所以如果我把这个 `const` 从 `getX()` 方法中移走，突然间我就不能调用 `getX()` 函数了，因为它已经不能保证它不会写入 `Entity` 了：

```diff
#include <iostream>

class Entity {
private:
    int m_X, m_Y;

public:
+   int getX() {
        return m_X;
    }
};

void printEntity(const Entity& e) {
    std::cout << e.getX() << std::endl;
}

int main(){
    Entity e;
    printEntity(e);

    std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210708163425569.png)



我没有直接修改 `Entity`，然而我调用了一个可能可以修改 `Entity` 的方法，这是不被允许的，所以这里 `getX()` 函数的 `const` 是必须的。

记住，如果你的方法实际上没有修改类或不应该修改类时标记它们为 `const`，否则在有常量引用或类似的情况下就用不了你的方法。

在某些情况下你确实要标记方法为 `const`，但由于某些原因，它又确实需要修改一些变量。这里我新建一个 `var`，我们需要修改它：

```diff
class Entity {
private:
    int m_X, m_Y;
+   int var;

public:
    int getX() const {
+       var = 2;
        return m_X;
    }
};
```



也许只是为了调试或者它不会真正影响程序，我们仍然想标记这个方法为 `const`。在 C++ 中有一个关键词 `mutable`，这个词意味着它是可以被改变的：

```diff
class Entity {
private:
    int m_X, m_Y;
+   mutable int var;

public:
    int getX() const {
        var = 2;
        return m_X;
    }
};
```



#### mutable

`mutable` 实际上有两种不同的用途，其中之一是与 `const` 一起使用；另一种是用在 lambda 表达式中。这两种情况实际上是不同的，英文单词 `mutable` 意味着它是很容易改变的东西，它是可以改变的。你可能之前听过不可改变 `immutable`，意为某事无法改变，`mutable` 是它的反义词，是可以改变的。

##### const

所以当我们在常量 `const` 的背景下谈论可变 `mutable` 时，很明显我们谈论的是某种 `const` 但它实际上又可以改变，这就像 `mutable` 翻转了 `const` 的意思。我们有一个应用了 `mutable` 的程序，来看一看：

```c++
#include <iostream>
#include <string>

class Entity {
private:
    std::string name;
public:
    const std::string& getName() const {
        return name;
    }
};

int main(){

    std::cin.get();
}
```



我们创建了一个 `Entity` 的类，有一个私有成员 `name` 和一个 `getter` 函数返回 `name`。这里的 `const` 意味着我们不允许修改实际的类成员，所以我不能把 `name` 重新赋值为别的东西。

让方法为 `const` 的主要原因是承诺不会改变类，如果我们有一个常量的 `Entity` 对象，我们应该可以调用 `const` 方法，而如果没有标记就不行了。

然而在某些情况下我们还是想将方法标记为 `const`，因为无论如何它的目的都是不变的，它本质上没有修改对象本身，但它可能需要触及/修改某个变量。在 `Entity` 类中，从技术上讲是有可能的，但没人真的想要这样修改类的对象。

假设为了调试，我们想计算一下这个函数在程序中被调用了多少次，声明一个 `count` 用于计数，每次我们调用 `getName()` 这个函数就增加这个计数：

```diff
class Entity {
private:
+   int count = 0;
    std::string name;

public:
    const std::string& getName() const {
+       count++;
        return name;
    }
};
```



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210708174020025.png)



可以看到现在我们不能这样做，解决方法是去掉 `const`。但是可以看到在主函数中又不能调用了：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210708174450408.png)



这个 `getter` 方法应该是 `const` 的，所以不能做累加操作。当然我们可以把 `count` 移到其他类中或者什么地方，但是会很混乱，因为这个参数在这个类中是用在这个函数中的。

我们能做的就是恢复 `const`，然后标记这个 `count` 为 `mutable`：

```diff
#include <iostream>
#include <string>

class Entity {
private:
+   mutable int count = 0;
    std::string name;

public:
+   const std::string& getName() const {
        count++;
        return name;
    }
};

int main(){
    const Entity e;
    e.getName();

    std::cin.get();
}
```



现在一切ok了，我们有了一个很好的 `const` 方法，可以修改这个特定的成员变量。所以，标记类成员为 `mutable`意味着类中的 `const` 方法可以修改这个成员。这种用法也是 `mutable` 最常见的用法，老实说，在类成员中使用 `mutable` 可能是你唯一会使用到它的情况了。



##### lambda

但是，还有一个用到 `mutable` 的地方，就是 lambda。我不会把这个讲的太复杂，因为我们还没有讲到这方面的知识。这里的变量 `x = 8`，然后我想声明某种 lambda，所以我就叫它 `f`：

```c++
int main(){
    int x = 8;
    auto f = []() {
        std::cout << "Hello World!" << std::endl;
    };
    f();

    std::cin.get();
}
```



这就是一个 lambda 式子。lambda 基本上就像一个一次性的小函数，你可以写出来并赋值给一个变量，我们可以像调用其他函数一样调用它，就像这样使用它的名字，然后指定任何参数。

现在假设我们想在这里使用变量 `x`，不打印 `Hello World!` 了，变成打印 `x`：

```diff
int main(){
    int x = 8;
    auto f = []() {
+       std::cout << x << std::endl;
    };
    f();

    std::cin.get();
}
```



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210708211722202.png)



我需要定义一些捕获方法，我们可以像这样通过引用发送这个变量：

```c++
auto f = [&x]() {
		std::cout << x << std::endl;
};
```



或者这样直接传值：

```c++
auto f = [x]() {
		std::cout << x << std::endl;
};
```



或者通过 `=` 号对所有变量进行传值传递：

```c++
auto f = [=]() {
		std::cout << x << std::endl;
};
```





或者通过引用符号 `&` 对所有的变量进行引用传递：

```c++
auto f = [&]() {
		std::cout << x << std::endl;
};
```





假设这个 lambda 式子搞点额外的东西比如 `x++`，我们还是想按值来传递，会得到错误：

```diff
auto f = [=]() {
+		x++;
		std::cout << x << std::endl;
};
f();
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210708212609375.png)



在这种情况下，我实际上需要做的是搞另外一个变量，赋值给它，然后修改这个变量：

```diff
auto f = [=]() {
+		int y = x;
+		y++;
		std::cout << x << std::endl;
};
f();
```



相当于复制：创建一个局部变量，然后将 `x` 赋值给它。这有点乱，所以我要做的就是用 `mutable` 关键字：

```diff
int main(){
    const Entity e;
    e.getName();

    int x = 8;
+   auto f = [=]() mutable {
        x++;
        std::cout << x << std::endl;
    };
    f();

    std::cin.get();
}
```



这意味着你通过值传递的变量，这里做的实际上和刚才的 `y` 局部变量一样，只是在源码上看起来会干净很多。当然，在这个函数之外 `x` 的值仍然是8，它不会增加为9，因为你不是通过引用来传递它的。
