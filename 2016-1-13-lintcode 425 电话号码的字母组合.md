#lintcode 425 电话号码的字母组合

---
layout: post
category : lintcode
tagline: "lintcode"
tags : [lintcode]
excerpt: 

---
{% include JB/setup %}

##题目

题目链接：http://www.lintcode.com/zh-cn/problem/letter-combinations-of-a-phone-number/

##解题报告

递归DFS 

##Source Code / C++
 
```C++

class Solution {
public:
    /**
     * @param digits A digital string
     * @return all posible letter combinations
     */
    map< char, string > phone;
    vector<string> ret;
    vector<string> letterCombinations(string& digits) {
        // Write your code here
        if(digits.empty()) return ret;
        phone.insert( make_pair('0',"") );
        phone.insert( make_pair('1',"") );
        phone.insert( make_pair('2',"abc") );
        phone.insert( make_pair('3',"def") );
        phone.insert( make_pair('4',"ghi") );
        phone.insert( make_pair('5',"jkl") );
        phone.insert( make_pair('6',"mno") );
        phone.insert( make_pair('7',"pqrs") );
        phone.insert(make_pair('8',"tuv") );
        phone.insert(make_pair('9',"wxyz") );
        string res;
        dfs(digits, 0 , res);
        return ret;
    }
    void dfs(string& digits, int index, string res){
        if(index == digits.size()) {
            ret.push_back(res);
            return;
        }
        if(digits[index] == '0' || digits[index] == '1') {
            dfs(digits, index+1, res);
        }
        for(int i=0; i<phone[ digits[index] ].size(); ++i) {
            dfs(digits, index+1, res + phone[digits[index]][i]);
        }
        
    }
};

```