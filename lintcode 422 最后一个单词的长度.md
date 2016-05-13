#422 最后一个单词的长度

---
layout: post
category : lintcode
tagline: "lintcode"
tags : [lintcode]
excerpt: 

---
{% include JB/setup %}

##题目

题目链接：http://www.lintcode.com/zh-cn/problem/submatrix-sum/
给定一个字符串， 包含大小写字母、空格' '，请返回其最后一个单词的长度。
如果不存在最后一个单词，请返回 0 。
注意事项

一个单词的界定是，由字母组成，但不包含任何的空格。

样例
给定 s = "Hello World"，返回 5。

##解题报告



##Source Code / C++ 

```C++
class Solution {
public:
    /**
     * @param s A string
     * @return the length of last word
     */
    int lengthOfLastWord(string& s) {
        // Write your code here
        int retlent = 0;
        for( int i = 0; i< s.size(); ++i) {
            if(s[i] ==' ') {
                retlent= 0 ;
            }
            else{
                retlent++;
            }
        }
        return retlent;
    }
};

```