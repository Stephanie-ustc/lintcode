#lintcode 212 空格替换

---
layout: post
category : lintcode
tagline: "lintcode"
tags : [lintcode]
excerpt: 

---
{% include JB/setup %}

##题目

题目链接：http://www.lintcode.com/zh-cn/problem/space-replacement/

##解题报告



##Source Code / C++
 
```C++

class Solution {
public:
    /**
     * @param string: An array of Char
     * @param length: The true length of the string
     * @return: The true length of new string
     */
    int replaceBlank(char string[], int length) {
        // Write your code here
        if( !length) return 0;
        int spaces_num = 0;
        for(int i=0; i <length; ++i) {
            if(string[i] == ' ') {
                ++ spaces_num;
            }
        }
        
        if( !spaces_num ) return length;
        
        int newlen = length + spaces_num * 2;
        int pn = newlen -1; int p= length -1;
        while(p >=0 && pn >=0) {
            if(string[p] == ' ') {
                string[pn] ='0';
                string[--pn] ='2';
                string[--pn] ='%';
                
            } else {
                string[pn] = string[p];
                
            }
            --pn;
            --p;
        }
        
        return newlen;
    }
};  

```