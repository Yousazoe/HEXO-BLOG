---
title: LeetCode刷题记录
comment: false
tags:
  - Cpp
  - LeetCode
  - Algorithm
  - Online Judge
categories: LeetCode题解 (LeetCode Solution)
abbrlink: ba8c707b
top: 2
date: 2021-02-26 13:16:45
banner_img:
index_img:
translate_title:
mathjax: true
---



![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/beb27864152259.5ac8b75847ad9-20210303093009942.jpg)

<div align=center>
  <font size="3">
    <i>
      <a href="https://www.behance.net/gallery/64152259/Keyclack-posters">Keyclack posters</a> by 
      <a href="https://www.behance.net/MChahin">Mohamed Chahin</a>
    </i>
  </font>
</div>





### 引言

力扣提供海量题库，帮助你高效提升编程技能，轻松拿下世界 IT 名企 Dream Offer。本文作为博主的LeetCode刷题记录，包含基于C++的解题思路与完整代码以供参考学习。

<!--more-->



> 来源：力扣（LeetCode）
> 链接：https://leetcode-cn.com
> 著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。



### 两数之和

给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出 **和为目标值** 的那 **两个** 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。

你可以按任意顺序返回答案。

#### 示例 1

```
输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
```

#### 示例 2

```
输入：nums = [3,2,4], target = 6
输出：[1,2]
```

#### 示例 3

```
输入：nums = [3,3], target = 6
输出：[0,1]
```

#### 提示

+ 2 <= nums.length <= 103
+ $-10^9$ <= nums[i] <= $10^9$
+ $-10^9$ <= target <= $10^9$
+ 只会存在一个有效答案

#### 默认模板

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {

    }
};
```

#### 题解

##### 暴力枚举

这道题很像AOJ中的一道题，那时候我就用的这种二次循环的遍历方式枚举每一种情况。需要注意到每一个位于 `x` 之前的元素都已经和 `x` 匹配过，因此不需要再进行匹配。而每一个元素不能被使用两次，所以我们只需要在 `x` 后面的元素中寻找 `target - x`。

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> v(2);

        for(int i = 0;i < nums.size();i++){
            for(int j = i + 1;j < nums.size();j++){
                if(nums[i] + nums[j] == target){
                    v[0] = i;
                    v[1] = j;
                    return v;
                }
            }
        }
        return v;
    }
};
```



### 两数相加

给你两个 **非空** 的链表，表示两个非负的整数。它们每位数字都是按照 **逆序** 的方式存储的，并且每个节点只能存储 **一位** 数字。

请你将两个数相加，并以相同形式返回一个表示和的链表。

你可以假设除了数字 0 之外，这两个数都不会以 0 开头。

#### 示例1

![](https://cdn.jsdelivr.net/gh/Yousazoe/picgo-repo/img/addtwonumber1.jpg)

<br/>

```
输入：l1 = [2,4,3], l2 = [5,6,4]
输出：[7,0,8]
解释：342 + 465 = 807.
```

#### 示例 2

```
输入：l1 = [0], l2 = [0]
输出：[0]
```

#### 示例 3

```
输入：l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
输出：[8,9,9,9,0,0,0,1]
```

#### 提示

+ 每个链表中的节点数在范围 `[1, 100]` 内
+ `0 <= Node.val <= 9`
+ 题目数据保证列表表示的数字不含前导零



#### 模板

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {

    }
};
```





#### 题解

这道题涉及到了链表的知识。我一开始的想法是先把链表遍历导出到比较方便访问的数据结构比如`vector`然后再倒置最后相加，后面开始写伪代码的时候困难重重，比较难实现所以就放弃了这个思路。

之后参考了精选解题的思路，对于两个链表节点个数不同的情况我们可以选择将节点数较小的那个表补零，比如`l1=[2,0,4,3]`、`l2=[5,6,8]`，此时`l2`少一个节点，那么我们就可以对`l2`补零为`[5,6,8,0]`使之节点数相同。

```c++
int len1 = 0,len2 = 0;
ListNode* p = l1;
ListNode* q = l2;

while(p->next != NULL){
  len1++;
  p = p->next;
}

while(q->next != NULL){
  len2++;
  q = q->next;
}

ListNode* zero = len1 > len2 ? q : p;
for(int i = 0;i < len1 - len2;i++){
  zero->next = new ListNode(0);
  zero = zero->next;
}
```

在`l1`与`l2`位数相同后该考虑的就是相加的问题，这个其实就简单很多了，设置一个用于进位的`carry`负责下一位的进制，而对于输出的链表`l3`而言`sum%10`就是它在该位置上的值。



```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int len1 = 0,len2 = 0;
        ListNode* p = l1;
        ListNode* q = l2;
        
        while(p->next != NULL){
            len1++;
            p = p->next;
        }

        while(q->next != NULL){
            len2++;
            q = q->next;
        }

        ListNode* zero = len1 > len2 ? q : p;
        for(int i = 0;i < len1 - len2;i++){
            zero->next = new ListNode(0);
            zero = zero->next;
        }

        p = l1;
        q = l2;
        int carry = 0,sum = 0;
        ListNode* l3 = new ListNode(0);
        ListNode* r = l3;

        while(p != NULL && q != NULL){
            sum = carry + p->val + q->val;
            r->next = new ListNode(sum%10);
            carry = sum >= 10 ? 1 : 0;
            r = r->next;
            p = p->next;
            q = q->next;
        }

        return l3;
    }
};
```



然而满怀欣喜的提交后倒在了**1138** 样例中，大家不妨先不往下翻，先带入该样例看看哪里出了问题。

```
输入：
[2,4,9]
[5,6,4,9]
输出：
[7,0,4,1]
预期：
[7,0,4,0,1]
```

一检查源码问题可太多了：

+ 补零没有使用绝对值函数`abs()`，导致如果`len1<len2`不会补零而实际上我们需要补零
+ 没有考虑最后一位的情况，如果还有进制会导致结果出错（少一个最高位位的1）
+ 结果输出实际上是从`l3->next`开始的，最初始的节点并没有派上用场



```diff
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int len1 = 0,len2 = 0;
        ListNode* p = l1;
        ListNode* q = l2;
        
        while(p->next != NULL){
            len1++;
            p = p->next;
        }

        while(q->next != NULL){
            len2++;
            q = q->next;
        }

        ListNode* zero = len1 > len2 ? q : p;
-       for(int i = 0;i < len1 - len2;i++){
+       for(int i = 0;i < abs(len1 - len2);i++){
            zero->next = new ListNode(0);
            zero = zero->next;
        }

        p = l1;
        q = l2;
        int carry = 0,sum = 0;
        ListNode* l3 = new ListNode(0);
        ListNode* r = l3;

        while(p != NULL && q != NULL){
            sum = carry + p->val + q->val;
            r->next = new ListNode(sum%10);
            carry = sum >= 10 ? 1 : 0;
            r = r->next;
            p = p->next;
            q = q->next;
        }
+        if(carry){
+            r->next = new ListNode(1);
+            r = r->next;
+        }

-        return l3;
+        return l3->next;
    }
};
```



### 无重复字符的最长子串

给定一个字符串，请你找出其中不含有重复字符的 **最长子串** 的长度。

#### 示例 1

```
输入: s = "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

#### 示例 2

```
输入: s = "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```

#### 示例 3

```
输入: s = "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```

#### 示例 4

```
输入: s = ""
输出: 0
```

#### 提示

+ 0 <= s.length <= $5 * 10^4$
+ `s` 由英文字母、数字、符号和空格组成



#### 默认模板

```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {

    }
};
```

#### 题解

本题属于典型的滑动窗口问题，这类问题的逻辑基本上是这样：

```c++
int left = 0,right = 0;

while(right < s.size()){
  window.add(s[right]);
  right++;
  
  while(window needs shrink){
    window.remove(s[left]);
    left++;
  }
}
```

因为左右指针只遍历字符串一次，所以时间复杂度为$O(N)$，比字符串暴力算法要高效的多。对上面的逻辑再加以整理，labuladong总结出一套滑动算法的代码框架：

```c++
void slidingWindow(string s){
  unordered_map<char,int> window;
  
  int left = 0,right = 0;
  while(right < s.size()){
    char c = s[right];
    right++;
    
    ......
    
    while(window needs shrink){
      char d = s[left];
      left++;
      
      ......
    }  
  }
}
```

其中两处`...`表示更新窗口数据的地方，我们只需要在这里填入具体的窗口数据更新的逻辑即可，而且右移和左移的操作是完全对称的。

回到本题，很显然当`window[c]`的值大于1时窗口存在重复的字符，不满足题目要求，移动`left`缩小窗口。比较难理解的是`res = max(res,right - left);`，我们可以理解为一种另类的求最大值，虽然指针在不断滑动，但`res`与`right-left`求最大值保证了之前的最大值与现在可能超过的长度进行比较从而得出我们需要的最长子串。如果还有疑问或者不理解可以带入下面的求解过程体会：

```
(a)bcabcbb
(ab)cabcbb
(abc)abcbb
abc(a)bcbb
abc(ab)cbb
abc(abc)bb
abcabc(b)b
abcabcb(b)
```

最后完整源码如下：

```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_map<char,int> window;
        int left = 0,right = 0;
        int res = 0;

        for(int i = 0;i < s.size();i++){
            char c = s[right++];
            window[c]++;

            while(window[c] > 1){
                char d = s[left++];
                window[d]--;
            }

            res = max(res,right - left);
        }

        return res;
    }
};
```



### [未解决]寻找两个正序数组的中位数

给定两个大小分别为 m 和 n 的正序（从小到大）数组 nums1 和 nums2。请你找出并返回这两个正序数组的 中位数 。

 

#### 示例 1

```
输入：nums1 = [1,3], nums2 = [2]
输出：2.00000
解释：合并数组 = [1,2,3] ，中位数 2
```


#### 示例 2

```
输入：nums1 = [1,2], nums2 = [3,4]
输出：2.50000
解释：合并数组 = [1,2,3,4] ，中位数 (2 + 3) / 2 = 2.5
```

#### 示例 3

```
输入：nums1 = [0,0], nums2 = [0,0]
输出：0.00000
```

#### 示例 4

```
输入：nums1 = [], nums2 = [1]
输出：1.00000
```

#### 示例 5

```
输入：nums1 = [2], nums2 = []
输出：2.00000
```

#### 提示

+ `nums1.length == m`
+ `nums2.length == n`
+ 0 <= m <= 1000
+ 0 <= n <= 1000
+ 1 <= m + n <= 2000
+ $-10^6$ <= nums1[i], nums2[i] <= $10^6$


进阶：你能设计一个时间复杂度为 O(log (m+n)) 的算法解决此问题吗？



#### 默认模板

```c++
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {

    }
};
```



#### 题解







### 最长回文子串

给你一个字符串 s，找到 s 中最长的回文子串。

#### 示例 1

```
输入：s = "babad"
输出："bab"
解释："aba" 同样是符合题意的答案。
```

#### 示例 2

```
输入：s = "cbbd"
输出："bb"
```

#### 示例 3

```
输入：s = "a"
输出："a"
```

#### 示例 4

```
输入：s = "ac"
输出："a"
```

#### 提示

+ 1 <= s.length <= 1000
+ s 仅由数字和英文字母（大写和/或小写）组成

#### 默认模板

```c++
class Solution {
public:
    string longestPalindrome(string s) {

    }
};
```

#### 题解

本题要求我们求出字符串中回文子串中长度最长的一个子串。

我们可以举两个回文串`aa`、`babab`来理解题目，首先回文串有`a`、`b`、`aa`、`bab`、`aba`、`babab`，可以观察到回文串有奇数和偶数两种情况，并且由于回文串对称的特性，我们应该不断判断字符串左右是否相同以保持这个对称的特性。

基于此我们可以先写出这个判断函数，内容就是以某个点为中心向左右两边发散，判断是否为回文串并返回最小的回文子串：

```c++
string traceMid2Side(string s,int left,int right){
  while(left >= 0 && right <= s.length() - 1 && s[left] == s[right]){
				left--;
        right++;
  }
	return s.substr(left + 1,right - left - 1);
}
```

命令第一个元素为最后返回的结果`res`，如果没有第一个元素返回空字符串。之后遍历字符串，按刚才依次从中间向左右寻找是否有回文子串以临时变量`tmp`储存，并比较与`res`的长度。

两次调用`traceMid2Side()`是考虑到之前提到的奇偶问题，奇数情况左右都是`i`，偶数情况左边是`i`右边是`i+1`：

```c++
class Solution {
public:
    string longestPalindrome(string s) {
        int len = s.length();
        if(len == 0) return "";
        string res = s.substr(0,1);
        
        for(int i = 0;i <= len - 2;i++){
            string tmp = traceMid2Side(s,i,i);
            if(tmp.length() > res.length())
                res = tmp;

            tmp = traceMid2Side(s,i,i + 1);
            if(tmp.length() > res.length())
                res = tmp;
        }
        return res;
    }

    string traceMid2Side(string s,int left,int right){
        while(left >= 0 && right <= s.length() - 1 && s[left] == s[right]){
            left--;
            right++;
        }
        return s.substr(left + 1,right - left - 1);
    }
};
```



### Z 字形变换

将一个给定字符串 `s` 根据给定的行数 `numRows` ，以从上往下、从左到右进行 Z 字形排列。

比如输入字符串为 `"PAYPALISHIRING"` 行数为 `3` 时，排列如下：

```
P   A   H   N
A P L S I I G
Y   I   R
```


之后，你的输出需要从左往右逐行读取，产生出一个新的字符串，比如：`"PAHNAPLSIIGYIR"`。

请你实现这个将字符串进行指定行数变换的函数：

```c++
string convert(string s, int numRows);
```



#### 示例 1

```
输入：s = "PAYPALISHIRING", numRows = 3
输出："PAHNAPLSIIGYIR"
```



#### 示例 2

```
输入：s = "PAYPALISHIRING", numRows = 4
输出："PINALSIGYAHRPI"
解释：
P     I    N
A   L S  I G
Y A   H R
P     I
```


#### 示例 3

```
输入：s = "A", numRows = 1
输出："A"
```

#### 提示

+ 1 <= s.length <= 100
+ `s` 由英文字母（小写和大写）、`','` 和 `'.'` 组成
+ 1 <= numRows <= 1000



#### 默认模板

```c++
class Solution {
public:
    string convert(string s, int numRows) {

    }
};
```



#### 题解





### 整数反转

给你一个 32 位的有符号整数 x ，返回 x 中每位上的数字反转后的结果。

如果反转后整数超过 32 位的有符号整数的范围 [−231,  231 − 1] ，就返回 0。

假设环境不允许存储 64 位整数（有符号或无符号）。

#### 示例 1

```
输入：x = 123
输出：321
```

#### 示例 2

```
输入：x = -123
输出：-321
```

#### 示例 3

```
输入：x = 120
输出：21
```

#### 示例 4

```
输入：x = 0
输出：0
```

#### 提示

+ $-2^{31}$ <= x <= $2^{31} - 1$



#### 默认模板

```c++
class Solution {
public:
    int reverse(int x) {

    }
};
```

#### 题解