---
title: C#中级编程
tags:
- Csharp
- Unity
categories: Unity 游戏引擎 (Unity Game Engine)
banner_img: 'https://tva1.sinaimg.cn/large/0081Kckwgy1gmd6blk9puj30xc0eg0w4.jpg'
abbrlink: 7d83bb70
date: 2021-01-13 20:04:58
index_img:
comment:
sticky:
---



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/008eGmZEly1gn4nztqqvjj30xc0egq44.jpg)

### 引言

本课程将通过Unity社区简单易学的讲解，在初级教程的基础上更近一步介绍游戏开发编程，了解面向对象思想的编程模式。

<!--more-->

[点击查看Unity社区全部教程](https://unity.cn/ask/question/5f924d5cedbc2a0020a89d1e)

[**观看地址：**https://www.bilibili.com/video/BV1f5411G7bp/](https://www.bilibili.com/video/BV1f5411G7bp/)





### 课程大纲

**创建属性：**如何创建属性以访问类中的成员变量（字段）。

**三元运算符：**如何利用三元运算符建立简单、简写的 IF-ELSE 逻辑条件。

**静态：**了解如何创建静态变量、方法和类。

**方法重载：**如何重载方法以创建具有相同名称的不同方法。

**通用：**如何创建和使用通用方法和类。

**继承：**如何使用继承来重用代码并在相关类之间建立牢固的关系。

**多态：**如何使用多态 (Polymorphism)、向上转换 (Upcasting) 和向下转换 (Downcasting) 在继承的类之间创建强大而动态的功能。

**成员隐藏：**如何在派生类中实现基成员的隐藏。

**覆盖：**如何用子类的成员覆盖基类的成员。

**接口：**如何创建接口并在类中实现它们。

**扩展方法：**如何创建、实现和调用扩展方法。

**命名空间：**如何创建和使用命名空间来组织您的类。

**列表和字典：**如何创建和使用列表和字典集合。

**协程：**如何创建协程并使用它们来实现复杂的行为。

**四元数：**如何利用四元数系统来管理游戏对象的旋转。

**委托：** 如何创建和使用委托在脚本中提供复杂的动态功能。

**属性：**使用属性可以将其他行为附加到所创建的方法和变量。在本视频中，您将学习属性的格式以及如何使用“Range”和“ExecuteInEditMode”属性。

**事件：**如何使用事件创建动态的“广播”系统。


### 创建属性

我们经常需要通过某种方式从位于类之外的代码访问这个类的成员变量。一种方法是公开变量，然后直接访问，虽然这种方法已经够用，但还有更好的办法，那就是使用属性。

属性本身可以当作变量并可以封装成员变量，我们也称之为字段。通过这种封装我们可以更好地控制字段的访问时间和访问方式。假设有一个名为`experience`的字段，该字段位于`Player`类中，我们要想办法让位于该类之外的代码能够访问这个字段，我们要创建一个属性。

属性语法的工作原理如下：首先指定访问修饰符；然后指定类型后跟属性名称，最好将属性命名为字段的名称，不同的是以大写字母开头。在属性名称的后面输入左右花括号就像函数一样，在括号内输入属性的访问器。一个属性可以有两个访问器`get`和`set`，引用属性和分配属性时会分别调用这两个函数，它们使用关键字`get`和`set`，后跟花括号进行声明。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Player
{
   private int experience;

   public int Experience
   {
      get { return experience; }
      set { experience = value; }
   }
}
```

在`get`访问器内我们返回所封装的字段；在`set`访问器中我们使用关键字`value`给字段赋值。以上就是实现属性所需的操作。现在打开另一个脚本，我们可以使用属性代替字段就像平时一样。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Game : MonoBehaviour
{
   void private void Start() 
   {
       Player mPlayer = new Player();

       myPlayer.Experience = 5;
       int x = myPlayer.Experence;
   }
}
```

既然可以使用公共访问修饰符作为变量的开头，为什么还要完成属性创建的过程？使用属性可以执行两项公开变量无法实现的操作：第一，通过省略`get`或`set`可以有效地将字段设置为只写或只读，如果字段是私有的，那么没有`get`访问器就无法读取该字段、没有`set`访问器就无法写入该字段；第二，还可以将访问器视为函数，这表示你可以在访问器内部运行其他代码或调用其他函数，顺着这一思路继续想，可以推断出使用`set`访问器启动协同程序。

字段封装不需要是直接的。设想一个游戏，玩家每获得1000经验即可升级。如果有一个字段代表经验值，就可以使用属性来代表玩家的等级。等级属性的`get`访问器可以返回`experience`字段除以1000得到的值而不返回真实的经验值，这样一来它会返回数字等级而不是玩家拥有的经验数量。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Player
{
   private int experience;

   public int Experience
   {
      get { return experience; }
      set { experience = value; }
   }

   public int Level
   {
       get { return experience/1000; }
       set { experience = value * 1000; }
   }
}
```

此外，等级属性可以有`set`访问器用于接收等级和计算玩家所获得的经验数量并将值存储在`experience`字段中。

属性的另一个特点是它们可以被自动实现。要创建自动实现的属性，可以使用简写语法。在这种语法中，`get`和`set`访问器后面仅跟一个分号。通过这种方式创建的属性，行为与字段完全相同，区别在于可以通过移除`get`或`set`访问器使属性只读或只写。



### 三元运算符

三元运算符是`if-else`语句的精简形式。作为最基本的形式，三元运算符用于根据布尔表达式在两个值之间做出选择，语法格式为`bool ? true表达式 : false表达式`。第一个参数是布尔值或求值为要检验的布尔值的条件，这个参数的结尾标有一个问号；下一个参数是条件为`true`时三元运算符的求值结果，后跟一个冒号；最后一个参数是条件为`false`时三元运算符的求值结果。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class TernaryOperator : MonoBehaviour
{
   void Start()
   {
      int health = 10;
      string message;

      message = health > 0 ? "Player is Alive" : "Player is Dead";
   }
}
```

在这里，我们使用一个简单的三元运算符来判断玩家是生是死。


```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class TernaryOperator : MonoBehaviour
{
   void Start()
   {
      int health = 10;
      string message;

      message = health > 0 ? "Player is Alive" : health == 0 ? "Player is Barely Alive" : "Player is Dead";
   }
}
```

三元运算符可相互嵌套，但如果用于长表达式，这可能会导致代码繁琐，难以理解。使用三元运算符而非`if`语句的一个基本规则是代码需要简单的`if-else`结构且每种情况只需要一个短表达式。



### 静态

静态成员如变量和方法是跨类的所有实例共享的成员，此外，静态成员可直接通过类访问无需先对类的对象进行实例化。通常，成员变量对于类的每个对象是唯一的，虽然类的每个对象具有相同的变量，但它们各有自己的值。然而对于静态变量，类的每个对象具有相同的变量和相同的值，因此如果在一处更改某个静态变量的值，则所有其他静态变量的值也将改变。

假设你想知道`Enemy`类中实例化了多少个对象，一种简单的方法是使用名为`enemyCount`的静态成员变量，将关键字`static`输入到成员声明中即表示声明这是静态的，因此它属于类本身而不属于类的任何实例。然后每次创建enemy对象时都需要让这个变量递增，由于每个对象都让同一个变量递增，因此它自己将包含已创建的所有敌人总数。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Enemy
{
   public static int enemyCount = 0;

   public Enemy()
   {
      enemyCount++;
   }
}
```

访问该静态变量也非常简单，这是一个`game`类，其中创建了几个敌人。为了弄清创建了多少个敌人，我们只需使用类的名称和点运算符来访问`enemyCount`静态变量。在本例中，`enemyCount`变量等于3。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Game
{
   void Start()
   {
      Enemy enemy1 = new Enemy();
      Enemy enemy2 = new Enemy();
      Enemy enemy3 = new Enemy();
   }
}
```

这个过程也适合要用做游戏对象组件的脚本。例如如果要了解在某个场景中创建玩家的数量，我们可以创建一个玩家脚本组件，在这个脚本中我们可以声明静态变量`playerCount`，在`Start()`方法中让这个变量递增。现在只要创建与这个脚本关联的游戏对象，玩家总数就会增加。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Player : MonoBehaviour
{
   public static int playerCount = 0;

   void Start()
   {
      playerCount++;
   }
}
```

在另一个脚本组件中，我们可以使用脚本名称和点运算符来访问这个静态变量。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PlayerManager : MonoBehaviour
{
   void Start()
   {
      int x = Player.playerCount;
   }
}
```

与静态变量一样，静态方法属于类而不属于类的特定对象。举一个非常简单的例子，假设有一个名为`Utilities`的类，在这个类中有一个名为`Add`的静态方法，它返回两个数字相加得到的结果，你可以通过方法`Add`前面的`static`关键字来判断它是静态的。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Utilities
{
   public static int Add(int num1,int num2)
   {
       return num1 + num2;
   }
}
```

现在在另一个类中，你可以使用类的名称和点运算来调用`Add`方法，无需通过实例化类的对象来使用其静态成员。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class UtilitiesExample : MonoBehaviour
{
   void Start()
   {
      int x = Utilities.Add(5,6);
   }
}
```

有可能你已经使用过静态方法只是自己还没有意识到，回顾Unity中使用`Input`的情景，`Input.GetAxis`、`Input.GetKey`和`Input.GetButton`等方法都是静态方法，之所以可以判断这些是静态方法，因为不需要通过实例化`Input`类的对象来使用它们。事实上，Unity提供类许多静态方法从而为您提供多种实用工具和功能。

需要注意的是，不能在静态方法内部使用非静态成员变量。记住，静态方法属于类，而非静态变量属于类的实例。你也可以使整个变量成为静态，只需将关键字`static`置于名称前面即可，结果是类成为静态并且不能创建类的实例。如果想要使类完全由静态成员变量和方法组成如`Input`类，则这样非常有用。



### 方法重载

通过重载过程可以为单个方法提供多个定义，这意味着可以使用同一个方法名称执行两项不同的操作。假设你需要一个方法来执行加法，可以创建`AddNumbers`方法将两个数字相加。但是将字符串相加的工作原理不同，你需要一个名为`AddStrings`的新方法，这样虽然可以达到目的，但问题在于现在需要记住两个不同的方法名称，而它们本质上执行的是相同的操作，一种更好的方法是重载名为`Add`的方法使其处理数字或字符串。

在这里我们有一个名为`Add`的方法，它读取两个数字并返回一个数字，每个方法都有签名。签名(形式参数)由方法的名称和参数组成，在同一个作用域内每个方法的签名(形式参数)都是唯一的。重载方法的操作是为新方法指定相同名称，但指定不同的签名(形式参数)。继续之前的示例，我们可以重载这个`Add`方法来创建一个将字符串相加的新方法，请注意新的`Add`方法名称相同，但具有不同的参数列表。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class SomeClass
{
   public int Add(int num1,int num2)
   {
      return num1 + num2;
   }

   public int Add(stirng str1,string str2)
   {
      return str1 + str2;
   }
}
```

由于签名(形式参数)不同，因此这样是可行的。在其他类中，当我们尝试访问`Add`方法时，可以看到它有两个版本，将根据传入的参数选择正确的版本。如果传入两个数字，将运行用来数字相加的方法；同样，如果传入两个字符串则运行用来将字符串相加的方法。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class SomeOtherClass : MonoBehaviour
{
   void Start()
   {
        SomeClass myClass = new SomeClass();

        myClass.Add(1, 2);
        myClass.Add("Hello ", "World");   
   }
}
```

当系统尝试确定要运行的正确的已重载方法版本时可能会出现三种情况：
+ Exact Match: 与传入参数完全匹配运行这个版本的已重载方法
+ Least Conversion: 如果不是完全匹配，系统将查看所有可能的匹配项，并将选择一个需要最少转换量的版本
+ Error: 最后如果没有可能的匹配项或多个版本所需的转换量相同，则会抛出错误





### 泛型

泛型是一种特征，通过该特征类型可以作为参数传递给类和方法等。实际上，这允许你在不了解所处理数据的确切类型的情况下进行一般编程。我们之前已经看到过`GetComponent`方法使用泛型参数来获取其所寻找的组件的类型，它就是泛型方法。

我们来看一下如何创建泛型方法，这是一个简单泛型方法的示例，首先要看的是泛型的参数`T`，用尖括号括起来置于方法名称之后形参之前。由于这个`T`可以代表任意类型，所以其名称是任意的，但按照惯例字母`T`最为常用。同样，如果要添加多个泛型参数，你可以使用逗号继续添加，命名惯例通常遵循`T`之后的参数是`U`和`V`。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class SomeClass
{
   public T GenericMethod<T, U, V>(T param)
   {
      return param;
   }
}
```

虽然泛型函数不仅限于三个参数，但很少看到人们使用超过三个参数。现在我们知道与这个方法关联的泛型类型是`T`，但`T`只是一个占位符，调用这个方法时`T`最终会成为实际类型，也将成为方法的返回类型和参数类型，因为它们都使用`T`作为其类型。

即使我们有一个方法可使用泛型类型，但目前还不是很有用，泛型类型有什么用途呢？由于我们不知道这个泛型类型的行为方式，所以能做的操作不多。这个泛型参数可以是任意值：浮点数、模型行为等，由于我们不知道它是什么，所以能对它执行的运算很少。例如，我们不能用模型行为乘以2、我们不能访问浮点数的游戏对象字段。

目前，我们把它当作类对象进行处理，这是基类，所有C#类隐式地从基类继承而来，如何才能执行更多运算呢？为了解类型的一些特征，我们必须限制可能的类型，方法是对泛型参数施加限制。为了给函数添加限制，我们在参数之后函数主题之前输入`where`后跟我们将限制的泛型类型，即本例中的`T`。

限制通常分为以下几种类别：
+ 使用关键字`class`确保`T`是引用类型
+ 使用关键字`struct`确保它是值类型
+ 使用关键字`new()`确保它具有不含参数的公共构造函数
+ 使用类名称`MonoBehaviour`表示`T`代表这个类或通过多态表示，`T`代表从中衍生的任意类
+ 使用接口名称表示`T`已实现这个接口


```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class SomeClass
{
   public T GenericMethod<T>(T param) where T : limit
   {
      return param;
   }
}
```

为使用泛型方法，必须指定希望它使用的具体类型。假设你想要使用刚刚创建的泛型方法，在另一个类中，你可以写入方法名称，后跟尖括号里面是你想要的类型，然后在后面输入圆括号和任意参数。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class SomeOtherClass : MonoBehaviour
{
   void Start() 
   {
        SomeClass myClass = new SomeClass();

        myClass.GenericMethod<int>(5);   
   }
}
```

我们讨论的所有特征都适用于`GenericClass`和接口以及方法。通过为类指定泛型类型，你可以影响其中的字段、属性和方法的类型，创建`GenericClass`是泛型的一种较为常见的用法，有助于轻松实现数据结构。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class GenericClass<T>
{
    T item;

    public void UpdateItem(T newItem)
    {
        item = newItem;
    }
}
```

这意味着在使用时在类中用作类型的类型`T`的每个实例将替换为实际类型，为了实例化这个对象必须为`T`指定一个类型，方法是输入类的名称后跟尖括号和所需类型。在输入构造函数的名称之后并在构造函数的参数列表之前也必须执行这个操作。泛型最常见的一种用法是用于字典和列表等集合。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class GenericClassExample : MonoBehaviour
{
    void Start()
    {
        GenericClass<int> myClass = new GenericClass<int>();

        myClass.UpdateItem(5);
    }
}
```





### 继承

Unity支持的脚本语言拥有一个特征叫做继承（Inheritance）。继承是面向对象编程即OOP的基础之一，一个类继承自另一个类时，它会获得被继承类的特征。

在继承的语境下，被继承类称为父类或基类（Parent），继承类称为子类或派生类（Child）。继承结果是父类中存在的项也将出现在子类中，因此方法和变量可以在子类中使用就像父类中一样。例如假设你有一个父类名为`ClassA`，它包含两个方法`dance()`和`sing()`。

```c#
Class A{
	dance();
	sing();
}
```

你还有一个类`ClassB`是从`ClassA`继承而来，因此也会拥有`dance()`和`sing()`这两个方法，无需在`ClassB`中创建这两个方法，因为它们已经存在于`ClassA`中。



处理继承时需要注意三个访问修饰符`public`、`private`和`protected`。大家应该已经熟悉`public`和`private`访问修饰符的概念了，请注意公开的父类的特征将存在于子类中并且可供访问；而私有的特征将存在于子类中但不可访问。`protected`访问修饰符相当于`public`和`private`的混合，与公开的特征一样，受保护的父类的所有特征将存在于子类中并可供访问，但在父类或子类之外将不可访问就像私有的特征一样。

到目前为止你在Unity中使用的大多数类可能都是继承的，作为组件应用于游戏对象的所有脚本的确都是`MonoBehaviour`，这这表明它们继承自`MonoBehaviour`类，默认情况下Unity中创建的脚本遵循这种格式：

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class SomeScript : MonoBehaviour
{
   void Start()
   {
      
   }

   void Update()
   {
      
   }
}
```



要使这个类继承自其他类，只需将名称`MonoBehaviour`更改为其他类名即可：

```c#
public class SomeScript : SomeClass
```

要更改类以使其不继承任何父类，只需删除冒号和父类名称即可。大家可能会疑惑我们的脚本为什么继承自`MonoBehaviour`，游戏对象、转换、`start()`方法、`update()`方法等项均来自`MonoBehaviour`，因为继承了`MonoBehaviour`，我们能够访问这些特征。

继承结构是分层的，通常可以将继承想象成动物王国。在本例中我们有一个父类名为`Animal`，这个类将包含所有必需的定义和属性以使这个类拥有动物行为。从这个`Animal`基类我们可以派生出两个子类`Vertebrate`和`Invertebrate`，然后`Vertebrate`又成为更多类的父类比如哺乳动物、爬行动物或两栖动物，每个子类将获得其基类提供的信息并添加更多信息。

```
Animal
|_ Vertebrate
|_ Invertebrate
```



正如我们的动物示例，面向对象编程中的继承称为IS-A关系，这表示子类是父类，爬行动物是脊椎动物，哺乳动物是动物。大家之前可能遇到过Unity中的一个示例：`Capsule Collider`是`Collider`，后面将进一步介绍多态这一概念。

在游戏开发中，继承的概念可能非常有用且适用。例如我们可能有一个名为`Humanoid`的类，这个类含钙类人动物应该在游戏中执行的所有操作。然后有两个子类`Enemy`和`Player`，这两个子类控制玩家和敌人在游戏中的行为细节同时仍具有类人动物的行为，因为它们继承了`Humanoid`类的所有成员。

```
Humanoid
|_ Player
|_ Enemy
	 |_ Orc
	 |_ Goblin
```

然后`Enemy`可能还有两个子类`Orc`和`Goblin`，这两者的行为类似于`Enemy`，继而又类似于`Humanoid`。通过这种方式为了使`Orc`和`Goblin`拥有我们所设计的行为，要编写的代码大大减少，因为我们在反复利用`Humanoid`和`Enemy`的代码。



在子类继承的项中构造函数是一个例外，因为它们对类是唯一的，不会共享。但是在子类中调用构造函数时，其父类的构造函数会立即被调用。由于类可能有多个不同的构造函数，因此我们可能想要控制调用哪个基类构造函数函数。为此可以使用关键字`base`，通过在子类构造函数的参数列表后添加一个冒号可以使用关键字`base`，在基类构造函数的参数列表中显式调用基类的具体构造函数；如果不显式调用基类的构造函数，则仍会隐式调用默认构造函数。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Apple : Fruit
{
   public Apple() : base("apple")
   {
      //Constructor Code
   }
}
```

除了调用基类的构造函数，`base`关键字还可用来访问基类的其他成员。这种方法十分适用于访问基类版本的任何内容，因为它不同于派生的版本，覆盖函数时通常会有这样的需要。





### 多态

多态是继承的一个特征，允许类拥有多个类型。在继承层次结构中任何子类都可以称为父类，这表示再需要基类的时候可用派生类来替代它。假设有一个游戏使用继承层次结构，其中`Orc`和`Goblin`派生自`Enemy`，而`Enemy`派生自`Humanoid`。你可能想要创建一个集合让它包含场景中的所有`Enemy`对象，不必创建两个集合一个包含所有`Orc`一个包含所有`Goblin`，而是创建一个集合让它包含所有`Enemy`对象（即`Orc`对象和`Goblin`对象都是这个集合的元素）。同样，如果有一个`Player`类继承自`Humanoid`，你可以创建一个集合让它包含场景中的所有`Humanoid`对象。

```
Humanoid
|_ Player
|_ Enemy
	 |_ Orc
	 |_ Goblin
```

多态也适用于函数参数等。思考一下`OnTriggerEnter()`函数，它们通常包含`Collider`参数`other`，游戏对象没有`Collider`组件，但它们可能有`BoxCollider`，`Sphere Collider`，`Mesh Collider`或类似组件。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class SomeScript : MonoBehaviour
{
   void OnTriggerEnter(Collider other)
   {
      //Do Something Fun!
   }
}
```

调用`OnTriggerEnter()`函数时，我们不知道会使用什么类型的`Collider`。事实上，每个对象的特定`Collider`都会传入函数，由于所有这些不同的`Collider`均继承自`Collider`父类，因此它们都将发挥作用。需要注意的是，反过来则不成立。在前面的示例中`Orc`是`Enemy`但是`Enemy`不是`Orc`，你不能为需要子类的某个项提供父类。

多态的一种较为明智的用法是涉及构造函数和对象引用，你可以声明基类类型的对象，然后调用其中一个派生类的构造函数。这是因为变量引用需要的是基类的类型，子类的构造函数会创建衍生类型的项。如果你感到困惑，只要记得子类是父类即可，因此这种转换是有效的，这个过程被称为向上转型（up-casting），当对象向上转型时，它只能被视作其父类的一个对象。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class SomeScript : MonoBehaviour
{
   void Start()
   {
      ParentClass myClass = new ChildClass();
     
      myClass.ParentMethod();
   }
}
```

在本例中，子类向上转型时它只能被视作父类，这表示只能使用父类中可用的变量和方法。在使用时会把它们视为位于父类对象中。虚拟函数是一个例外，它将调用最新覆盖版本，有关虚拟函数以及覆盖虚拟函数的更多信息在后面会讲到。

为了将这个子类视作子类我们需要向下转型子类变量使其恢复为子类类型，具体方法是将类型名称括在括号内并将其置于变量前面，我们可以再用一组括号括起来并使用点运算符来访问成员，也可以创建对这个新版本的引用。

```c#
ChildClass myChild = (ChildClass)myClass;
myChild.ChildMethod();
```





### 成员隐藏

通过继承父类的成员在子类中自动可用或继承到子类中。在子类中重新创建即重新声明父类成员的过程被称为成员隐藏。隐藏成员使用关键字`new`的方式略有不同，为了隐藏基类的成员，应在成员的类型前面使用`new`声明子类成员。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class ChildCLass : ParentClass
{
   new float SomeValue = 5f;

   void SayHello()
   {
      //Do something fun!
   }
}
```

一般情况下，这不会影响以这种方式生命的成员的使用，但是当子类向上转型为父类和使用的成员时它将是来自父类的成员，尽管实例为子类。

想象之前的继承层次结构`Humanoid-Enemy-Orc`。`Humanoid`中有一个方法`Yell()`，这个方法会播放一个音频片段并移动模型手臂。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Humanoid
{
   void Yell()
   {
     //Play audio clip
     //Move arms.
   }
}
```

`Enemy`中有另一个函数`Yelll()`，这个函数将`Enemy`主纹理的颜色更改为黄色。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Enemy : Humanoid
{
   new void Yell()
   {
      ///Change material color to yellow
   }
}
```

`Orc`也有一个新的`Yell()`函数，但这个函数将导航网格目的地发送到Northern Shetland Isle。假设我们有一个`Humanoid`对象集合，其中包括部分`Humanoid`、部分`Enemy`和部分`Orc`。如果我们对这个集合中的所有对象调用`Yell()`函数，则它们都将调用`Humanoid`版本的`Yell`，这是因为我们将`Orc`和`Enemy`对象声明为`Humanoid`并且它们已隐式向外转型为`Humanoid`。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Orc : Enemy
{
   new void Yell()
   {
      //Set nav mesh to Northern Shetland Isle
   }
}
```

这种行为通常不是期望的行为因此并不常用，但这一点值得引起注意，事实上这种行为与覆盖完全相反，有关覆盖的更多信息在之后的章节会介绍。







### 覆盖

覆盖是指更改子类中的父类方法，结果是当我们调用方法时将调用最新版本的方法或最新覆盖的版本。使用继承层次结构时，我们通常想要使用与积累略微不同的函数版本，这个操作非常简单，只需在子类中重新创建方法并根据需要编写代码即可。

考虑这样一种情况，有一个`Humanoid`基类，它有一个`Enemy`派生类，后者又有一个`Orc`派生类。`Humanoid`类有一个名为`Yell()`的函数，调用时模型会发出叫喊声并举起双手捂住嘴巴。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Humanoid
{
   public void Yell()
   {
     //Play "Yelling Sound"
     //Raise hands to mouth
   }
}
```

`Enemy`类自动继承这个`Yell()`方法，但是我们要进行修改想让敌人吸引其他敌人。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Enemy : Humanoid
{
   public void Yell()
   {
      ///Attract nearby enemies
   }
}
```

我们也希望`Orc`能够调用这个函数，但从`Orc`对象调用`Yell()`时这个区域内的所有`Orc`会在短时间内因其攻击而获得奖励。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Orc : Enemy
{
   public void Yell()
   {
      //Power up nearby orcs
   }
}
```

我们实际要做的是在每个子类中覆盖`Yell()`方法的父版本。当我们尝试覆盖子类中的父方法时Unity会发出警告，为了抑制该警告并告知Unity我们就是要覆盖方法，可以使用`virtual`和`override`关键字，它们位于方法的返回类型之前，父类中的方法定义为`virtual`，而所有子类中的方法定义为`override`。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Humanoid
{
   public virtual void Yell()
   {
     //Play "Yelling Sound"
     //Raise hands to mouth
   }
}

public class Enemy : Humanoid
{
   public override void Yell()
   {
      ///Attract nearby enemies
   }
}

public class Orc : Enemy
{
   public override void Yell()
   {
      //Power up nearby orcs
   }
}
```

声明为`virtual`的任何方法可被任何子类覆盖，覆盖的一种更有趣的用法是让每个子类为方法添加特定的功能，同时不失去父类提供的原始功能。为此需要使用`base`关键字来同时调用方法的父版本。

在上一个示例中，我们想让`Enemy`保留`Humanoid`的功能同时添加其自己的效果、让`Orc`保留`Enemy`的功能同时添加自己的效果，为此我们需要对`Enemy`和`Orc`中的父`Yell()`方法进行`base`调用：

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Enemy : Humanoid
{
   public override void Yell()
   {
   		base.Yell();
      ///Attract nearby enemies
   }
}
```

现在调用`Orc`的`Yell()`方法时将调用`Enemy`的`Yell()`方法，继而将调用`Humanoid`的`Yell()`方法：

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class Orc : Enemy
{
   public override void Yell()
   {
      base.Yell();
      //Power up nearby orcs
   }
}
```



覆盖对多态也非常有用，通常将父方法声明为`virtual`、将子方法声明为`override`，我们将有效覆盖方法的父版本。当我们将子引用向上转型为父对象然后调用方法时，将调用这个方法的子版本。



### 接口

接口可被视为关于功能的协定，实现接口的任何类必需拥有其所有方法和属性。作为交换，通过使用多态其他类可将实现类视作接口，需要注意的是借口不是类，不能有自己的实例。继承是一种类的关系（即一个类继承自另一个类）；而接口使用实现关系（即一个类实现一个接口）。

接口通常在类外部声明，声明接口时通常对每个接口使用一个脚本。但在本示例中我们将在同一个脚本中展示两个接口。按照惯例，声明接口所使用的名称以大写字母I开头，后跟以另一个大写字母开头的名称；由于接口通常描述实现类将具备的某种功能，因此许多接口以后缀`able`结尾，但值得注意的是这不是强制性的并且可能具有误导性，具体取决于接口。



```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public interface IKillabe
{
    void Kill();
}

public interface IDamageable<T>
{
    void Damage(T damageTaken);
}
```



我们在这里声明了两个接口，`IKillable`中有一个函数`Kill()`，它的返回类型为`void`没有参数。实现`IKillable`接口的任何类必须有一个与这个签名匹配的公共函数。`IDamageable`接口具有泛型类型`T`，这表示这个接口中的任意内容都可以具有泛型类型，它的函数`Damage()`需要一个类型为`T`的参数，当类实现具有泛型类型的接口时必须选中这个类型，然后必须始终使用相应类型。

实现接口需要满足一些要求，也有一些好处。为了实现接口，类必须公开这个接口中存在的所有方法、属性、事件和索引器，如果不这样做将导致错误。接口的主要优势是允许跨多个类定义通用功能，因此你可以根据类实现的接口安全的对类的用途作出假设。

要实现接口，只需在类具有的任何继承之后添加一个逗号，后跟接口的名称。如果类不是从其他类继承而来，则不需要逗号。如果接口具有泛型类型，则名称应后跟尖括号并在里面输入类型。在本例中，我们有一个`Avatar`类，它继承自`MonoBehaviour`并实现`IKillable`和类型为`float`的`IDamageable`。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;


public class Avatar : MonoBehaviour, IKillable , IDamageable<float>
{
    public void Kill()
    {
      	//Do something fun
    }
  
  	public void Damage(float damageTaken)
    {
      	//Do something fun
    }
}
```



我们还必须声明这些接口所需要的两个函数，请注意函数主体与接口相互独立，可按你希望的任何方式进行实现。在你的游戏中如果想要实现全毁或全灭的效果，那么这些接口来源可能很有用。只要找到实现了`IKillable`或`IDamageable`的所有项，就能确保它们将获得`Kill()`或`Damage()`函数。

你可能会好奇既然可在一个类中合理使用函数并让其他类继承这个函数，为什么还要在类中实现接口呢？简单点回答就是：你可以实现多个接口，但不能从多个类继承，因此通过接口可以很好的提供广泛功能。

```
IDamageable
|__ Wall
|__ Car
```



更好的答案是接口用于跨多个互不相关的类定义通用功能。考虑两个类`Wall`和`Car`，它们之间几乎没有什么关联，唯一的共通之处是它们都是可破坏的。由于两者之间如此不同，因此继承父类毫无意义，但实现接口则非常实用。



### 扩展方法

通过扩展方法，可以向类型添加功能而不必创建`Drive Type`或更改原始类型，它们非常适用于需要向类添加功能但不能编辑类的情况。

考虑一下Unity中内置的`Transform`类，我们无法访问它的源码，假设我们想要使用函数轻松重置`Transform`的位置：旋转和缩放。这个函数的理想位置是放在`Transform`类中，但由于不能直接向这个类进行添加并且将这个函数添加到派生类也没有任何意义，所以我们将为其创建扩展。

扩展方法必须放在非泛型静态类中。静态类中常见做法是专门创建一个类来包含它们，扩展方法的用法与实例方法类似它们也声明为静态方法，而非静态类方法需要在参数中使用`this`关键字。在我们的示例中将创建一个静态类`ExtensionMethods`，然后创建扩展方法`ResetTransformation`，注意该方法声明为静态方法，并且第一个参数带有`this`关键字，如果我们想要更多参数，可以直接输入而不使用`this`关键字。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;


public static class ExtensionMethods
{
    public static void ResetTransformation(this Transform trans)
    {
        trans.position = Vector3.zero;
        trans.localRotation = Quaternion.identity;
        trans.localScale = new Vector3(1,1,1);
    }    
}
```



在方法中我们可以编写代码来重置`Transform`。需要注意的是，尽管这个函数声明具有参数，但调用函数时它将没有参数，参数隐式地成为`Transform`的实例。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class SomeClass : MonoBehaviour
{
    void Start()
    {
        transform.ResetTransformation();
    }
}
```

为了使用这个拓展方法，你只需将其视为所扩展的类的成员。在本例中我们扩展的是`Transform`，可以认为这个方法现已成为`Transform`类的一部分。





### 命名空间

命名空间就像类的容器，其目的是帮助组织脚本避免脚本之间发生冲突。例如你可能会在Unity中创建工具来帮助你开发应用，你可以将工具和实际应用放在不同的命名空间中，这样一来自动补全功能就不会建议过多不必要的类。

到目前为止编写的所有脚本可能一直在使用命名空间，在Unity中的C#脚本顶部默认情况下你会看到几行：

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
```

它们都是命名空间，`using`关键字表示其后面的命名空间中的任何内容都可在脚本中使用，如果注释掉其中的一部分可以看到自动补全功能建议的可供使用的类大幅减少，这是因为游戏对象、转换、刚体等许多类均位于`UnityEngine`命名空间中。

为了将我们的类放入命名空间中，需要用命名空间语法将类包围起来，首先输入关键字`namespace`，然后是命名空间的名称（可以是现有命名空间，也可以是新的）。在本例中，我们将命名空间称为`SampleNamespace`，然后在类前面输入花括号括起来。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using SampleNamespace;

namespace SampleNamespace
{
		public class SomeClass : MonoBehaviour
		{
    		void Start()
    		{
          	
    		}
		}
}
```

我们可以通过三种方法使用来自特定命名空间的类。前面已介绍过第一种用法，即在脚本顶部包含`using`指令。访问类的第二种方法是使用点运算符，例如无需在脚本顶部添加`using SampleNamespace`，每次要引用来自`SampleNamespace`的类时都可以输入`SampleNamespace.SomeClass`:

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class SomeClass : MonoBehaviour
{
    void Start()
    {
 				SampleNamespace.SomeClass myClass = new SampleNamespace.SomeClass();          	
    }
}
```

这种方法可以避免歧义，但可能较为繁琐，尤其是对于大命名空间名称例如`SampleNamespace`。

最后一种选择是将你编写的类放入需要访问的命名空间中，一般不建议使用这种方法除非你打算将这个类放入同一个命名空间中。只要类位于不同的命名空间中，它们就可以使用相同名称，但是由于脚本的名称与其中包含的类的名称相同，因此脚本必须位于不同文件夹中，这样才能具有相同的类名。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using SampleNamespace;

namespace SampleNamespace
{
		public class SomeClass : MonoBehaviour
		{
    		void Start()
    		{
          	SomeClass myClass = new SomeClass();
    		}
		}
}
```

使用命名空间时，请注意避免模糊定义，比如`System`和`UnityEngine`是两个常用的命名空间，它们均包含`Random`类的定义如果你同时使用它们则需要通过使用点运算符来消除类的歧义。

命名空间可以嵌套，只需将一个命名空间声明括在另一个命名空间声明内即可。





### 列表和字典

在本章中我们将介绍两个泛型集合列表和字典，我们还将使用它们的方法，两者的工作原理类似于数组，但有一些明显区别。

#### 列表

我们首先介绍`List`类，列表就像是大小动态变化的数组，这表示你不需要提前知道列表将包含多少个元素。在深入讲解之前，我们快速创建一个可以存储在列表中的类：

```c#
using UnityEngine;
using System.Collection;

public class BadGuy
{
   public string name;
   public int power;

   public BadGuy(string newName,int newPower)
   {
      name = newName;
      power = newPower;
   }
}

```

现在我们可以开始创建列表。`List`是泛型类，因此在任何修饰符之后我们输入类名后跟要存储在列表中的类型。在本例中我们输入`BadGuy`，然后为列表指定名称。由于列表是一个类，因此我们调用构造函数。

```c#
using UnityEngine;
using System.Collection;
using System.Collection.Generic;

public class SomeClass : MonoBehaviour
{
   void Start()
   {
      List<badGuy> badguys = new List<BadGuy>();
   }
}
```

列表现在是空的，我们来为它分配内容。我们使用`Add`函数执行这个操作，这将在列表末尾添加新元素。`Add`函数的参数是要添加到列表的对象，在本例中我们将为`BadGuy`类调用构造函数，然后填充列表。

```c#
using UnityEngine;
using System.Collection;
using System.Collection.Generic;

public class SomeClass : MonoBehaviour
{
   void Start()
   {
      List<badGuy> badguys = new List<BadGuy>();

      badguys.Add(new BadGuy("Harvey",50));
      badguys.Add(new BadGuy("Magneto",100));
      badguys.Add(new BadGuy("Pip",5));
   }
}
```

要访问列表项，可以像数组一样使用索引进行访问。它还有一个`count`属性，作用类似于数组的`length`属性。列表的`RemoveAt`和`Insert`等函数用于手动排列，`RemoveAt`用于列表中移除给定索引处的元素，这个元素上方的所有元素会下移一位；`Insert`需要一个索引和一个元素将这个索引之后的所有元素上移一位。

列表的最强大函数之一是`Sort`，可用于按给定类型的任何变量对这个类型的列表进行排序，它依赖于类型来实现`IComparable`接口。我们回到`BadGuy`类进行实现，首先`IComparable`位于系统名称空间所以需要声明我们正在使用它；接着需要声明这个类正在实现这个接口，这看起来类似于继承，我们将使用泛型`IComparable`其泛型类型必须是这个类；最后为了完成`IComparable`接口的协定，我们需要声明公开函数`CompareTo`返回整数并以我们的泛型类型`BadGuy`作为参数。

```c#
using UnityEngine;
using System.Collection;

public class BadGuy : IComparable<BadGuy>
{
   public string name;
   public int power;

   public BadGuy(string newName,int newPower)
   {
      name = newName;
      power = newPower;
   }
  
  public int CompareTo(BadGuy other)
  {
    	if(other == null)
        return 1;
    	return power - other.power;
  }
}
```

`CompareTo`方法的思路是如果从中调用这个方法的对象大于被视作参数的对象，则函数返回正数；反之返回负数；两者相等则返回零。定义一个对象是否大于另一个对象由程序员决定，对于我们的函数首先要检查传递函数的`BadGuy`是否存在，如果不存在则这个`BadGuy`较大，函数应返回正数；否则函数返回两个`BadGuy`的差值。

这个比较的结果可以给予任何依据，接口只要求我们实现方法。现在为了这个比较结果对列表排序，我们调用`badguys.Sort`并打印输出结果：

```c#
using UnityEngine;
using System.Collection;
using System.Collection.Generic;

public class SomeClass : MonoBehaviour
{
   void Start()
   {
      List<badGuy> badguys = new List<BadGuy>();

      badguys.Add(new BadGuy("Harvey",50));
      badguys.Add(new BadGuy("Magneto",100));
      badguys.Add(new BadGuy("Pip",5));
     
     	badguys.Sort();
     	foreach(BadGuy guy in badguys)
      {
        	print(guy.name + " " + gut.power);
      }
   }
}
```

要想重新创建列表并移除所有元素，可使用`Clear`函数，在本例中为`badguys.Clear()`。



#### 字典

字典的工作原理与列表类似，但它有两种类型，这表示每个元素组成一个键值对（有时简称KVP）。字典的用途也与列表不同，列表通常用于替代需要更多灵活性或功能的数组；字典用作可通过一个或多个键访问的值的集合。

声明字典的过程与列表非常类似，首先添加名称空间，然后像之前一样声明变量但具有两个泛型类型，第一个类型是键，这是为了访问第二个类型而引用的类型；第二个类型是值。在本例中，我们的键类型为`string`，值类型为`BadGuy`，我们使用这个字典来存储可用于识别特定`BadGuy`的不同搜索词：

```c#
using UnityEngine;
using System.Collection;
using System.Collection.Generic;

public class SomeOtherClass : MonoBehaviour
{
   void Start()
   {
     	Dictionary<string, BadGuy> badguys = new Dictionary<string, BadGuy>();

     	BadGuy bg1 = new BadGuy("Harvey",50);
     	BadGuy bg2 = new BadGuy("Magneto",100);

			badguys.Add("gangster",bg1);
     	badguys.Add("mutant",bg2);
   }
}
```

访问与键相关的值非常类似于访问数组或列表的元素，但是我们不使用索引因为索引对字典没有内在含义，我们在方括号中插入一个键。在本例中，我们插入一个字符串，这样就会返回对应的`BadGuy`，如果提供了键但字典中不存在这个键则会抛出异常。因此如果无法保证键的存在，最好使用`TryGetValue`方法。这个方法具有一个键类型的参数和值类型的输出参数，如果作为第一个参数传递的键存在则返回`ture`。

```c#
using UnityEngine;
using System.Collection;
using System.Collection.Generic;

public class SomeOtherClass : MonoBehaviour
{
   void Start()
   {
     	Dictionary<string, BadGuy> badguys = new Dictionary<string, BadGuy>();

     	BadGuy bg1 = new BadGuy("Harvey",50);
     	BadGuy bg2 = new BadGuy("Magneto",100);

			badguys.Add("gangster",bg1);
     	badguys.Add("mutant",bg2);
     
      BadGuy magneto = badguys["mutant"];
     	BadGuy temp = null;
     
     	if(badguys.TryGetValue("birds",out temp))
      {
        	//success
      }
     	else
      {
        	//failure
      }
   }
}
```

虽然这种从字典中返回值的方法更加安全，但比直接引用具体键速度略慢。为提高效率可在方括号内使用键，但前提是指定键确定位于字典中。



### 协程

协同程序可被视为按时间间隔执行的函数，这类函数与特殊的`Yield`语句搭配使用，`Yield`语句从函数中返回代码执行，然后当函数继续时将从上次停止的地方开始执行。我们来看一个示例协同程序：

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class CoroutinesExample : MonoBehaviour
{
    public float smoothing = 1f;
    public Transform target;

    void Start()
    {
        StartCoroutine(MyCoroutine(target));
    }

    IEnumerator MyCoroutine(Transform target)
    {
        while (Vector3.Distance(transform.position,target.position) > 0.05f)
        {
            transform.position = Vector3.Lerp(transform.position,target.position,smoothing * Time.deltaTime);

            yield return null;
        }
        
        print("Reached the target.");
    
        yield return new WaitForSeconds(3f);
        
        print("MyCoroutine is not finished");
    }
}
```

首先我们来看协同程序`MyCoroutine`本身，其返回类型`IEnumerator`表示函数可以返回实现`IEnumerator`接口的任意内容，但是稍后会看到从协同程序返回的内容比平时要多。接着可以看到，它将`Transform`作为参数，然后我们开始`while`循环直到对象和目标的距离小于0.05为止。

```c#
while (Vector3.Distance(transform.position,target.position) > 0.05f)
{
		transform.position = Vector3.Lerp(transform.position,target.position,smoothing * Time.deltaTime);

    yield return null;
}
```

在这个循环中我们首先计算对象和目标之间的线性插值，下面一行是`yield return null;`，这允许协同程序照常工作。这表明在执行这行代码时将产生函数执行并返回空的`IEnumerator`，代码将在返回值指示的时间从这个点继续执行，返回值为`null`表示协同程序将在下一个更新后继续。

由于协同程序将在循环结束时继续，因此将重新评估循环条件：如果`Transform`尚未达到目标则进行插值计算向目标靠近，协同程序再次`yield`直到下次更新。当循环条件不再为`ture`时循环将推出，协同程序将在控制台上输出，然后协同程序将再次`yield`，但这次它将返回`WaitForSeconds`类的实例，结果是在给定秒数之后代码继续执行，3秒之后"MyCoroutine is not finished"将输出到控制台。

```c#
IEnumerator MyCoroutine(Transform target)
{
    while (Vector3.Distance(transform.position,target.position) > 0.05f){}

    print("Reached the target.");

    yield return new WaitForSeconds(3f);

    print("MyCoroutine is not finished");
}
```



调用协同程序只需要使用`StartCoroutine`函数，它以协同程序调用或协同程序名称字符串为参数，这里展示的是前一种调用。这种方法更明智，但如果你使用名称字符串进行调用则还可以调用`StopCoroutine`以提前中止。

```c#
void Start()
{
		StartCoroutine(MyCoroutine(target));
}
```



协同程序的一个真正优势是与属性结合使用时发挥的作用。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class PropertiesAndCoroutines : MonoBehaviour
{
    private Vector3 target;
    
    public float smoothing = 7f;
    public Vector3 Target
    {
        get { return target; }
        set
        {
            target = value;
            
            StopCoroutine("Movement");
            StartCoroutine("Movement",target);
        }
    }

    IEnumerator Movement(Transform target)
    {
        while (Vector3.Distance(transform.position,target.position) > 0.05f)
        {
            transform.position = Vector3.Lerp(transform.position,target.position,smoothing * Time.deltaTime);

            yield return null;
        }
    }
}
```



在属性`Target`中首先我们将目标字段设为正确值，然后停止任何移动协同程序。需要注意的是`StopCoroutine`仅适用于已通过字符串调用启动的协同程序，就像下一行一样。

我们的移动协同程序与上个示例相似，它计算对象位置到给定目标位置的插值距离并移动直至二者接近。这样设置脚本的效果是将获得一个移动的游戏对象而不必使用逐帧轮询值的`Update`函数，轮询值会降低我们编写代码的效率，虽然有时必须要这么做，但我们应尽量避免。





### 四元数

在Unity中，转换旋转存储为四元数，它们类似于向量但有4个组件`x`、`y`、`z`和`w`，这些组件相互依赖并配合使用，从而定义对象可能需要的任何旋转。关于四元数的处理最值得注意的其中一个方面是由于`x`、`y`、`z`和`w`组件是配合使用的，因此不能仅调用个别组件，所幸Unity有许多内置函数可简化四元数的管理。有一种管理旋转的系统大家可能都有所耳闻，叫做欧拉角。Inspector中显示的旋转值就使用了这个系统，因为它更易于理解。

欧拉角旋转基于围绕x、y和z轴的旋转，你可能会问既然欧拉角更容易理解那为什么Unity要使用四元数？特别是在Inspector中Unity要将四元数转换为欧拉角。可以这样说，欧拉角要遵从万向节锁，而万向节锁会妨碍增量旋转正常工作。幸运的是Unity将旋转存储为四元数，四元数不受万向节锁的影响，因此我们不会遇到这个问题。

#### LookRotation

我们来看通过四元数类提供的某个功能，我们从`LookRotation`函数入手：

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class LookAtScript : MonoBehaviour
{
    public Transform target;

    void Update()
    {
        Vector3 relativePos = target.position - transform.position;
        transform.rotation = Quaternion.LookRotation(relativePos);
    }
}
```

公开字段`target`用于表示目标转换，在`Update`函数中我们将使用`Quaternion.LookRotation`旋转对象使其面向目标。`LookRotation`函数以`Vector3`为参数，返回与传入的`Vector3`相符的四元数旋转。

通过计算对象和目标之间的相对向量，我们可以使对象的z轴指向目标，其工作原理与`transform.LookAt`相似，但利用四元数明确设置旋转。另外值得注意的是，我们可以向函数传递第二个`Vector3`，这个`Vector3`告知函数哪个方向被认为是向上的。

```c#
transform.rotation = Quaternion.LookRotation(relativePos,new Vector3(0,1,0));
```



#### Slerp

`slerp`是球形插值的简称，它与线性插值`lerp`函数非常相似，两者最大的区别是`lerp`在两个四元数之间的均匀插值而`slerp`在曲线上插值，结果是随着时间推移`lerp`提供均匀的变化，而`slerp`开始后会变慢并在中间时加快速度。我们来看一个实现重力轨道效应的例子：

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class GravityScript : MonoBehaviour
{
    public Transform target;

    void Update()
    {
        Vector3 relativePos = (target.position + new Vector3(0, .5f, 0)) - transform.position;
        Quaternion rotation = Quaternion.LookRotation(relativePos);

        Quaternion current = transform.localRotation;
        
        transform.localRotation = Quaternion.Slerp(current,rotation,Time.deltaTime);
        transform.Translate(0,0,3 * Time.deltaTime);
    }
}
```

在`GravityScript`中设置与之前的`LookAtScript`类似，同样有一个公开字段用于表示目标转换，同样计算对象和目标之间的相对向量，但这一次我们添加偏移将球体高度考虑进去。和之前一样计算`LookRotation`，但这次不将它存储在对象转换的旋转中，相反将它存储在名为`rotation`的四元数变量中，然后我们存储名为`current`的对象四元数变量的局部旋转。

之后使用`slerp`函数缓慢转动对象使其面向目标，`slerp`函数读入`current`旋转，最终结果旋转和它应该插值或转动的速度。旋转不会立即发生，而是随时间缓慢旋转，这是本示例的关键所在。朝着目标稍微转动对象后，我们将其向前移动一点。最终呈现的效果是流畅的轨道效应。



#### identity

将四元数设置为`Quaternion.identity`，实际会将其欧拉旋转设为`(0,0,0)`或无旋转。

```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class SomeClass : MonoBehaviour
{
    private void Start()
    {
 				transform.rotation = Quaternion.identity;       
    }
}
```





### 委托

通过委托，你可以在脚本中创建可靠且复杂的行为。委托可被简单地视作函数的容器，可以进行传递；或像变量一样使用，可以向委托分配值。区别在于变量包含数据，而委托包含函数。

```c#
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class DelegateScript : MonoBehaviour
{
    delegate void MyDelegate(int num);
    private MyDelegate myDelegate;
    
    void Start()
    {
        myDelegate = PrintNum;
        myDelegate(50);

        myDelegate = DoubleNum;
        myDelegate(50);
    }

    void PrintNum(int num)
    {
        print("Print Num: " + num);
    }

    void DoubleNum(int num)
    {
        print("Double Num: " + num);
    }
}
```

在`DelegateScript`中首先要做的是清除委托模板，这个模板将明确指示可以分配给委托哪些类型的方法。我们用`delegate`关键字创建委托，后跟委托的签名。与函数一样，委托有返回类型、名称和参数列表，在本例中我们可以看到要将这个方法分配给这个委托，它的返回类型必须为`void`并接受单个整数参数。

```c#
delegate void MyDelegate(int num);
```

创建委托类型后声明成员变量，这个成员变量拥有刚刚创建的委托的类型。

```c#
private MyDelegate myDelegate;
```

脚本底部有两个方法`PrintNum`和`DoubleNum`，可以看到每个方法的返回类型都为`void`并接受单个整数参数，这雨我们的委托一样。此外，每个方法对传入的整数数据的处理略有不同。

```c#
void PrintNum(int num)
{
		print("Print Num: " + num);
}

void DoubleNum(int num)
{
		print("Double Num: " + num);
}
```



现在我们来看看委托的具体用途，在`Start()`方法中可以看到我们将`PrintNum`方法的名称分配给`myDelegate`变量，然后将`myDelegate`变量当作函数来使用。我们传入值50，然后将`DoubleNum`方法的名称分配给`myDelegate`变量，同样像函数一样调用这个变量。

```c#
void Start()
{
    myDelegate = PrintNum;
    myDelegate(50);

    myDelegate = DoubleNum;
    myDelegate(50);
}
```



查看控制面板，可以看到我们能够使用同一个委托变量调用两个不同的方法，这让我们能够更好地动态控制在游戏里调用哪些函数。

```
Print Num: 50
Double Num: 50
```





委托还支持多播，多播允许单个委托变量同时代表多个方法。

```c#
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class MulticastScript : MonoBehaviour
{
    delegate void MultiDelegate();
    MulticastDelegate myMultiDelegate;
    
    void Start()
    {
        myMultiDelegate += PowerUp;
        myMultiDelegate += TurnRed;

        myMultiDelegate();
    }

    void PowerUp()
    {
        print("Orb is powering up!");
    }

    void TurnRed()
    {
        GetComponent<Renderer>().material.color = Color.red;
    }
}
```

在`MulticastScript`中，可以看到我们创建了一个委托模板，这个委托查找名为`MultiDelegate`的委托，它没有参数且返回类型为`void`。接着创建名为`myMultiDelegate`的成员变量，其类型是刚刚创建的委托模板的类型。

在脚本底部有两个分别名为`PowerUp`和`TurnRed`的方法，这两个方法都没有参数且返回类型为`void`，这与我们的委托类型一样。

```c#
void PowerUp()
{
		print("Orb is powering up!");
}

void TurnRed()
{
		GetComponent<Renderer>().material.color = Color.red;
}
```

在`Start()`方法中我们将多播委托变量，为此我们使用`+=`运算符，将`PowerUp`和`TurnRed`方法分配给同一个委托变量。这样一来变量`myMultiDelegate`同时包含`PowerUp`和`TurnRed`方法，然后我们将变量`myMultiDelegate`当作函数进行调用。

```c#
void Start()
{
    myMultiDelegate += PowerUp;
    myMultiDelegate += TurnRed;

    myMultiDelegate();
}
```



回到Unity运行场景，可以看到通过多播委托变量一次调用即可同时调用，通过这种方式我们可以叠加功能。如果要从委托变量中移除方法，可以使用`-=`运算符结合方法名称进行删除。

```c#
myMultiDelegate -= PowerUp;
myMultiDelegate -= TurnRed;
```



必须注意的一点是如果在向委托变量了分配之前尝试将其视为函数进行调用，这种做法将引发错误，我们应该避免。目前未分配到方法的任何委托变量的值为`null`，因此在使用前最好经常检查以确保委托不等于`null`。

```c#
if(myMultiDelegate != null)
		myMultiDelegate();
```





### 特性

通过特性，你可以在声明方法、变量或类时为其附加信息。要获取并增强现有代码，或通过某种方式更改代码，这非常有用。特性本身的作用和用途相差很大，下面我们来看一个例子：

```c#
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class SpinScript : MonoBehaviour
{
    public int speed = 0;

    void Update()
    {
        transform.Rotate(new Vector3(0,speed * Time.deltaTime,0));
    }
}
```

在`SpinScript`中可以看到，首先声明整数`speed`变量并将其设为0，然后在`Update`方法中，我们基于当前速度围绕y轴旋转对象。这样一来，我们可以为`speed`变量提供所需对象的任意值，对象的旋转速度也会因此更改。

这种方法虽然有效，但如果想要限制`speed`变量的值该怎么做呢？我们可以编写代码来检测变量的当前值并防止其超出范围，或者可以为其附加特性。特性直接编写在要修改的代码之上或之前，一般不会影响脚本的任何其他部分，在本例中我们将使用`range`特性。

```c#
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class SpinScript : MonoBehaviour
{
  	[Range(-100,100)]
    public int speed = 0;

    void Update()
    {
        transform.Rotate(new Vector3(0,speed * Time.deltaTime,0));
    }
}
```

所有特性的语法均以左方括号开始。对于`range`特性，写入关键字`Range`后跟圆括号，在圆括号内写入最小值和最大值，然后用右方括号结束特性。注意，在本例中我们将特性置于变量声明上方，我们也可以轻松将其置于声明之前：

```c#
[Range(-100,100)] public int speed = 0;
```

回到Unity，`speed`字段会变成一个滑块，可以从最小值滑倒最大值。



我们要介绍的另一个特性是`ExecuteInEditMode`特性，这个特性会使关联脚本运行即使场景未处于运行模式也是如此，下面我们再来看一个例子：

```c#
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class ColorScript : MonoBehaviour
{
    void Start()
    {
        GetComponent<Renderer>().sharedMaterial.color = Color.red;
    }
}
```

在`ColorScript`中，我们将对象的共享颜色设为红色。如果我们想要在不允许场景的情况下在Unity中看到这个变化，可对其应用`ExecuteInEditMode`特性。为此，我们将其置于类名前面，因为`ExecuteInEditMode`特性将应用于脚本中的所有代码，而不只是一个部分。

```c#
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

[ExecuteInEditMode]
public class ColorScript : MonoBehaviour
{
    void Start()
    {
        GetComponent<Renderer>().sharedMaterial.color = Color.red;
    }
}
```

这个特性没有任何参数，因此不需要任何圆括号。回到Unity会发现物体已经变红，即使我们从未运行场景脚本也已执行。

值得注意的是，需要谨慎使用`ExecuteInEditMode`特性。脚本通常在运行场景时运行，当你停止运行场景时，对场景中游戏对象进行的任何更改都会撤销；但是在编辑模式下执行的脚本将能够修改、创建和删除场景中的对象。由于更改不实在运行模式下发生的，因此它不会恢复，而是永久性的。





### 事件

事件是一种特殊委托，非常适用于想要提醒其他类发生了某个事件，实际上你会发现事件函数与公共多播委托非常相似。事件可被视为广播系统，对事件感兴趣的任何类都可以将方法订阅到事件，发生这个特定情况时如点击按钮、充能或玩家受伤，我们会调用事件，进而调用已订阅的方法。

在本例中，我们想要在玩家点击我们在屏幕上绘制的按钮时调用事件。

```c#
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class EventManager : MonoBehaviour
{
    public delegate void ClickAction();

    public static event ClickAction OnClicked;

    void OnGUI()
    {
        if (GUI.Button(new Rect(Screen.width / 2 - 50,5,100,30), "Click"))
        {
            if (OnClicked != null)
                OnClicked();
        }
    }
}
```

在`EventManager`在我们可以看到，首先创建委托类型，命名为`ClickAction`。我们可以看到希望订阅到事件的任何方法必须没有参数且返回类型为`void`。接下来我们创建事件变量，此时要使用关键字`event`，注意这也是一个静态变量因此我们可以在类外部使用它而无需实例化这个类的对象。

```c#
public delegate void ClickAction();
public static event ClickAction OnClicked;
```

正如前面所说，我们将在玩家点击按钮时调用这个事件，因此这个脚本具有`OnGUI`方法。在`OnGUI`方法内，我们在屏幕上创建一个按钮，玩家点击这个按钮时我们会像使用函数一样使用事件变量，这实际上将调用我们的事件。请注意，与委托一样如果我们调用没有订阅的事件，则将引发错误，因此在调用之前，我们应始终确保事件不等于`null`。

```c#
void OnGUI()
{
    if (GUI.Button(new Rect(Screen.width / 2 - 50,5,100,30), "Click"))
    {
      if (OnClicked != null)
        OnClicked();
    }
}
```



下面我们再来看看这个事件的订阅者：

```c#
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class TeleportScript : MonoBehaviour
{
    void OnEable()
    {
        EventManager.OnClick += Teleport;
    }

    void OnDisable()
    {
        EventManger.Onclicked -= Teleport;
    }

    void Teleport()
    {
        Vector3 pos = transform.position;
        pos.y = Random.Range(.3f,1.0f);
        transform.position = pos;
    }
}
```

在`TeleportScript`中我们创建了一个名为`Teleport`的方法，我们将这个方法订阅到在`EventManager`中创建的事件。注意，`Teleport`方法没有参数且返回类型为`void`，就像委托一样，该方法负责沿Y轴随机放置对象。

脚本顶部附近有一个名为`OnEnable`的内置方法，在场景中创建或启用这个脚本关联的对象时将调用这个内置方法。我们使用这个方法将`Teleport`方法订阅到`Event`脚本的`OnClicked`事件。

```c#
void OnEable()
{
  	EventManager.OnClick += Teleport;
}
```

接下来是`OnDIsable`方法，这个方法与之前相反，场景中的某个对象被禁用或销毁时会调用`OnDisable`方法。我们从事件退订方法，这样做可确保当事件发生时不会再调用我们的方法。

```c#
void OnDisable()
{
  	EventManger.Onclicked -= Teleport;
}
```

这一步非常重要，如果不执行可能会导致内存泄漏和游戏出错。最好是每当你将方法订阅到事件时必须同时设定相应的退订。



```c#
using System;
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Random = System.Random;

public class TurnColorScript : MonoBehaviour
{
    void OnEable()
    {
        EventManager.OnClick += TurnColor;
    }

    void OnDisable()
    {
        EventManger.Onclicked -= TurnColor;
    }

    void TurnColor()
    {
        Color col = new Color(Random.value,Random.value,Random.value);
        GetComponent<Renderer>().material.color = col;
    }
}
```



与`TeleportScript`非常相似，在本例中有一个名为`TurnColor`的方法，它没有参数且返回类型为`void`。该方法可将对象材质变成任意颜色。

```c#
void TurnColor()
{
    Color col = new Color(Random.value,Random.value,Random.value);
    GetComponent<Renderer>().material.color = col;
}
```

同样也有`OnEnable`和`OnDisable`方法，负责事件的订阅和退订：

```c#
void OnEable()
{
  	EventManager.OnClick += TurnColor;
}

void OnDisable()
{
  	EventManger.Onclicked -= TurnColor;
}
```

再次提醒，必须注意的是要正确使用事件并防止代码出错，从事件退订方法至关重要。





我们可以看到`EventManager`只需留意事件本身和事件触发器，它不需要了解`TeleportScript`或`TurnColorScript`；同样，`TeleportScript`和`TurnColorScript`也不需要相互了解。这样一来，我们就能创建一个非常可靠且灵活的广播系统。

还有一个问题是为什么在`EventManager`中使用静态事件变量而非公开委托变量，事实上可以使用公开委托变量实现完全相同的事件功能，事件只是特殊的委托。

```c#
public static event ClickAction OnClicked;
```

对于这种情况，我们使用事件而非公开委托变量的原因是事件具有内在的安全性，而委托变量没有。通过事件，其他类只能订阅和退订；如果改为公开委托变量，其他类可能会调用或覆盖委托变量来执行各种不合理操作。

一般而言，如果想要创建一个包含多个类的动态方法系统，请使用事件变量而非委托变量。