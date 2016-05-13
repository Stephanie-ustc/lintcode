#lintcode 423 有效的括号序列

---
layout: post
category : lintcode
tagline: "lintcode"
tags : [lintcode]
excerpt: 

---
{% include JB/setup %}

##题目

题目链接：http://www.lintcode.com/zh-cn/problem/valid-parentheses/

给定一个字符串所表示的括号序列，包含以下字符： '(', ')', '{', '}', '[' and ']'， 判定是否是有效的括号序列。

您在真实的面试中是否遇到过这个题？ Yes
样例
括号必须依照 "()" 顺序表示， "()[]{}" 是有效的括号，但 "([)]"则是无效的括号。

挑战 
O(n)的时间，n为括号的个数

##解题报告



##Source Code / C++ 

```C++


class Solution {
public:
	/**
	* @param s A string
	* @return whether the string is a valid parentheses
	*/
	bool isleft(char ch) {
		if (ch == '(' || ch == '{' || ch == '[') {
			return true;
		}
		return false;
	}
	bool isValidParentheses(string& s) {
		// Write your code here
		if (s.size() == 0) return true;
		stack<char> sta;
		for (int i = 0; i < s.size(); ++i) {
			if (isleft(s[i])) {
				sta.push(s[i]);
			}
			else {
				if (sta.empty()) return false;
				char top = sta.top();
				sta.pop();
				if (s[i] == ')' && top == '(') {
					;
				}
				else if (s[i] == '}' && top == '{') {
					;
				}
				else if (s[i] == ']' && top == '[') {
					;
				}
				else {
					return false;
				}
			}
		}
		if (sta.empty()) return true;
		else return false;
	}
};

```