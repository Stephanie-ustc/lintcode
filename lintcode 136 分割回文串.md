#lintcode 136 分割回文串

---
layout: post
category : lintcode
tagline: "lintcode"
tags : [lintcode]
excerpt: 

---
{% include JB/setup %}

##题目

题目链接：http://www.lintcode.com/zh-cn/problem/palindrome-partitioning/

##解题报告

简单递归应用

##Source Code / C++ 

```C++

class Solution {
public:
    /**
     * @param s: A string
     * @return: A list of lists of string
     */
    vector< vector<string> > ret;
    vector<vector<string>> partition(string s) {
        // write your code here
        vector<string> res;
        findPar(s, res);
        return ret;
    }
    void findPar(string s, vector<string> res) {
        if(s.empty()) {
            ret.push_back(res);
            return;
        }
        for(int i =1; i<=s.size(); ++i) {
            string str = s.substr(0,i);
            if( isPar( str ) ) {
                res.push_back(str);
                findPar(s.substr(i, s.size() - i), res);
                res.pop_back();
            }
        }
        
    }
    bool isPar(string s) {
        int len = s.length()-1;
        int index =0;
        while(index < len) {
            if(s[index] != s[len]) {
                return false;
            }
            index ++;
            len --;
        }
        return true;
    }
};

```