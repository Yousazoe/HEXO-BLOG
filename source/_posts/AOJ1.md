---
title: Algorithms and Data Structures I
comment: false
tags:
  - Algorithm
  - AOJ
  - Online Judge
  - Cpp
categories: 会津大学在线测评 (Aizu Online Judge)
abbrlink: ff860a3b
mathjax: ture
date: 2021-03-01 09:06:36
type:
banner_img:
index_img:
translate_title:
top: 1
---



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/2c6a8066350161.5b14609dc369c.png)

<div align=center>
  <font size="3">
    <i>
      <a href="https://www.behance.net/gallery/66350161/Vintage-80s-office">Vintage 80s office</a> by 
      <a href="https://www.behance.net/MChahin">Mohamed Chahin</a>
    </i>
  </font>
</div>



### 引言

Acquire fundamental elements of algorithms and data structures.

<!--more-->



### Topic #1 Getting Started

#### ALDS1_1_A Insertion Sort

> Time Limit : `1 sec` , Memory Limit : `131072 KB` 

Write a program of the Insertion Sort algorithm which sorts a sequence A in ascending order. The algorithm should be based on the following pseudocode:

```c++
for i = 1 to A.length-1
    key = A[i]
    /* insert A[i] into the sorted sequence A[0,...,j-1] */
    j = i - 1
    while j >= 0 and A[j] > key
        A[j+1] = A[j]
        j--
    A[j+1] = key
```

Note that, indices for array elements are based on 0-origin.

To illustrate the algorithms, your program should trace intermediate result for each step.

##### Input

The first line of the input includes an integer N, the number of elements in the sequence.

In the second line, *N* elements of the sequence are given separated by a single space.

##### Output

The output consists of *N* lines. Please output the intermediate sequence in a line for each step. Elements of the sequence should be separated by single space.

##### Constraints

1 ≤ *N* ≤ 100

##### Sample Input 1

```
6
5 2 4 6 1 3
```

##### Sample Output 1

```
5 2 4 6 1 3
2 5 4 6 1 3
2 4 5 6 1 3
2 4 5 6 1 3
1 2 4 5 6 3
1 2 3 4 5 6
```

##### Sample Input 2

```
3
1 2 3
```

##### Sample Output 2

```
1 2 3
1 2 3
1 2 3
```

##### 問題を解く

###### 算法原理

本题要求我们实现插入排序算法并输出升序排列过程。在插入排序的过程中，会将整体数组分成“已排序部分”和“未排序部分”，题目中已经给出了插入排序的伪代码，我们可以先翻译一下整个排序过程：

```
将开头元素视为已排序
执行下述处理，直至未排序部分消失：
	1. 取出未排序部分的开头元素赋给变量v
	2. 在已排序的部分，将所有比v大的元素向后移一个单位
	3. 将已取出的元素v插入空格
```

如果这段话不是很好理解，我们可以用下图来阐释排序的整个过程：

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/insertionSort.gif)

再举个例子，我们对数组`A={8,3,1,5,2,1}`进行插入排序时，整体流程如下：

```
	 0 1 2 3 4 5
0: 8 3 1 5 2 1
1: 3 8 1 5 2 1
2: 1 3 8 5 2 1
3: 1 3 5 8 2 1
4: 1 2 3 5 8 1
5: 1 1 2 3 5 8
```

在步骤1中，将开头元素`A[0]`（=8）视为已排序，所以我们去除`A[1]`的3，将其插入已排序部分的恰当位置。首先把原先位于`A[0]`的8移动至`A[1]`，再把3插入`A[0]`。这样一来，开头2个元素就完成了排序。

在步骤2中，我们要把`A[2]`的1插入恰当位置。这里首先将比1大的`A[1]`（=8）和`A[0]`（=3）顺次向后移一个位置，然后把1插入`A[0]`。

在步骤3中，我们要把`A[3]`的5插入恰当位置。这次将比5大的`A[2]`（=8）向后移一个位置，然后把5插入`A[2]`。

之后同理，将已排序部分的其中一段向后移动，再把未排序部分的开头元素插入已排序部分的恰当位置。插入排序的特点在于，只要0到第i号元素全部排入已排序部分，那么无论后面如何插入，这个0到第i号的元素将永远保持排序完毕的状态。



###### 代码实现

回到代码实现，首先我们先将主函数的输入部分和单独的输出部分`trace()`函数写出来：

```c++
#include <iostream>
using namespace std;

void trace(int arr[],int n){
    for (int i = 0; i < n; ++i) {
        if (i == 0)
            cout << arr[i];
        else
            cout << " " << arr[i];
    }
    cout << endl;
}

int main(){
    int n;
    cin >> n;
    int arr[n];
    for (int i = 0; i < n; ++i) {
        cin >> arr[i];
    }

    return 0;
}
```

准备工作完成后开始写`insertionSort()`插入排序的函数：

+ `i`：循环变量，表示未排序部分的开头元素
+ `key`：临时保存`arr[i]`值的变量
+ `j`：循环变量，用于在已排序部分寻找`key`的插入位置



```c++
void insertionSort(int arr[],int n){
    int j,key;

    for (int i = 0; i < n; ++i) {
        key = arr[i];

        j = i - 1;
        while (j >= 0 && arr[j] > key){
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
        trace(arr,n);
    }
}
```

外层循环的`i`自增。在每次循环开始时，将`arr[i]`的值临时保存在变量`key`中。

接下来是内部循环。我们要从已排序的部分找出比`key`大的元素并让它们顺次后移一个位置。这里我们让`j`从`i-1`开始向前自减，同时将比`key`大的元素从`arr[j]`移动到`arr[j+1]`。一旦`j`等于-1或当前`arr[j]`小于等于`key`则结束循环，并将`key`插入当前`j+1`的位置。



```c++
#include <iostream>
using namespace std;

void trace(int arr[],int n){
    for (int i = 0; i < n; ++i) {
        if (i == 0)
            cout << arr[i];
        else
            cout << " " << arr[i];
    }
    cout << endl;
}

void insertionSort(int arr[],int n){
    int j,key;

    for (int i = 0; i < n; ++i) {
        key = arr[i];

        j = i - 1;
        while (j >= 0 && arr[j] > key){
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
        trace(arr,n);
    }
}


int main(){
    int n;
    cin >> n;
    int arr[n];
    for (int i = 0; i < n; ++i) {
        cin >> arr[i];
    }

    insertionSort(arr,n);

    return 0;
}
```



###### 注意点

+ 数组长度是否足够长
+ 是否搞错了0起点和1起点的数组下标
+ 是否误用了循环变量（比如`i`、`j`）
+ 是否输出了多余的空格或换行



###### 思考

在插入排序中，我们只将比`key`（取出的值）大的元素向后平移，不相邻的元素不会直接交换位置，因此整个排序算法十分稳定。

然后我们考虑一下插入排序算法的复杂度。这里需要估算每个`i`循环中`arr[j]`元素向后移动的次数。最坏情况下，每个`i`循环都需要执行`i`次移动，总共需要$1+2+...+N-1=(N^2-N)/2$次移动，即算法复杂度为$O(N^2)$。

插入排序是一种很有趣的算法，输入数据的顺序能大幅影响它的复杂度。我们前面说它的复杂度为$O(N^2)$，也仅是指输入数据为降序排列的情况。如果输入数据为升序排列，那么`arr[j]`从头到尾都不需要移动，程序仅需要经历`N`次比较便可执行完毕。可见，插入排序法的优势在于能快速处理相对有序的数据。



#### ALDS1_1_B Common Divisor Greatest

> Time Limit : `1 sec` , Memory Limit : `131072 KB` 

Write a program which finds the greatest common divisor of two natural numbers *a* and *b*

##### Input

*a* and *b* are given in a line sparated by a single space.

##### Output

Output the greatest common divisor of *a* and *b*.

##### Constrants

1 ≤ *a*, *b* ≤ 109

##### Hint

You can use the following observation:

For integers *x* and *y*, if *x* ≥ *y*, then gcd(*x*, *y*) = gcd(*y*, *x*%*y*)

##### Sample Input 1

```
54 20
```

##### Sample Output 1

```
2
```

##### Sample Input 2

```
147 105
```

##### Sample Output 2

```
21
```



##### 問題を解く





#### ALDS1_1_C Prime Numbers

> Time Limit : `1 sec` , Memory Limit : `131072 KB`  

A prime number is a natural number which has exactly two distinct natural number divisors: 1 and itself. For example, the first four prime numbers are: 2, 3, 5 and 7.

Write a program which reads a list of *N* integers and prints the number of prime numbers in the list.

##### Input

The first line contains an integer *N*, the number of elements in the list.

*N* numbers are given in the following lines.

##### Output

Print the number of prime numbers in the given list.

##### Constraints

1 ≤ *N* ≤ 10000

2 ≤ *an element of the list* ≤ 108

##### Sample Input 1

```
5
2
3
4
5
6
```

##### Sample Output 1

```
3
```

##### Sample Input 2

```
11
7
8
9
10
11
12
13
14
15
16
17
```

##### Sample Output 2

```
4
```



##### 問題を解く





#### ALDS1_1_D Maximum Profit

> Time Limit : `1 sec` , Memory Limit : `131072 KB`

You can obtain profits from foreign exchange margin transactions. For example, if you buy 1000 dollar at a rate of 100 yen per dollar, and sell them at a rate of 108 yen per dollar, you can obtain (108 - 100) × 1000 = 8000 yen.

Write a program which reads values of a currency $R_t$ at a certain time tt (t=0,1,2,...n−1), and reports the maximum value of $R_j−R_i$ where $j>i$ .

##### Input

The first line contains an integer nn. In the following nn lines, RtRt (t=0,1,2,...n−1t=0,1,2,...n−1) are given in order.

##### Output

Print the maximum value in a line.

##### Constraints

- 2≤n≤200,000
- 1≤$R_t$≤$10^9$

##### Sample Input 1

```
6
5
3
1
3
4
3
```

##### Sample Output 1

```
3
```

##### Sample Input 2

```
3
4
3
2
```

##### Sample Output 2

```
-1
```



##### 問題を解く



### Topic #2 Sort I

#### ALDS1_2_A Bubble Sort





問題を解く

###### 算法原理

本题要求我们实现冒泡排序算法并输出升序排列过程。与插入排序一样，冒泡排序的各个计算步骤中，数组也分成“已排序部分”和“未排序部分”。题目中已经给出了插入排序的伪代码，我们可以先翻译一下整个排序过程：

```
重复执行下述处理，直到数组中不包含顺序相反的相邻元素：
	从数组末尾开始依次比较相邻两个元素，如果大小关系相反则交换位置
```

如果这段话不是很好理解，我们可以用下图来阐释排序的整个过程：



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/bubbleSort.gif)





###### 代码实现



```c++
#include <iostream>
using namespace std;


int bubbleSort(int arr[],int n){
    int count = 0,flag = 1;

    for (int i = 0; flag; ++i) {
        flag = 0;

        for (int j = n - 1; j >= i + 1; --j) {
            if (arr[j] < arr[j - 1]){
                swap(arr[j],arr[j - 1]);
                flag = 1;
                count++;
            }
        }
    }
    return count;
}


int main(){
    int n;
    cin >> n;
    int arr[n];
    for (int i = 0; i < n; ++i) {
        cin >> arr[i];
    }

    int res = bubbleSort(arr,n);
    for (int i = 0; i < n; ++i) {
        if (i) cout << " ";
        cout << arr[i];
    }
    cout << endl;
    cout << res << endl;

    return 0;
}
```



###### 思考

冒泡排序仅对数组中的相邻元素进行比较和交换，因此键相同的元素不会改变顺序。所以冒泡排序也属于一种稳定排序的算法。但要注意的是，一旦将比较运算`arr[j] < arr[j - 1]`改为`arr[j] <= arr[j - 1]`，算法就会失去稳定性。

然后我们来考虑一下冒泡排序的复杂度。假设数据总量为`N`，冒泡排序需对未排序部分的相邻元素进行$(N-1)+(N-2)+...+1=(N^2-N)/2$次比较。也就是说，冒泡排序在最坏的情况下需要进行$(N^2-N)/2$次比较运算，算法复杂度数量级为$O(N^2)$。

顺便一提，冒泡排序中的交换次数又称为反序数或逆序数，可用于体现数列的错乱程度。

