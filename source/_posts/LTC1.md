---

title: 从C到C++简明教程
abbrlink: 293466a9
date: 2021-01-29 16:13:49
tags:
- Cpp
- LeetCode
- Algorithm
categories: LeetCode题解 (LeetCode Solution)
---





![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/008eGmZEly1gn4mym0wp6j30xc0irn4o.jpg)

<div align=center>
  <font size="3">
    <i>
      <a href="https://www.behance.net/gallery/110074175/Haokan_Newbrand_video?tracking_source=search_projects_recommended">Haokan_Newbrand_video</a> by 
      <a href="https://www.behance.net/donerzozo">Donerzozo</a>
    </i>
  </font>
</div>


### 引言

关于由C转向C++的一些拓展与注意事项。


<!--more-->



### 使⽤C++刷算法的好处

+ 在已经学习过C语⾔的前提下，学习C++并使⽤它刷算法的学习成本⾮常低～只需要⼏个⼩时就可以学会～
+ C++向下兼容C，C语⾔⾥⾯的语法⼤部分都可以在C++⽂件中运⾏，所以学习C++对刷算法时编程语⾔的表达能⼒进⾏扩充有益⽆害，例如C语⾔的输⼊输出（ `scanf` 和 `printf` ）⽐C++快，那么就可以在使⽤C++刷算法同时使⽤ `scanf` 和 `printf` 提⾼代码运⾏效率
+ C++拥有丰富的STL标准模版库，这也是PAT甲级、LeetCode等题⽬中经常需要⽤到的，单纯使⽤C语⾔解决问题会⽐C++的STL解决该问题麻烦很多～
+ C++的 string 超级好⽤～⽐C语⾔⾥⾯的char数组好⽤多啦～⽤了就再也不想回去的那种～
+ C++可以在某⼀变量使⽤前随时定义该变量，⾮常⽅便
+ 在解决⼀些较为简单的PAT⼄级题⽬的时候（例如⼀些时间复杂度限制不严格的题⽬）， `cin` 、 `cout` 输⼊输出⾮常⽅便～⽤过的都说好～ (๑• . •๑)

虽然C++是⼀⻔⾯向对象语⾔，但是对于刷算法这件事⽽⾔，我们并不需要掌握它⾯向对象的部分～只需要掌握刷算法的时候需要⽤到的部分（基本输⼊输出、STL标准模板库、 `string` 字符串等）就可以啦～C语⾔和C++有很多相似之处，且C++向下兼容C语⾔，所以我没有说的地⽅就直接⽤C语⾔的语法表示就好～以下是正⽂，先来段代码⽅便讲解：

```c++
#include <iostream>
using namespace std;
int main() {
  int n;
  cin >> n;
  cout << "hello, world" << n + 1 << endl;
  return 0; 
}
```



### 名称空间

这句话是使⽤“std”这个名称空间（ `namespace` ）的意思～因为有的时候不同⼚商定义的函数名称彼此之间可能会重复，为了避免冲突，就给所有的函数都封装在各⾃的名称空间⾥⾯，使⽤这个函数的时候就在`main`函数前⾯写明⽤了什么名称空间，⼏乎在C++中使⽤到的⼀些⽅法如 `cin` 、 `cout` 都是在 `std` 名称空间⾥⾯的，所以可以看到 `using namespace std; `这句话⼏乎成了我每段C++代码的标配，就和 `return 0;` ⼀样必须有～其实也可以不写这句话，但是使⽤ std ⾥⾯的⽅法的时候就会麻烦点，要在⽅法名前加上 `std::` ，⽐如写成这样：

```c++
std::cin >> n;
std::cout << "hello, world" << n + 1 << endl;
```

我觉得这样⽐较丑，所以不管要不要⽤到，直接每道题的代码标配得写 `using namespace std;` 就好啦～



### 输入输出

就如同 `scanf` 和 `printf` 在 `stdio.h` 头⽂件中⼀样， `cin` 和 `cout` 在头⽂件 `iostream` ⾥⾯，看名字就知道， `io` 是输⼊输出 `input` 和 `output` 的⾸字⺟， `stream` 是流，所以这个 `iostream` 头⽂件⾥包含的⽅法就是管理⼀些输⼊输出流的～

`cin` 和 `cout` ⽐较⽅便，不⽤像C语⾔⾥的 `scanf` 、 `printf` 那样写得那样繁琐， `cin >> n;` 和`scanf("%d", &n);` ⼀样的意思（⽽且⽤ `cin` 再也不⽤担⼼像 `scanf` ⼀样忘记写取地址符 `&` 了耶），注意 `cin` 是向右的箭头，表示将内容输⼊到 `n` 中～

同样， `cout << n;` 和 `printf("%d", n);` ⼀样的意思，此时 `cout` 是向左的两个箭头，注意和 `cin` 区分开来～

⽽且不管 `n` 是 `double` 还是 `int` 或者是 `char` 类型，只⽤写 `cin >> n;` 和 `cout << n;` 这样简单的语句就好，不⽤像C语⾔中需要根据 `n` 的类型对应地写 `%lf` 、 `%d` 、 `%c` 这样麻烦～

`endl` 和 `"\n"` 的效果⼤致相同， `endl` 的全称是end of line，表示⼀⾏输出结束，然后输出下⼀⾏～（微⼩区别是，使⽤ `endl` 会⽐使⽤ `"\n"` 换⾏后多⼀个刷新输出缓冲区的操作，but不必care这些细节…）⼀般如果前⾯是个字符串引号的话直接 `"\n"` ⽐较⽅便，如果是变量之类的我觉得写 `endl` 会⽐较好看～想⽤哪个就⽤哪个～

```c++
cout << "hello, guy～\n";
cout << n << endl;
```

`cin` 和 `cout` 虽然使⽤起来更⽅便，但是输⼊输出的效率不如 `scanf` 和 `printf` 快，所以如果是做PAT⼄级⾥⾯那种简单、对时间复杂度要求不⾼的题⽬，直接⽤ `cin` 和 `cout` 会觉得写起来⽐较省事⼉；如果题⽬对时间复杂度要求⽐较⾼，全都改成 `scanf` 和 `printf` 可以提⾼代码的输⼊输出效率，⽐如有的时候发现⽤ `cin` 、 `cout` 做题⽬超时了，改成 `scanf` 和 `printf` 就AC了～



### 头文件

C++的头⽂件⼀般是没有像C语⾔的 `.h` 这样的扩展后缀的，⼀般情况下C语⾔⾥⾯的头⽂件去掉 `.h` 然后在前⾯加个 `c` 就可以继续在C++⽂件中使⽤C语⾔头⽂件中的函数啦～⽐如：

```c++
#include <cmath> // 相当于C语⾔⾥⾯的#include <math.h>
#include <cstdio> // 相当于C语⾔⾥⾯的#include <stdio.h>
#include <cctype> // 相当于C语⾔⾥⾯的#include <ctype.h>
#include <cstring> // 相当于C语⾔⾥⾯的#include <string.h>
```



### 变量声明

C语⾔的变量声明⼀般都在函数的开头，但是C++在⾸次使⽤变量之前声明即可～（当然也可以都放在函数的开头），⽽且⼀般C语⾔⾥⾯会在 for 循环的外⾯定义 i 变量，但是C++⾥⾯可以在 `for` 循环内部定义～（关于这点， VC++6.0 ⾥⾯可能会发现代码复制进去编译不通过，这是因为这个编译器太⽼啦，建议不要⽤这么上古的编译器啦～）⽽且在 `for` 循环⾥⾯定义的局部变量，在循环外⾯就失效啦（就是脱离这个局部作⽤域就会查⽆此变量的意思），所以⼀个 `main` 函数⾥⾯可以定义好多次局部变量 `i` ，再也不⽤担⼼写的循环太多变量名 `i` 、 `j` 、 `k` 不够⽤啦～

```c++
#include <iostream>
using namespace std;
int main() {
    int n;
    cin >> n;
    cout << "hello, liuchuo" << n + 1 << endl;
    int m;
    cin >> m;
    for (int i = 0; i < n; i++) { // 这个i只在for循环⾥⾯有⽤，出了这个for循环就相当于
    不⻅了
    		cout << i;
     }
    for (int i = 0; i < m; i++) { // ⼜可以定义⼀个i啦，和上⾯那个i不会冲突～
    		cout << i + 2;
     }
  return 0;
}
```



### bool变量

`bool` 变量有两个值， `false` 和 `true` ，以前⽤C语⾔的时候都是⽤ `int` 的 `0` 和 `1` 表示 `false` 和 `true`的，现在C++⾥⾯引⼊了这个叫做 `bool` （布尔）的变量，⽽且C++把所有⾮零值解释为 `true` ，零值解释为 `false` ～所以直接赋值⼀个数字给 `bool` 变量也是可以的～它会⾃动根据 `int` 值是不是零来决定给 `bool` 变量赋值 `true` 还是 `false` ～

```c++
bool flag = true;
bool flag2 = -2; // flag2为true
bool flag3 = 0; // flag3为false
```



### 定义常量

和C语⾔相同，C++⾥⾯可以使⽤ `const` 这个限定符定义常量，⽐如 `int` 类型的常量 `a` 这样定义：

```c++
const int a = 99999999; // a为int类型的常量，它的值不可更改
```



### string类

以前⽤ `char[]` 的⽅式处理字符串很繁琐，现在有了 `string` 类，定义、拼接、输出、处理都更加简单啦～不过 `string` 只能⽤ `cin` 和 `cout` 处理，⽆法⽤ `scanf` 和 `printf` 处理：

```c++
string s = "hello world"; // 赋值字符串
string s2 = s;
string s3 = s + s2; // 字符串拼接直接⽤+号就可以
string s4;
cin >> s4; // 读⼊字符串
cout << s; // 输出字符串
```

⽤ `cin` 读⼊字符串的时候，是以空格为分隔符的，如果想要读⼊⼀整⾏的字符串，就需要⽤ `getline`～

`s` 的⻓度可以⽤ `s.length()` 获取～（有⼏个字符就是⻓度多少，不存在 `char[]` ⾥⾯的什么末尾的结束符之类的～）

```c++
string s; // 定义⼀个空字符串s
getline(cin, s); // 读取⼀⾏的字符串，包括空格
cout << s.length(); // 输出字符串s的⻓度
```

`string` 中还有个很常⽤的函数叫做 `substr` ，作⽤是截取某个字符串中的⼦串，⽤法有两种形式：

```c++
string s2 = s.substr(4); // 表示从下标4开始⼀直到结束
string s3 = s.substr(5, 3); // 表示从下标5开始，3个字符
```



### 结构体

定义好结构体 `stu` 之后，使⽤这个结构体类型的时候，C语⾔需要写关键字 `struct` ，⽽C++⾥⾯可以省略不写：

```c++
struct stu {
  int grade;
  float score;
};
struct stu arr1[10]; // C语⾔⾥⾯需要写成struct stu
stu arr2[10];// C++⾥⾯不⽤写struct，直接写stu就好了～
```



### 引用&传值

这个引⽤符号 `&` 要和C语⾔⾥⾯的取地址运算符 `&` 区分开来，他们没有什么关系，C++⾥⾯的引⽤是指在变量名之前加⼀个 `&` 符号，⽐如在函数传⼊的参数中 `int &a` ，那么对这个引⽤变量 `a` 做的所有操作都是直接对传⼊的原变量进⾏的操作，并没有像原来 `int a` ⼀样只是拷⻉⼀个副本（传值），举两个例⼦：

```c++
void func(int &a) { // 传⼊的是n的引⽤，相当于直接对n进⾏了操作，只不过在func函数中换了个名字叫a
  a = 99; }
int main() {
	int n = 0;
	func(n); // n由0变成了99
}
```

```c++
void func(int a) {// 传⼊的是0这个值，并不会改变main函数中n的值
	a = 99; }
int main() {
	int n = 0;
	func(n);// 并不会改变n的值，n还是0 
}
```



### STL

#### vector

之前C语⾔⾥⾯⽤ `int arr[]` 定义数组，它的缺点是数组的⻓度不能随⼼所欲的改变，⽽C++⾥⾯有⼀个能完全替代数组的动态数组 `vector` （有的书⾥⾯把它翻译成⽮量， `vector` 本身就是⽮量、向量的意思，但是叫做动态数组或者不定⻓数组我觉得更好理解，绝⼤多数中⽂⽂档中⼀般不翻译直接叫它`vector`～），它能够在运⾏阶段设置数组的⻓度、在末尾增加新的数据、在中间插⼊新的值、⻓度任意被改变，很好⽤～它在头⽂件 `vector` ⾥⾯，也在命名空间 `std` ⾥⾯，所以使⽤的时候要引⼊头⽂件 `#include <vector>` 和 `using namespace std;`

`vector` 、 `stack` 、 `queue` 、 `map` 、 `set` 这些在C++中都叫做容器，这些容器的⼤⼩都可以⽤ `.size()`获取到，就像 `string s` 的⻓度⽤ `s.length()` 获取⼀样～（ `string` 其实也可以⽤ `s.size()` ，不过对于`vector` 、 `stack` 、 `queue` 、 `map` 、 `set` 这样的容器我们⼀般讨论它的⼤⼩ `size` ，字符串⼀般讨论它的⻓度 `length` ～其实 string ⾥⾯的 `size` 和 `length` 两者是没有区别、可以互换使⽤的。

```c++
#include <iostream>
#include <vector>
using namespace std;
int main() {
  vector<int> v1; // 定义⼀个vector v1，定义的时候没有分配⼤⼩
  cout << v1.size(); // 输出vector v1的⼤⼩，此处应该为0
  return 0; 
}
```

`vector` 可以⼀开始不定义⼤⼩，之后⽤ `resize` ⽅法分配⼤⼩，也可以⼀开始就定义⼤⼩，之后还可以对它插⼊删除动态改变它的⼤⼩～⽽且不管在 `main` 函数⾥还是在全局中定义，它都能够直接将所有的值初始化为0（不⽤显式地写出来，默认就是所有的元素为0），再也不⽤担⼼C语⾔⾥⾯出现的那种 `int arr[10];` 结果忘记初始化为0导致的各种bug啦～

```c++
vector<int> v(10); // 直接定义⻓度为10的int数组，默认这10个元素值都为0
// 或者
vector<int> v1;
v1.resize(8); //先定义⼀个vector变量v1，然后将⻓度resize为8，默认这8个元素都是0
// 在定义的时候就可以对vector变量进⾏初始化
vector<int> v3(100, 9);// 把100⻓度的数组中所有的值都初始化为9
// 访问的时候像数组⼀样直接⽤[]下标访问即可～(也可以⽤迭代器访问，下⾯会讲～) 
v[1] = 2;
cout << v[0];
```

不管是 `vector` 、 `stack` 、 `queue` 、 `map` 还是 `set` 都有很多好⽤的⽅法，这些⽅法都可以在官⽅⽹站中直接查询官⽅⽂档，上⾯有⽅法的讲解和代码示例～官⽅⽂档是刷题时候必不可少的好伙伴～如果你⽤的是 `Mac OS` 系统，下载软件 `Dash` 然后在⾥⾯下载好C++，平时查⽂档会更⽅便，我平时做开发写算法都在 `Dash` ⾥⾯查⽂档，内容和官⽅⽂档是⼀样的～）PS：经此教程读者Keil Glay提醒， `Windows` 下有受 `Dash` 启发⽽开发的离线⽂档浏览器 `Zeal` ，和 `Dash` 的功能⼀样，使⽤ `Windows` 的⼩伙伴可以下载 `Zeal` 看离线官⽅⽂档～

⽐如进⼊官⽹搜索 `vector` ，就会出现 `vector` 拥有的所有⽅法，点进去⼀个⽅法就能看到这个⽅法的详细解释和代码示例～当然我们平时写算法⽤不到那么多⽅法啦，只有⼏个是常⽤的～以下是⼀些常⽤的 `vector` ⽅法：

```c++
#include <iostream>
#include <vector>
using namespace std;
int main() {
	vector<int> a; // 定义的时候不指定vector的⼤⼩
  cout << a.size() << endl; // 这个时候size是0
  for (int i = 0; i < 10; i++) {
  		a.push_back(i); // 在vector a的末尾添加⼀个元素i
   }
  cout << a.size() << endl; // 此时会发现a的size变成了10
  vector<int> b(15); // 定义的时候指定vector的⼤⼩，默认b⾥⾯元素都是0
  cout << b.size() << endl;
  for (int i = 0; i < b.size(); i++) {
  		b[i] = 15;
   }
  for (int i = 0; i < b.size(); i++) {
  		cout << b[i] << " ";
   }
  cout << endl;
  vector<int> c(20, 2); // 定义的时候指定vector的⼤⼩并把所有的元素赋⼀个指定的值
  for (int i = 0; i < c.size(); i++) {
  		cout << c[i] << " ";
   }
  cout << endl;
  for (auto it = c.begin(); it != c.end(); it++) { // 使⽤迭代器的⽅式访问vector
  		cout << *it << " ";
   } 
  return 0; 
}
```

容器 `vector` 、 `set` 、 `map` 这些遍历的时候都是使⽤迭代器访问的， `c.begin()` 是⼀个指针，指向容器的第⼀个元素， `c.end()` 指向容器的最后⼀个元素的后⼀个位置，所以迭代器指针 `it` 的for循环判断条件是 `it != c.end()`

访问元素的值要对 `it` 指针取值，要在前⾯加星号～所以是 `cout << *it;`这⾥的`auto`相当于 `vector<int>::iterator` 的简写，关于 `auto` 下⽂有讲解～



#### set

`set` 是集合，⼀个 `set` ⾥⾯的各元素是各不相同的，⽽且 `set` 会按照元素进⾏从⼩到⼤排序～以下是 `set` 的常⽤⽤法：

```c++
#include <iostream>
#include <set>
using namespace std;
int main() {
  set<int> s; // 定义⼀个空集合s s.insert(1); // 向集合s⾥⾯插⼊⼀个1
  cout << *(s.begin()) << endl; // 输出集合s的第⼀个元素 (前⾯的星号表示要对指针取值)
  for (int i = 0; i < 6; i++) {
  		s.insert(i); // 向集合s⾥⾯插⼊i
   }
  for (auto it = s.begin(); it != s.end(); it++) { // ⽤迭代器遍历集合s⾥⾯的每⼀个元素
  		cout << *it << " ";
   }
  cout << endl << (s.find(2) != s.end()) << endl; // 查找集合s中的值，如果结果等于s.end()表示未找到 (因为s.end()表示s的最后⼀个元素的下⼀个元素所在的位置)
  cout << (s.find(10) != s.end()) << endl; // s.find(10) != s.end()表示能找到10这个元素
  s.erase(1); // 删除集合s中的1这个元素
  cout << (s.find(1) != s.end()) << endl; // 这时候元素1就应该找不到啦～
  return 0; 
}
```



#### map

`map` 是键值对，⽐如⼀个⼈名对应⼀个学号，就可以定义⼀个字符串 `string` 类型的⼈名为“键”，学号 `int` 类型为“值”，如 `map<string, int> m;` 当然键、值也可以是其它变量类型～ `map` 会⾃动将所有的键值对按照键从⼩到⼤排序， `map` 使⽤时的头⽂件 `#include <map>` 以下是 `map` 中常⽤的⽅法：

```c++
#include <iostream>
#include <map>
#include <string>
using namespace std;
int main() {
  map<string, int> m; // 定义⼀个空的map m，键是string类型的，值是int类型的
  m["hello"] = 2; // 将key为"hello", value为2的键值对(key-value)存⼊map中
  cout << m["hello"] << endl; // 访问map中key为"hello"的value, 如果key不存在，则返
  回0
  cout << m["world"] << endl; m["world"] = 3; // 将"world"键对应的值修改为3 m[","] = 1; // 设⽴⼀组键值对，键为"," 值为1
  // ⽤迭代器遍历，输出map中所有的元素，键⽤it->first获取，值⽤it->second获取
  for (auto it = m.begin(); it != m.end(); it++) {
  		cout << it->first << " " << it->second << endl;
   }
  // 访问map的第⼀个元素，输出它的键和值
  cout << m.begin()->first << " " << m.begin()->second << endl;
  // 访问map的最后⼀个元素，输出它的键和值
  cout << m.rbegin()->first << " " << m.rbegin()->second << endl;
  // 输出map的元素个数
  cout << m.size() << endl;
  return 0; 
}
```



#### stack

栈 `stack` 在头⽂件 `#include <stack>` 中，是数据结构⾥⾯的栈～以下是常⽤⽤法：

```c++
#include <iostream>
#include <stack>
using namespace std;
int main() {
  stack<int> s; // 定义⼀个空栈s
  for (int i = 0; i < 6; i++) {
  		s.push(i); // 将元素i压⼊栈s中
   }
  cout << s.top() << endl; // 访问s的栈顶元素
  cout << s.size() << endl; // 输出s的元素个数
  s.pop(); // 移除栈顶元素
  return 0; 
}
```



#### queue

队列 `queue`在头⽂件 `#include <queue>` 中，是数据结构⾥⾯的队列～以下是常⽤⽤法：

```c++
#include <iostream>
#include <queue>
using namespace std;
int main() {
  queue<int> q; // 定义⼀个空队列q
  for (int i = 0; i < 6; i++) {
  		q.push(i); // 将i的值依次压⼊队列q中
   }
  cout << q.front() << " " << q.back() << endl; // 访问队列的队⾸元素和队尾元素
  cout << q.size() << endl; // 输出队列的元素个数
  q.pop(); // 移除队列的队⾸元素
  return 0; 
}
```



#### unordered_map & unordered_set

`unordered_map` 在头⽂件 `#include <unordered_map>` 中， `unordered_set` 在头⽂件 `#include<unordered_set>` 中～

`unordered_map` 和 `map` （或者 `unordered_set` 和 `set` ）的区别是， `map` 会按照键值对的键 `key` 进⾏排序（ `set` ⾥⾯会按照集合中的元素⼤⼩进⾏排序，从⼩到⼤顺序），⽽ `unordered_map` （或者 `unordered_set` ）省去了这个排序的过程，如果偶尔刷题时候⽤ `map` 或者 `set` 超时了，可以考虑⽤ `unordered_map` （或者 `unordered_set` ）缩短代码运⾏时间、提⾼代码效率～⾄于⽤法和 `map` 、 `set` 是⼀样的～



### 位运算

`bitset` ⽤来处理⼆进制位⾮常⽅便。头⽂件是 `#include <bitset>` ， `bitset` 可能在PAT、蓝桥OJ中不常⽤，但是在LeetCode OJ中经常⽤到～⽽且知道 `bitset` 能够简化⼀些操作，可能⼀些复杂的问题能够直接⽤ `bitset` 就很轻易地解决～以下是⼀些常⽤⽤法：

```c++
#include <iostream>
#include <bitset>
using namespace std;
int main() {
  bitset<5> b("11"); //5表示5个⼆进位
  // 初始化⽅式：
  // bitset<5> b; 都为0
  // bitset<5> b(u); u为unsigned int，如果u = 1，则输出b的结果为00001
  // bitset<8> b(s); s为字符串，如"1101"，则输出b的结果为00001101，在前⾯补0
  // bitset<5> b(s, pos, n); 从字符串的s[pos]开始，n位⻓度
  // 注意，bitset相当于⼀个数组，但是它是从⼆进制的低位到⾼位分别为b[0]、b[1]……的
  // 所以按照b[i]⽅式逐位输出和直接输出b结果是相反的
  cout << b << endl; // 如果bitset<5> b("11"); 则此处输出00011(即正常⼆进制顺序)
  for(int i = 0; i < 5; i++)
  cout << b[i]; // 如果bitset<5> b("11"); 则此处输出11000(即正常⼆进制顺序的倒
  序)
  cout << endl << b.any(); //b中是否存在1的⼆进制位
  cout << endl << b.none(); //b中不存在1吗？
  cout << endl << b.count(); //b中1的⼆进制位的个数
  cout << endl << b.size(); //b中⼆进制位的个数
  cout << endl << b.test(2); //测试下标为2处是否⼆进制位为1 b.set(4); //把b的下标为4处置1 b.reset(); //所有位归零
  b.reset(3); //b的下标3处归零
  b.flip(); //b的所有⼆进制位逐位取反
  unsigned long a = b.to_ulong(); //b转换为unsigned long类型
  return 0; 
}
```



### sort函数

`sort` 函数在头⽂件 `#include <algorithm>` ⾥⾯，主要是对⼀个数组进⾏排序（ `int arr[]` 数组或者 `vector` 数组都⾏）， `vector` 是容器，要⽤ `v.begin()` 和 `v.end()` 表示头尾；⽽ `int arr[]` ⽤ `arr` 表示数组的⾸地址， `arr+n` 表示尾部～

```c++
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;
bool cmp(int a, int b) { // cmp函数返回的值是bool类型
	return a > b; // 从⼤到⼩排列
}
int main() {
  vector<int> v(10);
  for (int i = 0; i < 10; i++) {
  		cin >> v[i];
   }
  sort(v.begin(), v.end());// 因为这⾥没有传⼊参数cmp，所以按照默认，v从⼩到⼤排列
  int arr[10];
  for (int i = 0; i < 10; i++) {
  		cin >> arr[i];
   }
  sort(arr, arr + 10, cmp); // arr从⼤到⼩排列，因为cmp函数排序规则设置了从⼤到⼩
  return 0; 
}
```



### ⾃定义cmp函数

`sort` 默认是从⼩到⼤排列的，也可以指定第三个参数 `cmp` 函数，然后⾃⼰定义⼀个 `cmp` 函数指定排序规则～ `cmp` 最好⽤的还是在结构体中，尤其是很多排序的题⽬～⽐如⼀个学⽣结构体 `stu` 有学号和成绩两个变量，要求如果成绩不同就按照成绩从⼤到⼩排列，如果成绩相同就按照学号从⼩到⼤排列，那么就可以写⼀个 `cmp` 数组实现这个看上去有点复杂的排序过程：

```c++
#include <iostream>
using namespace std;
struct stu { // 定义⼀个结构体stu，number表示学号，score表示分数
  int number;
  int score; 
}
bool cmp(stu a, stu b) { // cmp函数，返回值是bool，传⼊的参数类型应该是结构体stu类型
  if (a.score != b.score) // 如果学⽣分数不同，就按照分数从⼤到⼩排列
  	return a.score > b.score;
  else // 如果学⽣分数相同，就按照学号从⼩到⼤排列
  	return a.number < b.number; 
}
// 有时候这种简单的if-else语句我喜欢直接⽤⼀个C语⾔⾥⾯的三⽬运算符表示～
bool cmp(stu a, stu b) {
	return a.score != b.score ? a.score > b.score : a.number < b.number; 
}
```

注意： `sort` 函数的 `cmp` 必须按照规定来写，即必须只是 `>` 或者 `<` ，⽐如： `return a > b;` 或 者 `return a < b;` ⽽不能是 `<=` 或者 `>=` ，因为快速排序的思想中， `cmp` 函数是当结果为 `false` 的时候迭代器指针暂停开始交换两个元素的位置，当 `cmp` 函数 `return a <= b` 时，若中间元素前⾯的元素都⽐它⼩，⽽后⾯的元素都跟它相等或者⽐它⼩，那么 `cmp` 恒返回 `true` ，迭代器指针会不断右移导致程序越界，发⽣段错误～



### cctype头⽂件函数

刚刚在头⽂件那⼀段中也提到， `#include <cctype>` 本质上来源于C语⾔标准函数库中的头⽂件 `#include <ctype.h>` ，其实并不属于C++新特性的范畴，在刷PAT⼀些字符串逻辑题的时候也经常⽤到，但是很多⼈似乎不了解这个头⽂件中的函数，所以在这⾥单独提⼀下～

可能平时我们判断⼀个字符是否是字⺟，可能会写：

```c++
char c;
cin >> c;
if (c >= 'A' && c <= 'Z' || c >= 'a' && c <= 'z') {
	cout << "c is alpha"; 
}
```

但是在 `cctype` 中已经定义好了判断这些字符应该所属的范围，直接引⼊这个头⽂件并且使⽤⾥⾯的函数判断即可，⽆需⾃⼰⼿写（⾃⼰⼿写有时候可能写错或者漏写～）

```c++
#include <iostream>
#include <cctype>
using namespace std;
int main() {
  char c;
  cin >> c;
  if (isalpha(c)) {
  	cout << "c is alpha"; 
  }
  return 0; 
}
```

不仅仅能判断字⺟，还能判断数字、⼩写字⺟、⼤写字⺟等～C++官⽅⽂档中对这些函数归纳成了⼀个表格，我列出了官⽹的函数与所属范围总结表，有兴趣的可以看⼀下：https://www.liuchuo.net/archives/2999

总的来说常⽤的只有以下⼏个：

> `isalpha` 字⺟（包括⼤写、⼩写）
>
> `islower` （⼩写字⺟）
>
> `isupper` （⼤写字⺟）
>
> `isalnum` （字⺟⼤写⼩写+数字）
>
> `isblank` （space和 `\t` ）
>
> `isspace` （ space 、 `\t` 、 `\r` 、 `\n` ）

`cctype` 中除了上⾯所说的⽤来判断某个字符是否是某种类型，还有两个经常⽤到的函数： `tolower`和 `toupper` ，作⽤是将某个字符转为⼩写或者⼤写，这样就不⽤像原来那样⼿动判断字符c是否是⼤写，如果是⼤写字符就 `c = c + 32;` 的⽅法将 `char c` 转为⼩写字符啦～这在字符串处理的题⽬中也是经常⽤到：

```c++
char c = 'A';
char t = tolower(c); // 将c字符转化为⼩写字符赋值给t，如果c本身就是⼩写字符也没有关系～
cout << t; // 此处t为'a'
```





### C++11

C++11是2011年官⽅为C++语⾔带来的新语法新标准，C++11为C++语⾔带来了很多好⽤的新特性，⽐如 `auto` 、 `to_string()` 函数、 `stoi` 、 `stof` 、 `unordered_map` 、 `unordered_set` 之类的～现在⼤多数OJ都是⽀持C++11语法的，有些编译器在使⽤的时候需要进⾏⼀些设置才能使⽤C++11中的语法，否则可能会导致编译器上编译不通过⽆法运⾏，总之C++11的语法在OJ⾥⾯是可以使⽤的～⽽且很多语法很好⽤～以下讲解⼀些C++11⾥⾯常⽤的新特性～

#### atuo声明

`auto` 是C++11⾥⾯的新特性，可以让编译器根据初始值类型直接推断变量的类型。⽐如这样：

```c++
auto x = 100; // x是int变量
auto y = 1.5; // y是double变量
```

当然这个在算法⾥⾯最主要的⽤处不是这个，⽽是在STL中使⽤迭代器的时候， auto 可以代替⼀⼤⻓串的迭代器类型声明：

```c++
// 本来set的迭代器遍历要这样写：
for(set<int>::iterator it = s.begin(); it != s.end(); it++) {
		cout << *it << " "; 
}
// 现在可以直接替换成这样的写法：
for(auto it = s.begin(); it != s.end(); it++) {
		cout << *it << " "; 
}
```



#### 基于范围的for循环

除了像C语⾔的for语句 `for (i = 0; i < arr.size(); i++)` 这样，C++11标准还为C++添加了⼀种新的 `for` 循环⽅式，叫做基于范围（range-based）的for循环，这在遍历数组中的每⼀个元素时使⽤会⽐较简便～⽐如想要输出数组 `arr` 中的每⼀个值，可以使⽤如下的⽅式输出：

```c++
int arr[4] = {0, 1, 2, 3};
for (int i : arr)
	cout << i << endl; // 输出数组中的每⼀个元素的值，每个元素占据⼀⾏
```

`i` 变量从数组的第⼀个元素开始，不断执⾏循环， `i` 依次表示数组中的每⼀个元素～注意，使⽤ `int i` 的⽅式定义时，该语句只能⽤来输出数组中元素的值，⽽不能修改数组中的元素，如果想要修改，必须使⽤ `int &i` 这种定义引⽤变量的⽅式～⽐如想给数组中的每⼀个元素都乘以 2 ，可以使⽤如下⽅式：

```c++
int arr[4] = {0, 1, 2, 3};
for (int &i : arr) // i为引⽤变量
	i = i * 2; // 将数组中的每⼀个元素都乘以2，arr[4]的内容变为了{0, 2, 4, 6}
```

这种基于范围的 `for` 循环适⽤于各种类型的数组，将上述两段代码中的 `int` 改成其他变量类型如 `double` 、 `char` 都是可以的～另外，这种 `for` 循环⽅式不仅可以适⽤于数组，还适⽤于各种STL容器，⽐如 `vector` 、 `set` 等～加上上⾯⼀节所讲的C++11⾥⾯很好⽤的 `auto` 声明，将 `int` 、 `double` 等变量类型替换成 `auto` ，⽤起来就更⽅便啦～

```c++
// v是⼀个int类型的vector容器
for (auto i : v)
	cout << i << " ";
// 上⾯的写法等价于
for (int i = 0; i < v.size(); i++)
	cout << v[i] << " ";
```



#### to_string

`to_string` 的头⽂件是 `#include <string>` ， `to_string` 最常⽤的就是把⼀个 `int` 型变量或者⼀个数字转化为 `string` 类型的变量，当然也可以转 `double` 、 `float` 等类型的变量，这在很多PAT字符串处理的题⽬中很有⽤处，以下是示例代码：

```c++
#include <iostream>
#include <string>
using namespace std;
int main() {
  string s1 = to_string(123); // 将123这个数字转成字符串
  cout << s1 << endl;
  string s2 = to_string(4.5); // 将4.5这个数字转成字符串
  cout << s2 << endl;
  cout << s1 + s2 << endl; // 将s1和s2两个字符串拼接起来并输出
  printf("%s\n", (s1 + s2).c_str()); // 如果想⽤printf输出string，得加⼀个.c_str()
  return 0; 
}
```



#### stoi & stod

使⽤ `stoi` 、 `stod` 可以将字符串 `string` 转化为对应的 `int` 型、 `double` 型变量，这在字符串处理的很多问题中很有帮助～以下是示例代码和⾮法输⼊的处理⽅法：

```c++
#include <iostream>
#include <string>
using namespace std;
int main() {
  string str = "123";
  int a = stoi(str);
  cout << a;
  str = "123.44";
  double b = stod(str);
  cout << b;
  return 0; 
}
```

stoi如果遇到的是⾮法输⼊（⽐如stoi("123.4")，123.4不是⼀个int型变量）：

1. 会⾃动截取最前⾯的数字，直到遇到不是数字为⽌(所以说如果是浮点型，会截取前⾯的整数部分)

2. 如果最前⾯不是数字，会运⾏时发⽣错误



stod如果是⾮法输⼊：

1. 会⾃动截取最前⾯的浮点数，直到遇到不满⾜浮点数为⽌

2. 如果最前⾯不是数字或者⼩数点，会运⾏时发⽣错误

3. 如果最前⾯是⼩数点，会⾃动转化后在前⾯补0



不仅有stoi、stod两种，相应的还有：

> `stof` (string to float)
>
> `stold` (string to long double)
>
> `stol` (string to long)
>
> `stoll` (string to long long)
>
> `stoul` (string to unsigned long)
>
> `stoull` (string to unsigned long long)





#### Dev-Cpp

如果想要在 Dev-Cpp ⾥⾯使⽤C++11特性的函数，⽐如刷算法中常⽤的 `stoi` 、 `to_string` 、 `unordered_map` 、 `unordered_set` 、 `auto` 这些，需要在设置⾥⾯让dev⽀持C++11，需要在菜单栏中⼯具-编译选项-编译器-编译时加⼊ -std=c++11 这句命令即可～

