#template

---
layout: post
category : lintcode
tagline: "lintcode"
tags : [lintcode]
excerpt: 。
---
{% include JB/setup %}

**解题报告**

简单模拟一下 快乐树的寻找方式即可
不知道有没有更简单的解决方法


**Source Code/ C++**

```
    class Solution {
    public:
        /**
         * @param n an integer
         * @return true if this is a happy number or false
         */
        bool isHappy(int n) {
            // Write your code here
            map <int , int> num;
            
            while ( n != 1 ) {
                int new_num =0;
                int m = n;
                
                while ( m != 0 ) {
                    int rest = m%10;
                    m = m/10;
                    new_num += rest * rest;
                }
                
                if (num.find(new_num) != num.end()) {
                    return false;
                } else {
                    num.insert(make_pair(new_num, 1));
                }
                
                n = new_num;
            }
            return true;
        }
    };
```