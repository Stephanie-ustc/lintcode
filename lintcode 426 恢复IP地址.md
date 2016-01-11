#lintcode 426 恢复IP地址

---
layout: post
category : lintcode
tagline: "lintcode"
tags : [lintcode]
excerpt: 

---
{% include JB/setup %}

** 题目 **
题目链接：http://www.lintcode.com/zh-cn/problem/restore-ip-addresses/

给一个由数字组成的字符串。求出其可能恢复为的所有IP地址。

样例
给出字符串 "25525511135"，所有可能的IP地址为：

[
  "255.255.11.135",
  "255.255.111.35"
]
（顺序无关紧要）



** 解题报告 **

递归问题，主要在于判断Ip是否合法。

** Source Code / C++ **

```C++

class Solution {
public:
    /**
     * @param s the IP string
     * @return All possible valid IP addresses
     */
    
    vector<string> ret;
    void restore(string& s, int curIp, int n, vector<string> ipN) {
        ipN.push_back("");
        //递归条件
        if(curIp == 4 && n == s.size()) {
            //判断ip是否合法
            for(int i=0; i<4; ++i) {
                //是否存在以0开头
                if(ipN[i][0] == '0' && ipN[i].size() > 1) return;
                //是否在0-255之间
                stringstream ss;
                int tmp;
                ss << ipN[i];
                ss >> tmp;
                if(tmp<0 || tmp > 255) return;
            }
            //ip合法
            string ans ="";
            ans += ipN[0];
            for(int i=1; i<4;++i) {
                ans += "." + ipN[i];
            }
            ret.push_back(ans);
            return;
        }
        //递归条件
        if(n>=s.size() || curIp >= 4) return;
        for(int i=1;i<=3; ++i) {
            if(n+i > s.size()) break;
            ipN[curIp] +=s[n+i-1];
            //ipN[curIp+1] = "";
            restore(s, curIp+1, n+i, ipN);
        }
    }
    vector<string> restoreIpAddresses(string& s) {
        // Write your code here
        vector<string> ipN;

        restore(s, 0, 0, ipN);
        return ret;
    }
};

```