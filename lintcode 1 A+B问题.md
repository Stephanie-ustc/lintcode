#lintcode 1 A + B 问题

---
layout: post
category : lintcode
tagline: "lintcode"
tags : [lintcode]
excerpt: 

---
{% include JB/setup %}

##题目

题目链接：http://www.lintcode.com/zh-cn/problem/a-b-problem/

##解题报告

不适用加法的 加运算实现，位运算。

##Source Code / C++
 
```C++

class Solution {
public:
    /*
     * @param a: The first integer
     * @param b: The second integer
     * @return: The sum of a and b
     */
    int aplusb(int a, int b) {
        // write your code here, try to do it without arithmetic operators.
         while(b !=0) {
             int carry = a&b;
             a ^=b;
             b = carry << 1;
         }
         return a;
    }
};

```