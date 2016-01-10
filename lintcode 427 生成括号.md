#lintcode 427 生成括号

---
layout: post
category : lintcode
tagline: "lintcode"
tags : [lintcode]
excerpt: 。
---
{% include JB/setup %}

** 题目 **
题目链接：http://www.lintcode.com/zh-cn/problem/generate-parentheses/

给定 n 对括号，请写一个函数以将其生成新的括号组合，并返回所有组合结果。

样例
给定 n = 3, 可生成的组合如下:

"((()))", "(()())", "(())()", "()(())", "()()()"


** 解题报告 **

RMQ问题，可以选择使用线段树解决，但是没必要那么麻烦，所以就是简单的建立一个区间，然后求一个最大值即可。


** Source Code / C++ **

```C++

class Solution {
public:
    /**
     * @param n n pairs
     * @return All combinations of well-formed parentheses
     */
    vector<string> generateParenthesis(int n) {
        // Write your code here
        vector <string> ret;
        generate(n, n, "", ret);
        return ret;
    }
    void generate(int leftnum, int rightnum, string s, vector<string> &ret) {
        
        if(leftnum == 0 && rightnum ==0) {
            ret.push_back(s);
        }
        
        if(leftnum > 0) {
            generate(leftnum-1, rightnum, s+'(', ret);
        }
        
        if(rightnum >0 && leftnum < rightnum) {
            generate(leftnum, rightnum-1, s+')', ret);
        }
        
        return;
    }
};

```