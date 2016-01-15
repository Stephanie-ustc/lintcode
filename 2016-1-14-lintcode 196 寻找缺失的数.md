#lintcode 196 寻找缺失的数

---
layout: post
category : lintcode
tagline: "lintcode"
tags : [lintcode]
excerpt: 

---
{% include JB/setup %}

##题目

题目链接：http://www.lintcode.com/zh-cn/problem/find-the-missing-number/

##解题报告

应该有更简单的解法

##Source Code / C++
 
```C++

class Solution {
public:
    /**    
     * @param nums: a vector of integers
     * @return: an integer
     */
    int findMissing(vector<int> &nums) {
        // write your code here
        int sum = (nums.size() ) * (nums.size()+1)/2;
        for(int i= 0; i< nums.size(); ++i) {
            sum -= nums[i];
        }
        return sum;
    }
};

```