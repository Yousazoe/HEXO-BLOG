---
title: 面向对象设计
comment: false
tags: Cpp
categories: Cherno的C++笔记 (Cherno C++)
abbrlink: f28a8c2c
date: 2021-06-09 08:57:47
type:
banner_img:
index_img:
translate_title:
top:
mathjax:
---

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/cf34c4102453055.5f467520af6a5.png)

<div align=center>
  <font size="3">
    <i>
      <a href="https://www.behance.net/gallery/102453055/Tiny-Rooms">Tiny Rooms</a> by 
      <a href="https://www.behance.net/MChahin">Mohamed Chahin</a>
    </i>
  </font>
</div>

### 引言

这个系列将讲解C++需知道的一切内容，涵盖这门语言的基础知识。本节将开始讲解C++的面向对象特性。

<!--more-->



### 类

我们终于讲到了面向对象编程，这是一种非常流行的编程方式，但实际上只是一种你编写代码的一种方式，其他语言诸如C#、Java主要是面向对象的语言。事实上，用这些语言你不能写任何其他类型的代码，虽然你也可以尝试，最终这些语言都是面向对象的语言。

然而C++有点不同，因为它并没有给你强加一种特定风格。例如用C语言不支持面向对象编程，因为为了面向对象编程你需要有一些概念比如类和对象，这些东西C语言没有，而C++会添加所有这些功能，在某种程度上，使用面向对象总是一个好主意。



简单的说，类只是数据和功能组合在一起的一种方法。例如在游戏中我们可能想要一些代表角色的东西，那么我们需要什么样的东西来代表一个角色呢？我们当然需要一些数据，例如角色在游戏中的位置、角色可能拥有的某些属性比如角色移动的速度，我们还可能需要一些3D模型代表角色的屏幕形象，所有这些数据都需要存储在某个地方。

我们可以为所有这些创建变量，假设我们想要创建一个角色比如位置、速度：

````c++
#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main(){
    int x,y;
    int spped = 2;
    
    std::cin.get();
}
````



现在你可能发现这有点乱了，事实上这些名字太普通了，当我们游戏有两个角色时不得不复制然后改成`playerX0`、`playerX1`等：

```c++
#include <iostream>

#define LOG(x) std::cout << x << std::endl

int main(){
    int playerX0,playerY0;
    int playerSpped0 = 2;

    int playerX1,playerY1;
    int playerSpped1 = 2;
    
    std::cin.get();
}
```



你当然可以使用数组，但重点还是一样的：它们只是一堆没有组合在一起的变量，它们是无组织的放在我们的代码中，这不是一个好主意。另一个很好的例子可以说明为什么这很烦人，如果我想写一个函数来移动角色，我需要把这三个参数都指定为整数参数：

```c++
void Move(int x,int y,int spped){
	......
}
```



所有这一切变成了如此多的代码，难以维护且非常混乱。所以我们要做的是通过使用类简化它，我们可以创建一个叫做`Player`类，它包含了所有我们想要的数据变成一种类型：

```c++
class Player{
    int x,y;
    int speed;
};
```



我们通过使用`class`然后给它一个名字来实现，这个名字必须是唯一的，因为`class`是类型，这里是创建一个新的变量类型。

现在我们又了一个全新的类`Player`，本质上它是一种类型，如果我们开始使用`Player`类可以把它当作其他变量来创建：

```c++
int main(){
		Player player;
    std::cin.get();
}
```



由类类型构成的变量称为对象，新的对象变量称为实例，在这里我们实例化了一个`Player`对象，如果我想设置这些变量可以简单写为`player.+x`：

```c++
player.x = 5;
```



但这里会提示出错，原因是`Player`中这些成员变量都是私有的：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210609093343389.png)



这是可见性的原因，当你创建一个新类时你可以选择制定类中的内容的可见性。默认情况下，一个类中所有东西都是私有的，这意味着只有类中的函数才能访问这些变量，然而我们希望能够从`main`函数中访问这些变量，所以在这里把它设为`public`：意味着我们可以在类之外的任何地方访问这些变量：

```c++
#include <iostream>

#define LOG(x) std::cout << x << std::endl

class Player{
public:    
    int x,y;
    int speed;
};

int main(){
    Player player;
    player.x = 5;

    std::cin.get();
}
```



编译成功，现在我们实现了第一个目标：把所有的变量都放在了一个地方，这些变量集合可以代表一个`player`，所以我们把它很好的分组了。

现在我们有了这些数据，假设我们想让`player`做一些事情例如移动，需要写一个函数来改变`x`和`y`变量值，我们该怎么做呢？

```c++
#include <iostream>

#define LOG(x) std::cout << x << std::endl

class Player{
public:
    int x,y;
    int speed;
};

void Move(Player& player,int xa,int ya){
    player.x += player.speed * xa;
    player.y += player.speed * ya;
}

int main(){
    Player player;
    player.x = 5;
    Move(player,1,-1);

    std::cin.get();
}
```



我们已经写了一个可以移动`player`的函数，然而我们可以做的更好一点。类实际上可以包含函数，这意味着我们可以将`move`函数移动到类中，类中的函数被称为方法：

```c++
#include <iostream>

#define LOG(x) std::cout << x << std::endl

class Player{
public:
    int x,y;
    int speed;
  
    void Move(int xa,int ya){
      x += speed * xa;
      y += speed * ya;
    }
};



int main(){
    Player player;
    player.x = 5;
    player.Move(1,-1);

    std::cin.get();
}
```



现在函数在类里面了，我们可以直接得到这些变量而不需要传入`player`对象，所有的`x`、`y`和`speed`指的就是当前对象的变量。

我们已经简化了我们的代码，每个`Player`对象都有自己的`move`函数，当我们为指定的`Player`对象调用`move`时这个对象将会移动。这与`Player`类之外的`move`函数没有什么不同，它所做的就是让我们的代码更干净，这样看起来更好看，而当你处理很多代码时，这是一个巨大的优势。

这就是类的基本概念，允许我们将变量分组到一个类型中并为这些变量添加功能。如果你再看一下代码，我们真正做的是我们在一个类类型中定义了三个变量以及一个处理这些变量的函数，这就是我们所做的。类本质上只是语法糖，我们可以使用它来组织我们的代码，使它更容易维护。



#### 类与结构体对比

类和结构体有什么区别呢？上次我们讲到类的时候我们对类有了一些基本的介绍，结构体`struct`（structure的缩写）以及类`class`看起来有点相似，很多人有点困惑到底区别是什么。

事实是基本没有什么区别，只有一个关于可见度的小区别。一个类的成员默认为`private`，这意味着如果我没有加`public`之前的代码会报错，告诉我们`Player`类的`move`方法是不可访问的，因为它被标记为默认的`private`只有在类里面的方法才可以访问`move`方法。

这就是区别的本质所在，默认情况下类是私有的，所以如果你不指定修改任何可见性，那默认值就是私有的`private`。然而在结构体中，默认值却是`public`的。技术上讲，这是类与结构体的唯一区别，在代码中体现在把`class`换为`struct`：

```c++
#include <iostream>

#define LOG(x) std::cout << x << std::endl

struct Player{
    int x,y;
    int speed;

    void Move(int xa,int ya){
        x += speed * xa;
        y += speed * ya;
    }
};



int main(){
    Player player;
    player.x = 5;
    player.Move(1,-1);

    std::cin.get();
}
```





从技术上讲，它们可能没有太大的区别，然而实际发生的使用情况会有所不同。`struct`结构体在C++中继续存在的唯一原因是因为它希望与C保持向后兼容性，因为C代码没有类但有结构体，如果我们突然去掉整个结构体关键字会失去兼容性，C++编译器不知道什么是`struct`。

当然，你可以很容易解决这个问题，只需要用`#define`来查找，我们可以写一些类似`#define`的东西：

```c++
#define struct class
```

它要做的就是用`class`替换所有的`struct`，在这种情况下尽管这段代码看起来很简单，但如果我们编译它你会发现同样的编译错误，说`move`在类中，不能在外部访问它：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210610103012424.png)



这样做也许我们能得到C与C++的某种兼容性，因为理想情况下你应该能将C语言中的`struct`替换成`class`，然后将其变成`public`。所以语义上的不同以及人们如何看待它，或多或少取决于用法，如果没有区别，那什么时候使用`struct`或者类，如果我想要的所有的成员都是公共的，而又不想写`public`这个字，我应该使用结构体吗？

是的，它就是那么微不足道，人们都有自己对这两者的理解和定义，没有什么正确或错误的答案，这取决于你的编程风格。让我们谈谈我的编程风格，以及我可能在哪里使用什么类型。

当我讨论Plain old data（POD）时，我喜欢尽可能地使用`struct`，只表示变量的结构。这方面的一个很好的例子可能是数学上的向量类：

```c++
struct Vec2 {
    float x,y;
};
```



不管是`class`还是`struct`，都是代表这两个浮点数的一种结构，它不应该像之前的`Player`类一样包含大量的功能，`Player`类可能有一个3D模型，它可能会为这个3D模型处理渲染代码、如何在地图上移动并接受键盘输入......这里有很多功能，而我们的向量只是两个变量，我们把它分组只是为了让我们的代码更容易使用。

当然这不是说我不会在这里添加方法，其实完全可以。我可以添加一个名为`add`的方法，它取另一个`Vec2`作为参数，然后把它和当前向量相加：

```c++
struct Vec2 {
    float x,y;
    
    void Add(Vec2& other) {
        x += other.x;
        y += other.y;
    }
};
```



再次强调，我只是在处理这些变量。也许你会较真的说`Player`类不是也只是操纵这些变量吗？其实在设计上还是有一点不同的，因为我们讨论的东西要复杂的多。

另外的场景是继承，我不会在`struct`中使用继承。如果我要有一个完整的类层次结构或者某种继承层次结构，我将使用类，因为继承是一种增加另一层次复杂性的东西，我只希望我的结构体是数据的结构，仅此而已。除此之外如果你尝试混合使用这些类型，例如你有一个类`a`和一个结构体`b`，这个`b`继承自`a`，某些编译器会报错。

在这里我使用结构体而不是类的原因是如果我只是想用结构体表示一些数据，我将使用一个结构体；但如果我想要一个大量功能的整个类比如一个游戏世界或者一个Player亦或是其他可能需要继承的东西，我将使用一个类，这也是我个人区分这两种类型的方法。



#### 如何写一个C++的类

到目前为止我们学了类，并尝试着从头开始写一个类。今天我们会写一个基本的`log`类演示我们已经学过的东西。

让我们来讨论一下我们要写的这个`log`类，这个`log`类到底是什么？它是我们管理日志信息的一种方式，换句话说我们想要我们的程序打印消息或信息到控制台，这通常用于调试，非常有帮助。在游戏或应用中，如果你想知道发生了什么，你只需要将事物的状态打印到控制台，因为应用程序中的控制台就像一个放信息的地方，我们可以用它来打印出发生了什么，保证代码在正确的工作。

如果我们的游戏中有一个图形要显示在控制台或是一些不同的东西，它可能不会一直起作用，如果我们的图形渲染系统出现了问题我们可能得不到那些信息。然而控制台是操作系统内置的最基本的东西，所以我们可以保证它总是有效的。有些复杂的日志系统有几千行代码，只是为了把东西打印到控制台，但它对调试和开发非常重要，所以花时间在上面是绝对值得的。

`log`日志系统不仅可以打印到控制台，也可以用不同的颜色打印，或是通过网络输出日志消息到一个文件，你可以做很多事情。但`log`类开始的时候非常简单，它提供向控制台写入文本的能力、保持我们真正想要发送给控制台的日志信息的级别，开始我们有三个级别：

+ 错误
+ 警告
+ 信息

我们能做的是把日志系统级别设置为“警告”，这意味着只会打印警告和错误，而不会打印信息。这很有用，如果你不想看到一堆信息，你只是想知道哪里出了问题或警告是什么。同样通过过滤实际发送和打印的内容，控制台也会很清爽，让我们来看看它会是什么样子：

```c++
#include <iostream>

class Log {
    
};

int main(){

    std::cin.get();
}
```



现在让我们思考一下`log`类是如何工作的。创建一个类或设计API时，一个很好的方法是通过研究它的使用情况：

```c++
#include <iostream>

class Log {

};

int main(){
    Log log;
    log.SetLevel(LogLevelWarning);
    log.Warn("Hello!");

    std::cin.get();
}
```



首先我要实例化它，然后肯定会有一个设置`log`级别的`SetLevel`方法，意味着只有警告或更重要的信息比如警告或错误才会被打印出来。然后我可能想要打印一个警告符号，里面填点"Hello"这样的。

现在我知道了我的`log`类看起来像什么了，我可以直接回去开始填空：

```c++
#include <iostream>

class Log {
private:
    int m_LogLevel;
public:
    void SetLevel(int level){
        m_LogLevel = level;
    }

    void Warn(const char* message){

    }
};

int main(){
    Log log;
    log.SetLevel(1);
    log.Warn("Hello");

    std::cin.get();
}
```



其中设置日志级别这里的1很难让人理解，1是什么？因此我们需要创建一个变量，它的值是1，来表示我们想要表示的东西。我们给它起名为`LogLevelWarning`，完善三种类型的日志消息常数：

```diff
class Log {
public:
+   const int LogLevelError = 0;
+   const int LogLevelWarning = 1;
+   const int LogLevelInfo = 2;
private:
    int m_LogLevel = LogLevelInfo;
public:
    void SetLevel(int level){
        m_LogLevel = level;
    }

    void Warn(const char* message){
    
    }
};
```



我们有错误`Error`，警告`Warning`还有信息`Information`。默认情况下，我把我的日志级别设置为`LogLevelInfo`，意味着所有的东西都应该打印出来。最后我们补充`Warn`函数，把东西打印到控制台上，以此类推补充其余两种函数：

```c++
class Log {
public:
    const int LogLevelError = 0;
    const int LogLevelWarning = 1;
    const int LogLevelInfo = 2;
private:
    int m_LogLevel = LogLevelInfo;
public:
    void SetLevel(int level){
        m_LogLevel = level;
    }

    void Error(const char* message){
        std::cout << "[ERROR]: " << message << std::endl;
    }
    
    void Warn(const char* message){
        std::cout << "[WARNING]: " << message << std::endl;
    }

    void Info(const char* message){
        std::cout << "[INFO]: " << message << std::endl;
    }
};
```



这样我们就有了设置日志级别的方法，但目前我们还不能做到如果日志级别设置为`warning`就不打印所有的`info`信息，我们可以用条件语句来搞定：

```diff
#include <iostream>

class Log {
public:
    const int LogLevelError = 0;
    const int LogLevelWarning = 1;
    const int LogLevelInfo = 2;
private:
    int m_LogLevel = LogLevelInfo;
public:
    void SetLevel(int level){
        m_LogLevel = level;
    }

    void Error(const char* message){
+       if (m_LogLevel >= LogLevelError)
            std::cout << "[ERROR]: " << message << std::endl;
    }

    void Warn(const char* message){
+       if (m_LogLevel >= LogLevelWarning)
            std::cout << "[WARNING]: " << message << std::endl;
    }

    void Info(const char* message){
+       if (m_LogLevel >= LogLevelInfo)
            std::cout << "[INFO]: " << message << std::endl;
    }
};

int main(){
    Log log;
+   log.SetLevel(log.LogLevelWarning);
    log.Warn("Hello");

    std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210610212904211.png)



```diff

int main(){
    Log log;
    log.SetLevel(log.LogLevelWarning);
    log.Warn("Hello");
+   log.Error("Hello");
+   log.Info("Hello");

    std::cin.get();
}
```



这里我们打印三条不同的日志信息，但只有`warning`和`error`被打印出来，`info`没有：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210614025735750.png)



因为我们设定的级别为`warning`，去掉就会打印三个信息。这个类有很多问题，但它是简单的，而且很有逻辑。当一个人考虑如何编写这个类时，一个经验丰富的程序员是不会这样写的，它给了我一个很好的机会向你们展示如何使用一些不同的概念来改进这个类。



### 静态

#### 类/结构体外的静态

今天我们将讨论C++中的静态`static`。`static`关键字在C++中有两个意思，这取决于上下文，其中之一是在类或结构体外部使用`static`关键字；另一种是在类或结构体内部使用`static`。直白的说，类外面的`static`意味着链接将只是在内部，它只能对你定义的翻译单元可见。

然而类或结构体内部的静态变量意味着该变量实际上将与类的所有实例共享内存，在你在类中创建的所有实例中静态变量只有一个实例。类似的事情也适用于类中的静态方法，在类中，没有实例会传递给该方法，在这里我们不深入讨论静态`static`在类或结构体范围内的实际含义，今天我们关注在类和结构体外部的静态。

回到代码，在一个新建的`static.cpp`，我要做的就是定义一个静态变量：

```c++
static int s_variable = 5;
```



它和其他变量一样，但在前面是`static`关键字。它的意思是这个变量只会在这个翻译单元内部链接，静态变量或函数意味着，当需要将这些函数或变量与实际定义的符号链接时链接器不会在这个翻译单元的作用域之外，寻找那个符号的定义。

最好还是看例子，这里我们创建了一个静态变量`s_variable`并将它设为5，然后在另一个C++文件（也就是另一个翻译单元）声明同名的变量，编译不会有任何问题：

```c++
#include <iostream>

int s_variable = 10;

int main(){

    std::cout << s_variable << std::endl;

    std::cin.get();
}
```



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210618083556637.png)



假如我回到`static.cpp`文件删除`static`关键字，再次编译运行会得到一个链接错误：

```c++
#include <iostream>

int s_variable = 10;

int main(){

    std::cout << s_variable << std::endl;

    std::cin.get();
}
```



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210618083754174.png)



这是因为这个`s_variable`已经在另一个翻译单元中定义了，所以我们不能有两个同名的全局变量。

一种修改方法是修改这个变量的实际指向，标识这个变量为`extern`，这意味着它会在外部翻译单元中寻找`s_variable`变量，这被称为`external linking`：

```c++
#include <iostream>

extern int s_variable;

int main(){

    std::cout << s_variable << std::endl;

    std::cin.get();
}
```



如果我现在运行代码打印出来的是5，因为它引用了`static.cpp`中的`s_variable`变量：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210618084357358.png)





然而如果我在`static.cpp`标记为静态变量，这有点像在类中声明一个私有变量，其他所有的翻译单元都不能看到这个`s_variable`变量。链接器在全局作用域下，将不会看到这个变量，也就是说此时我们尝试编译代码，我们得到一个未解析的外部符号错误，它在任何地方都找不到名称为`s_variable`的整型变量：

```c++
static int s_variable = 5;
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210618085312201.png)



这是因为我们已经有效地标记了这个变量是私有的。回到`static.cpp`，和之前一样声明一个函数`Function`：

```diff
static int s_variable = 5;

+void Function() {
+    
+};
```



在`main.cpp`我们声明一个同样签名的函数：

```diff
#include <iostream>

-extern int s_variable;

+void Function() {
+
+}

int main(){
-   std::cout << s_variable << std::endl;
    std::cin.get();
}
```



此时我们尝试编译，会在链接阶段得到一个重复符号的错误，因为有两个`Function`函数：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210618090417145.png)



如果我把`static.cpp`标记为静态，当链接器开始链接时它根本不会看到这个静态函数，所以我不会得到任何错误：

```diff
static int s_variable = 5;

+static void Function() {
    
};
```



这就是C++中静态的全部含义，当你在类和结构体之外使用静态时，它意味着当你声明静态函数或静态变量时它只会在被它声明的C++文件中被“看到”。

如果你想在头文件中声明一个静态变量并将该头文件包含在两个不同的C++文件中，你所做的就是和之前我所做的一样：在两个翻译单元中都声明了相同的`s_variable`变量为静态变量，因为当你包含那个头文件时它会复制所有内容并将其粘贴到C++文件中，你所做的是将一个静态变量放到两个不同的翻译单元中。

至于你为什么要用`static`，考虑一下为什么要在类中使用`private`？如果你不需要变量是全局变量，你就需要尽可能多地使用静态变量，因为一旦你在全局作用域下声明东西的时候，如果没有设定为`static`，那么链接器会跨编译单元进行链接，这意味着你已经创建了一个全局的变量，这可能会导致一些非常糟糕的bug。

归根到底，全局变量是不好的，但重点是要让函数和变量标记为静态的，除非你真的需要它们跨翻译单元链接。





#### 类/结构体中的静态

上次我们讨论了C++中的`static`关键字以及它在类或结构体之外的意义，今天我们讨论类或结构体中的静态。

如果它在一个类或一个结构体中，`static`到底是什么？在几乎所有面向对象的语言中静态在一个类中意味着特殊的东西，如果你把它和变量一起使用，意味着在类的所有实例中，这个变量只有一个实例。如果我创建一个名为`Entity`的类，不断创建`Entity`实例，我仍然只会得到那个变量的一个版本：意思是如果某个实例改变了这个静态变量，它会在所有实例中反映这个变化，这是因为尽管我已经创建了一大堆类的实例，只有一个变量。

正因如此，通过类实例来引用静态变量是没有意义的，因为这就像类的全局实例。静态方法也是一样，不需要通过类的实例就可以被调用，而在静态方法的内部你不能写引用到类实例的代码，因为你不能引用到类的实例。让我们来看些例子：

```c++
#include <iostream>

struct Entity {
    int x;
    int y;
    
    void Print() {
        std::cout << x << "," << y << std::endl;
    }
};

int main(){
    Entity e;
    e.x = 2;
    e.y = 3;

    Entity e1 {5,8};
    
    e.Print();
    e1.Print();
    std::cin.get();
}
```



在这里我写了一个`Entity`的结构体，包含两个整数`x`、`y`（这里我使用结构体，你也可以使用类。这里我选择结构体的原因是希望变量是`public`）。然后我们给`Entity`结构体一个函数`print`打印。

打印`e`和`e1`，我们应该得到2，3和5，8:

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210619082513364.png)



如果我让变量是静态的，事情就会改变。如果我来到这里把`x`和`y`变成静态的，这里的初始化就会失败，因为`x`和`y`不再是类成员：

```diff
#include <iostream>

struct Entity {
+   static int x;
+   static int y;

    void Print() {
        std::cout << x << "," << y << std::endl;
    }
};

int main(){
    Entity e;
    e.x = 2;
    e.y = 3;

-   Entity e1 {5,8};
+   Entity e1;
+   e1.x = 5;
+   e1.y = 8;

    e.Print();
    e1.Print();
    std::cin.get();
}
```



可以看到我们引用了两个不同的实例，此时编译代码会报错，因为我们实际上需要在某个地方定义那些静态变量：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210619083147989.png)



我们可以这样做，先写作用域`Entity`，再写变量名`x`：

```diff
#include <iostream>

struct Entity {
    static int x;
    static int y;

    void Print() {
        std::cout << x << "," << y << std::endl;
    }
};

+int Entity::x;
+int Entity::y;

int main(){
    Entity e;
    e.x = 2;
    e.y = 3;

    Entity e1;
    e1.x = 5;
    e1.y = 8;

    e.Print();
    e1.Print();
    std::cin.get();
}
```



编译代码，你会看到我们实际上打印了两次5，8：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210619083611316.png)



这有点奇怪，因为在代码中第一个实例我们设定了2和3，第二个才是5和8。记住当我们让`x`和`y`变量为静态时，所有的`Entity`实例中只有一个这些变量的实例，这意味当我改变第二个`Entity`实例的`x`和`y`时它们实际上和第一个完全一致，它们指向的是相同的内存，两个不同的`Entity`实例它们的`x`和`y`指向同一个地方。

我们之前这样引用是没啥意义的，可以这样引用它们：

```diff
-e1.x = 5;
-e1.y = 8;

+Entity::x = 5;
+Entity::y = 8;
```





这就像我们在名为`Entity`的命名空间中创建了两个变量，它们实际上并不属于类。从这个意义上说，它们可以是`private`的，也可以是`public`的，它们仍然是类的一部分而不是命名空间。但无论出于何种目的，它们其实和在命名空间中一样，当你创建一个新的类的实例或者类似的东西时它们与任何分配无关。

我们重写一下代码：

```c++
#include <iostream>

struct Entity {
    static int x;
    static int y;

    void Print() {
        std::cout << x << "," << y << std::endl;
    }
};

int Entity::x;
int Entity::y;

int main(){
    Entity e;
    Entity::x = 2;
    Entity::y = 3;

    Entity e1;
    Entity::x = 5;
    Entity::y = 8;

    e.Print();
    e1.Print();
    std::cin.get();
}
```



可以看到这些都没啥意义了。这也解释了为什么之前我们得到两个5和8，因为我们实际上在修改相同的变量。

这当然很有用，在你想要跨类使用变量时可以创建一个全局变量，或者不使用全局变量而是使用一个静态全局变量，它是在内部进行链接的，它不会在你的整个项目中是全局的，这样做会有同样的效果，那你为什么要在类中使用静态呢？

答案是把它们放在`Entity`中是有意义的，如果你有东西比如一条信息，你想要在所有的`Entity`实例之间共享数据或将它实际存储在`Entity`类中是有意义的，因为它与`Entity`有关。要组织好代码，你最好在这个类中创建一个静态变量而不是一些静态或全局的东西到处乱放。

静态方法的工作方式与此类似。如果我让这个`Print`方法变成静态，它会正常工作，因为你可以看到它指向的`x`和`y`它们也是静态变量，所以我们的调用方式也可以换一下：

```diff
-e.Print();

+Entity::Print();
```



这是正确的调用方式。你也可以注意到，它会打印出相同的东西，因为我们运行了两次相同的方法，在这个例子中我们甚至根本不需要类实例：

```c++
#include <iostream>

struct Entity {
    static int x;
    static int y;

    static void Print() {
        std::cout << x << "," << y << std::endl;
    }
};

int Entity::x;
int Entity::y;

int main(){
    Entity::x = 2;
    Entity::y = 3;

    Entity::x = 5;
    Entity::y = 8;

    Entity::Print();
    Entity::Print();
    std::cin.get();
}
```



如果我们决定让`x`和`y`是非静态的，事情就变了。`Print`方法仍然保持`static`，但静态方法不能访问非静态变量，就是这样简单的原因。有些人可能会对静态的东西能访问什么非静态的东西感到困惑，它真的一点也不令人困惑。

返回我们的`Entity`实例重写代码：

```c++
#include <iostream>

struct Entity {
    int x;
    int y;

    static void Print() {
        std::cout << x << "," << y << std::endl;
    }
};


int main(){
    Entity e;
    e.x = 2;
    e.y = 3;

    Entity e1;
    e1.x = 5;
    e1.y = 8;

    Entity::Print();
    Entity::Print();
    std::cin.get();
}
```



这样我们实际上对于`Entity`类的每个实例都有一个单独的`x`和`y`，但`Print`方法仍然保持静态。此时编译代码，我们会得到一个错误，可以看到是“非法引用非静态成员”：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210619093455626.png)



因为你不能从静态方法访问它，原因是静态方法没有类实例。本质上，你在类中写的每一个非静态方法总是获得当前类的一个实例作为参数，这是类在幕后的实际工作方式。在类中你看不到这种东西，它们通过隐藏参数发挥作用，静态方法不会得到那个隐藏参数。

静态方法与在类外部编写方法相同，如果我在外面写一个`Print`方法，你就知道为什么不能访问`x`和`y`了：因为你不知道`x`、`y`是啥：

```c++
struct Entity {
    int x;
    int y;

    static void Print() {
        std::cout << x << "," << y << std::endl;
    }
};

static void Print(Entity e) {
    std::cout << e.x << "," << e.y << std::endl;
}

int main(){
		......
}
```



想象你有同样的`Print`方法，但有一个`Entity`对象作为参数传入。这个方法本质上是非静态类方法在编译时的真实样子，而去掉参数`Entity e`正是我们将`static`关键字添加到类方法时所做的，这就是为什么会报错：它不知道你想要访问哪个`Entity`的`x`和`y`，因为你没有给它一个`Entity`的引用。

`static`对于那些静态数据非常有用，这些数据不会在类实例之间发生变化，但实际上我们想要在类中使用它们。





#### 局部静态

在前面几节我们了解了`static`关键字在特定上下文中的含义，今天我们看一看局部作用域中的`static`关键字。你可以在局部作用域中使用`static`来声明一个变量，这和我们之前看到的两种`static`有点不同，这次的局部静态（local static）会有更多的含义，声明一个变量需要考虑两种情况：变量的生存期和变量的作用域。

生存期指的是变量实际存在的时间，换句话说就是在它被删除之前，它会在我们的内存中存在多久。而变量的作用域是指我们可以访问变量的范围，当然，如果在一个函数内部声明一个变量我们不能在其他函数中访问它，因为我们声明的变量对于我们声明的函数是局部的。

静态局部（local static）变量允许我们声明一个变量，它的生存期基本上相当于整个程序的生存期，然而它的作用域被限制在这个函数内，但它其实和函数没有什么关系，我的意思是你可以在任何作用域中声明这个，刚才只是用函数举个例子，这并不仅仅局限在函数内部，也可以在`if`语句中，也可以在任何位置。

这就是为什么函数作用域中的`static`和类作用域中的`static`之间没有太大的区别，因为生存期实际上是相同的，唯一的区别是在类作用域中，类的任何东西都可以访问它（这个静态变量）；如果你在函数作用域中声明一个静态变量，那么它将是那个函数的局部变量，对类来说也是局部变量。

让我们来看一些例子。最简单的例子就是创建一个函数，然后在其中声明一些静态变量：

```c++
#include <iostream>

void Function() {
    static int i = 0;
}

int main(){
    
    std::cin.get();
}
```



这意味着当我第一次调用函数时，这个变量将被初始化为0，然后所有对函数的后续调用实际上不会创建一个全新的变量。

检验这个最简单的方法是如果我打印`i`的值，然后每次调用函数时都增加`i`的值。如果我们暂时把`static`关键字去掉然后运行程序：



```c++
#include <iostream>

void Function() {
    static int i = 0;
    i++;
    std::cout << i << std::endl;
}

int main(){
    for (int i = 0; i < 5; ++i) {
        Function();
    }
    std::cin.get();
}
```



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210619100918732.png)



运行程序，1被打印了五次。如果我们把`static`关键字加上，再次运行程序：

```diff
void Function() {
-   int i = 0;
+   static int i = 0;
    i++;
    std::cout << i << std::endl;
}
```





![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210619102541655.png)



这种写法也可以写成下面这样（无论`i`静态与否），得到的效果是一样的：

```c++
#include <iostream>

int i = 0;

void Function() {
    i++;
    std::cout << i << std::endl;
}

int main(){
    for (int i = 0; i < 5; ++i) {
        Function();
    }
    std::cin.get();
}
```



但这种方法的问题是我可以在任意地方访问`i`，这极大的改变了我们程序所做的事情。所以如果你想要做这些，但又不希望每个人都能访问这个变量，你可以在局部作用域下声明成`static`。

有些人不赞成使用这种方法，我不完全理解其中的原因，因为我不认为这有什么问题。它确实有它的用处，你可以使用其他方法实现完全相同的行为，比如可以使用类来实现，但你根本不必使用类来编写程序，局部静态确实让编程更轻松。

另一个例子是如果你有一个单例类（只存在一个实例的类），如果我想创建这个单例类而不使用静态局部作用域，我就需要创建静态的单例实例：

```c++
class Singleton {
private:
    static Singleton* s_Instance;
public:
    static Singleton& Get() {
        return *s_Instance;
    }
};

Singleton* Singleton::s_Instance = nullptr;
```



现在我有了单例类，我可以调用`Singleton::Get`对它做任何我想做的事情：

```c++
#include <iostream>

class Singleton {
private:
    static Singleton* s_Instance;
public:
    static Singleton& Get() {
        return *s_Instance;
    }

    void Hello(){}
};

Singleton* Singleton::s_Instance = nullptr;

int main(){
    Singleton::Get().Hello();
    std::cin.get();
}
```



一切搞定，我们得到了一个可以使用的类实例，你可以用静态方式来使用它，你不一定要这么做。

另一种方式是使用我们的新知识局部静态local static：

```c++
class Singleton {
public:
    static Singleton& Get() {
        static Singleton instance;
        return instance;
    }

    void Hello(){}
};
```



我们得到了完全相同的行为，运行代码没有问题，你可以看到我们的代码现在干净多了。



### 枚举

今天我们要讲的是C++的枚举。`enum`是enumeration的缩写，基本上它就是一个数据集合。如果你想要给枚举一个更实际的定义，他们是给一个值命名的一种方法，所以我们不用一堆叫做`a`、`b`、`c`的整数，我们可以有一个枚举数，它的值是`a`、`b`、`c`与整数对应。

它能帮助我们将一组数值集合作为类型，而不仅仅是用整型作为类型。当然，你可以给它赋值任何整数或者限制哪些值可以赋值。它只是一种命名值的方法，当你想要使用整数来表示某些状态或者某些数值时，它非常有用。不管怎么说，枚举数其实就是一个整数。

假设我有三个值想要处理，可能有一些代码来检查当前的`value`值是什么，然后执行某种操作：

```c++
#include <iostream>

int A = 0;
int B = 1;
int C = 2;

int main(){
    int value = B;
    if (value == B) {
        // Do something here
    }
    
    std::cin.get();
}
```



然而这段代码带来了一些问题。首先这些`A`、`B`、`C`根本没有分组，在代码后面的某个地方你可能会有一个`D`或者你可能想再次声明`A`，本质上最大的问题是这些根本没有分组。此外，它们只是整数，这意味着如果`int value = 5`下面的这些已经没有任何意义了。

我们希望本质上定义一个类型，只能是这三个数中的一种，而且能够把它们组合起来，这正是我们可以使用枚举的地方：

```c++
#include <iostream>

enum Example {
    A,B,C
};

int a = 0;
int b = 1;
int c = 2;

int main(){
    Example value = B;
    if (value == B) {
        // Do something here
    }

    std::cin.get();
}
```



如果你不按照默认来搞，你也可以指定这些变量的值。默认的第一个是0，然后它一个接一个地递增：

```c++
enum Example {
    A = 0,
    B = 2,
    C = 6
};
```



如果你从一个非零的数字开始比如5，并且并没有指定其余的值，它会默认是6和7。我们还可以做的一件事是，指定你想要给枚举赋值的整数类型，你可以写一个冒号后接数据类型，例如`unsigned char`：

```c++
enum Example : unsigned char {
    A = 5, B, C
};
```



枚举默认为32位整型，然而在这个例子中我们没有必要使用32位，我们可以使用8位的整数比如`unsigned char`减少内存的使用。你不能使用`float`，因为它不是整数，枚举必须是一个整数比如`char`。

这就是枚举的本质，它只是给特定的值命名的一种方式，这样你就不必在各种地方处理各种整数。让我们把枚举用在之前的日志里：

```c++
#include <iostream>

class Log {
public:
    const int LogLevelError = 0;
    const int LogLevelWarning = 1;
    const int LogLevelInfo = 2;
private:
    int m_LogLevel = LogLevelInfo;
public:
    void SetLevel(int level){
        m_LogLevel = level;
    }

    void Error(const char* message){
        if (m_LogLevel >= LogLevelError)
            std::cout << "[ERROR]: " << message << std::endl;
    }

    void Warn(const char* message){
        if (m_LogLevel >= LogLevelWarning)
            std::cout << "[WARNING]: " << message << std::endl;
    }

    void Info(const char* message){
        if (m_LogLevel >= LogLevelInfo)
            std::cout << "[INFO]: " << message << std::endl;
    }
};
```



我们在这里使用了三个不同的`Log`级别，而它们只是整数0、1、2，这是一个非常适合使用枚举的地方，因为我们有三个值，用它们作为整数来表示某个状态。这个例子中日志级别的意思是指会展示哪种级别的日志：

```diff
class Log {
public:
+   enum Level{
+       ERROR = 0,
+       WARNING = 1,
+       INFO = 2
+   };
    
-   const int LogLevelError = 0;
-   const int LogLevelWarning = 1;
-   const int LogLevelInfo = 2;
private:
-   int m_LogLevel = LogLevelInfo;
+   Level m_LogLevel = INFO;
public:
+   void SetLevel(Level level){
        m_LogLevel = level;
    }

    void Error(const char* message){
+       if (m_LogLevel >= ERROR)
            std::cout << "[ERROR]: " << message << std::endl;
    }

    void Warn(const char* message){
+       if (m_LogLevel >= WARNING)
            std::cout << "[WARNING]: " << message << std::endl;
    }

    void Info(const char* message){
+       if (m_LogLevel >= INFO)
            std::cout << "[INFO]: " << message << std::endl;
    }
};

int main(){
    Log log;
+   log.SetLevel(Log::ERROR);
    log.Warn("Hello!");
    log.Error("Hello!");
    log.Info("Hello!");
}
```



注意这个枚举`Level`本身不是一个命名空间，这叫做枚举类。然而对于普通的枚举而言，这个`Level`并不是真正的命名空间，所以你不能把它当作一个命名空间，这意味着`ERROR`、`WARNING`和`INFO`只存在于这个日志类中。





### 构造函数

今天我们继续学习C++面向对象编程，包括像类、构造函数所有这些东西。那什么是构造函数呢？构造函数基本上是一种特殊类型的方法，它在每次实例化对象时运行，让我们来看个例子。



#### 初始化

假设我们想要创建一个`Entity`类并在主函数中实例化打印：

```c++
#include <iostream>

class Entity {
public:
    float x;
    float y;
    
    void Print() {
        std::cout << x << "," << y << std::endl;
    }
};

int main(){
    Entity e;
    e.Print();
    
    std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210626131612993.png)



这里得到`Entity`的位置，看似是随机的值。这是因为我们实例化`Entity`并为它分配内存时，我们实际上并没有初始化那个内存，这意味着我们得到了那个内存空间里原来的那些东西，我们可能想做的是初始化内存将其设置为0之类的，这样位置就默认为0。

我们已经知道需要某种初始化，需要一种方法当构造`Entity`实例时把`x`和`y`设为零。我们来创建一个叫`Init()`的方法，它将设置两者的值：

```diff
#include <iostream>

class Entity {
public:
    float x;
    float y;

+   void Init() {
+       x = 0.0f;
+       y = 0.0f;
+   }
    
    void Print() {
        std::cout << x << "," << y << std::endl;
    }
};

int main(){
    Entity e;
+   e.Init();
    e.Print();

    std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210627232258711.png)



#### 构造函数

我们额外编写了相当多的代码，需要定义`Init()`方法。每当我们想在代码中创建一个`Entity`对象（实例）都意味着我们需要实际运行`Init()`函数，相当多的代码代表着相当地不清爽。

当我们构造对象时，如果我们有办法直接运行这个初始化代码就好了，于是就有了构造函数。

构造函数时一种特殊类型的方法，每一次你构造一个对象都会调用这个方法。我们像定义其他方法一样定义它，然而它没有返回类型，并且它的名字必须与类的名称相同：

```diff
#include <iostream>

class Entity {
public:
    float x;
    float y;
    
+   Entity() {
+       x = 0.0f;
+       y = 0.0f;
+   }

-   void Init() {
-       x = 0.0f;
-       y = 0.0f;
-   }

    void Print() {
        std::cout << x << "," << y << std::endl;
    }
};

int main(){
    Entity e;
-   e.Init();
+   std::cout << e.x << "," << e.y << std::endl;
    e.Print();

    std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210629083055729.png)



运行代码可以看到我们得到的结果和`Init()`方法得到的结果是一样的，现在初始化函数可以被构造函数替代了。

如果不指定构造函数，你仍然有一个构造函数，它是一个叫默认构造函数的东西，默认情况下它已经为你准备好了。然而这个构造函数实际上什么都没做，它基本等于：

```c++
Entity() {

}
```



像Java等语言中数据基本类型（如`int`和`float`）会自动初始化为0，但C++的情况并非如此，你必须手动初始化所有基本类型，否则它们将被设置为留在该内存中的其他值。所以初始化非常重要，一定不要忘记。



#### 有参构造函数

我们来看一下带参数的构造函数，可以写很多个构造函数，前提是它们有不同的参数。这叫做函数重载，即有相同的函数（方法）名，但是有不同的参数的不同函数版本。

```c++
Entity(float x,float y) {
  this->x = x;
  this->y = y;
}
```



我们把`x`和`y`赋值，把参数赋值给了我们的成员变量。现在我可以选择使用参数来构造`Entity`对象了：

```diff
#include <iostream>

class Entity {
public:
    float x;
    float y;

    Entity() {
        x = 0.0f;
        y = 0.0f;
    }

+   Entity(float x,float y) {
+       this->x = x;
+       this->y = y;
+   }

    void Print() {
        std::cout << x << "," << y << std::endl;
    }
};

int main(){
+   Entity e(10,5);
-   std::cout << e.x << "," << e.y << std::endl;
		e.Print();

    std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210629084412052.png)



如果不实例化对象，构造函数将不会运行，所以如果你只使用一个类的静态方法，它不会运行。当然，当使用`new`关键字创建一个对象实例时，它也会调用构造函数。

这里也有一些方法可以删除构造函数，例如你有一个`Log`类，它只有静态的日志方法：

```c++
class Log {
public:
    static void write() {
        
    } 
};

int main(){
    
    Log::write();
    Log l;

    std::cin.get();
}
```



我只是想让人们像这样使用我的`Log`类，不希望人们创建实例。有两种不同的解决方法，我们可以通过设置为`private`来隐藏构造函数：

```diff
class Log {
+private:
+		Log() {
+		
+		}
public:
    static void write() {
        
    } 
};

int main(){
    
    Log::write();
    Log l;

    std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210629085153097.png)



可以看到这里得到一个错误，因为我不能访问构造函数。C++为我们提供了一个默认的构造函数，然而我们可以告诉编译器：“不，我不想要那个默认构造函数”：

```diff
class Log {
-private:
-		Log() {
-		
-		}
public:
+		Log() = delete;
		
    static void write() {
        
    } 
};

int main(){
    
    Log::write();
    Log l;

    std::cin.get();
}
```

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210629085538328.png)



我们同样不能调用`Log`，因为默认构造函数实际上并不存在，已经被删除掉了。

还有一些特殊类型的构造函数比如赋值构造函数还有移动构造函数，之后我们会讲。对于基本的使用，这就是构造函数：一个特殊的方法，当你创建类的实例时运行。它的主要用途是初始化该类，当你创建一个新的对象实例时，构造函数确保你初始化了所有的内存，做所有你需要做的设置。





### 析构函数

上次我们讨论了构造函数，包括它们是什么以及如何使用它们。今天我们要讨论一下它邪恶的孪生兄弟，析构函数，它们很相似：

+ 构造函数是你创建一个新的实例对象时运行；而析构函数时在销毁对象时运行，所以任何时候，一个对象要被销毁时将调用析构函数
+ 构造函数通常是设置变量或者做任何你需要的初始化；同样的，析构函数是你写在变量等东西，并清理你使用过的内存
+ 析构函数同时适用于栈和堆分配的对象。如果你使用`new`分配一个对象，当你调用`delete`时析构函数将会被调用；而如果只是一个栈对象，当作用域结束时栈对象将被删除，这时析构函数也会被调用

让我们为之前的`Entity`类添加一个析构函数：

```c++
~Entity() {

}
```



构造函数和析构函数在声明与定义时唯一区别，就是放在析构函数前面的波浪号，有了这个符号`~`，你就知道这是析构了。

在这个例子中我们只有一个简单的类，有两个成员`x`和`y`。当我们为这两个浮点变量申请内存的时候，完全没有考虑之后怎么清除内存，我们会在之后讨论内存分配等复杂问题。

我们继续添加两条消息，告诉我们对象已经被创建或删除：

```diff
class Entity {
public:
    float x;
    float y;

    Entity() {
        x = 0.0f;
        y = 0.0f;
        
+       std::cout << "Created Entity!" << std::endl;
    }

-   Entity(float x,float y) {
-       this->x = x;
-       this->y = y;
-   }

    ~Entity() {
+       std::cout << "Destroyed Entity!" << std::endl;
    }

    void Print() {
        std::cout << x << "," << y << std::endl;
    }
};

int main(){
    Entity e;
    e.Print();
    
    std::cin.get();
}
```



因为这是栈分配的，只有当主函数退出时析构函数才会被调用，所以我们实际上不会看到，因为我们的程序会在那之后立即结束。所以我要写一个`Function()`函数，它将执行`Entity`的相关操作：

```diff
+void Function() {
+   Entity e;
+   e.Print();
+}

int main(){
-   Entity e;
-   e.Print();
+   Function();

    std::cin.get();
}
```



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210629093357666.png)



让我们更深入地看看它是如何工作的。我在25行放一个断点开始调试：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210629093612094.png)



可以看到现在控制台啥都没有，继续走下去：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210629093758366.png)



我们看到`Entity`被创建，构造函数被调用的结果。接着走下去：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210629095135161.png)

这里调用`Print()`打印两个成员变量数值。再往下走：

![image-20210629095841847](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210629095841847.png)



最后作用域到此结束，我们要跳回30行：我们函数返回的地方。因为它的对象是在栈上创建的，当超出作用域时它会被自动销毁，也就是对象`e`，同时析构函数被调用。

这就是析构函数的本质，它只是一个特殊函数或方法，在对象被销毁时调用。为什么我们要写析构函数呢？因为如果在构造函数中调用了特定的初始化代码，你可能想要在析构函数中卸载或销毁所有这些东西，否则可能会造成内存泄漏。

这个方面一个很好的例子是在堆上分配的对象，如果你已经在堆上手动分配了任何类型的内存，那么你需要手动清理。如果在`Entity`类使用中或构造中分配了内存，你可能要在析构函数中删除内存，因为当析构函数调用时那个实例对象消失了。





### 继承

面向对象编程是一个巨大的编程范式，类之间的继承是它的一个基本方面，它是我们可以实际利用的最强大的特性之一。继承运行我们有一个相互关联的类的层次结构，换句话说它允许我们有一个包含公共功能的基类，然后它允许我们从那个基类中分离出来，从最初的父类中创建子类。

继承如此有用的主要原因是它可以帮助我们避免代码重复。代码重复是指我们必须多次写完全相同的代码或者只是可能会略有不同，本质是完全一样的东西。我们不需要一遍又一遍地重复自己，我们可以把类之间的所有公共功能放在一个父类中，然后从基类（父类）创建（派生）一些类，稍微改变下功能或者引入全新的功能。继承给我们提供了这样一种方法，将这些公共代码放到基类中，这样我们就不用像写模版那样不断重复了，让我们来看看如何定义它。

假设我有一个`Entity`类，它将管理游戏中所有的实体对象。在游戏中我们有很多非常具体的实体，然而在某些方面它们将共享功能。例如每个实体在游戏中都有自己的位置，这可以通过两个`float`数来表达：

```c++
#include <iostream>

class Entity {
public:
    float x;
    float y;
};

int main(){

    std::cin.get();
}
```



我们可能想赋予每个实体移动的能力，可通过`move()`方法，将移动位置作为参数：

```c++
void move(float dx,float dy) {
	x += dx;
	y += dy;
}
```



现在我们有了一个基类`Entity`，在游戏中创建的每一个实体都将具有这些特征。让我们继续创建一个新类型的实体，例如一个`Player`类：

```c++
class Player {
public:
    const char* name;
    float x;
    float y;

    void move(float dx,float dy) {
        x += dx;
        y += dy;
    }
};
```



此时还没有继承。如果我们从零开始，我们希望它也有位置以及移动，和`Entity`非常相似。也许这个`Player`类有我们想要额外存储的数据，例如名字`name`。

这实际上是不同的类了，然而有相当多的代码只是被复制粘帖。所以我们能做的就是利用继承的力量，扩展这个`Entity`实体类来创建一个名为`Player`的新类型，然后让它存储新数据以及提供额外的功能，例如打印名字：

```diff
class Player {
public:
    const char* name;
    float x;
    float y;

    void move(float dx,float dy) {
        x += dx;
        y += dy;
    }
    
+   void printName() {
+       std::cout << name << std::endl;
+   }
};
```



现在让我们把`Player`变成`Entity`的子类。我们在类型声明后面写一个冒号`:`，然后我们写`public Entity`：

```diff
+class Player : public Entity{
public:
    const char* name;
    float x;
    float y;

    void move(float dx,float dy) {
        x += dx;
        y += dy;
    }

    void printName() {
        std::cout << name << std::endl;
    }
};
```



现在我们写的这行代码中发生了一些事情，`Player`类现在不仅拥有`Player`类型，而且它也有`Entity`类型，意思是现在是两种类型了。

类型在C++中是相当复杂的主题，因为一方面它们实际上并不存在，然而另一方面它们又会搞事，特别是你有特定的运行时标记激活的话，那个时候我们再去深入了解这整个东西时如何工作的。

`Player`现在拥有`Entity`拥有的所有东西，所以我们拥有所有的类成员`x`、`y`，让我们把重复的代码都去掉：

```diff
class Player : public Entity{
public:
    const char* name;
-   float x;
-   float y;

-   void move(float dx,float dy) {
-       x += dx;
-       y += dy;
-   }

    void printName() {
        std::cout << name << std::endl;
    }
};
```



这样`Player`类看起来很干净了，然而它实际上是一个`Entity`，这意味着仅仅看这个类并不能告诉我们整个故事，我们必须去找`Entity`看看它有什么。就`Player`而言任何`Entity`类中不是私有的东西都可以被访问。

假设我有一个`Player`实例`player`，我不仅可以调用`printName()`函数，也可以调用`move()`函数并访问`x`、`y`：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/image-20210629111020683.png)
